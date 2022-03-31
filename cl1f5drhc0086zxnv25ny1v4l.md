## Introducing XdoX - Start Challenges, Log your Progress and Show them off to the World

## 🤔 What is XdoX?

XdoX is a web application that lets you start challenges and log your progress every day. You are also able to show your progress to the world via your unique profile page. These challenges can be anything from 100DaysOfCode to 30DaysOfRust to even 60DaysOfCooking!

It is also my submission for the [Hasura x Hashnode Hackathon](https://townhall.hashnode.com/hasura-hackathon)

[Live Demo](https://xdox.me/) / [GitHub Repository](https://github.com/AnishDe12020/xdox)

## ❓ What is Hasura?

GraphQL is a query language for APIs with a schema. It comes with multiple features like the ability to query specific fields, do pagination, do aggregation queries, and a lot more.

However, making a GraphQL backend is more complicated than making a simple REST backend and that is where Hasura comes in. [Hasura](https://hasura.io/) provides us with an easy way to make a GraphQL backend that connects our database with our application without the need to write a single line of code!

Hasura also has a cloud offering with a decent free tier so that we can get started with hosting our GaphQL backend without needing to worry about costs. It is Open Source and Self-Hostable as well.

## 📚 The Tech Stack

What all technologies did I use for XdoX?

For starters, I used [Hasura](https://hasura.io/) for my application's backend.

Other than that, I used the following services - 

- [Clerk](https://clerk.dev/) to add authentication to my application. It also integrated well with Hasura and I was able to secure my backend by using JWT Auth (more on this later on in this article)

- [Heroku Postgres](https://www.heroku.com/postgres) for my database. It also integrated well with Hasura

- [Vercel](https://vercel.com/) to host my frontend

And, here are the libraries and frameworks I used for the application - 

- [Next.js](https://nextjs.org/) for my application's frontend
- [TailwindCSS](https://tailwindcss.com/) for styling my frontend
- [Radix UI](https://www.radix-ui.com/) for un-styled UI components like Modals and Popovers
- [Headless UI](https://headlessui.dev/) for transitions
- [Apollo React Client](https://www.apollographql.com/docs/react/) for making GraphQL requests from my frontend. It also takes care of caching.
- [Tiptap](https://tiptap.dev/) for the rich-text editor with markdown support that is used to log progress

## 🧐 How does XdoX work?

It is a simple 3-step process. One signs up for an account using Google or Email and then starts a challenge (e.g. 100DaysOfCode). Then one logs their progress every day.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648735974435/jGQ7wv8a0.png)

Next, one can share their unique profile page to the world to show off their progress.

Also, it is not necessary to log your progress every day. The app is built in such a way that lets you be flexible with your challenges. Gone on a vacation? No problem, XdoX won't bug out for not logging your progress.

### Securing the backend

Backends have direct access to the database and it is considered a best practice to secure them. I need to use the GraphQL API from my front-end and hence it has to be a public API. However, I must secure it so that only limited unauthorized requests and authorized requests can be made.

As I was using Clerk for user authentication, it didn't take me long to implement this. Clerk integrated with Hasura using JWT templates. Here is the [documentation explaining how to implement this](https://docs.clerk.dev/integrations/hasura).

Here, we create a JWT template from the Clerk dashboard. Here is what mine looks like - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648723772908/ke9jezE3i.png)

When making a request to the API, we pass in a header called `Authorization` with a bearer token as the value. This is verified by Hasura using a signing key (this is set in Hasura via environment variables). 

This is the code in the frontend that takes care of passing in the bearer token when making requests - 
```ts
import {
  ApolloClient,
  ApolloProvider,
  from,
  HttpLink,
  InMemoryCache,
} from "@apollo/client";
import { setContext } from "@apollo/client/link/context";
import { useSession } from "@clerk/clerk-react";
import { ReactNode } from "react";

const hasuraGraphqlApi = process.env.NEXT_PUBLIC_HASURA_GRAPHQL_API;

interface IApolloProviderWrapperProps {
  children: ReactNode;
}

export const ApolloProviderWrapper = ({
  children,
}: IApolloProviderWrapperProps) => {
  const { getToken } = useSession();
  const authMiddleware = setContext(async (_, { headers }) => {
    const token = await getToken({ template: "hasura" });

    return {
      headers: {
        ...headers,
        authorization: `Bearer ${token}`,
      },
    };
  });

  const httpLink = new HttpLink({
    uri: hasuraGraphqlApi,
  });

  const apolloClient = new ApolloClient({
    link: from([authMiddleware, httpLink]),
    cache: new InMemoryCache(),
  });

  return <ApolloProvider client={apolloClient}>{children}</ApolloProvider>;
};
```

We simply get a bearer token by using the `getToken` function made available to us by the Clerk React SDK and pass it in the `Authorization` header.

Now, if the bearer token is valid, the `X-Hasura-User-Id` header is added to the request that contains the user id of the user who is making the request. The headers for the `user` role are passed in as well. Note that this is taken care of on Hasura's side. 

I am also making some unauthenticated requests with a `viewer` role. This has been set as the unauthorized role in my Hasura instance and is used in the public user profile pages. Here is the code that take cares of making an unauthenticated requests - 
```ts
import {
  ApolloClient,
  ApolloProvider,
  from,
  HttpLink,
  InMemoryCache,
} from "@apollo/client";
import { setContext } from "@apollo/client/link/context";
import { ReactNode } from "react";

const hasuraGraphqlApi = process.env.NEXT_PUBLIC_HASURA_GRAPHQL_API;

interface IApolloProviderWrapperProps {
  children: ReactNode;
}

export const UnauthenticatedApolloProviderWrapper = ({
  children,
}: IApolloProviderWrapperProps) => {
  const authMiddleware = setContext(async (_, { headers }) => {
    return {
      headers: {
        ...headers,
        "X-Hasura-User-Role": "viewer",
      },
    };
  });

  const httpLink = new HttpLink({
    uri: hasuraGraphqlApi,
  });

  const apolloClient = new ApolloClient({
    link: from([authMiddleware, httpLink]),
    cache: new InMemoryCache(),
  });

  return <ApolloProvider client={apolloClient}>{children}</ApolloProvider>;
};
```

### Setting row-level permissions for the data

Although the API is now secured, no data is accessible by default. We need to set up permissions and this will also let us limit the data one can access. For example, we will let a user only access their own user data and only access private challenges they have created.

Thankfully, Hasura again makes doing this extremely easy. Let us look at an example - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648727072397/ZET1GtAf8.png)

Here, I have setup insert permissions for the `user` role in such a way that one can insert rows only where the `user_id` column is equal to the user id of the user making the request (this was passed in as a header).

I am also allowing the `user` to only update specific columns. Here, the `id` column is auto-generated with the `gen_random_uuid()` PostgreSQL function. The `created_at` and `updated_at` fields are also being taken care of by the backend.

I am also adding a column preset for the `user_id` column that will be equal to the `X-Hasura-User-Id` header. Now, that is crazy powerful!

Similarly, I have set permissions for update, select and delete for the `user` role where I check that the `user_id` column matches the `X-Hasura-User-Id` header.

For the `viewer` role, I have set it up this way - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1648733581527/V6oGYUvmP.png)

Here, the viewer is only able to select rows from the database (that is, only read data). I have additionally added a check that makes sure that the challenge is public.

## 👓 What I learned from this Hackathon
Although I have used GraphQL in the past, my experience was quite limited. Also, I had never built a GraphQL backend, I was just using public GraphQL APIs. I had also never used Hasura before, nor did I ever use a SQL database for any production project.

This hackathon gave me a chance to explore the backend side of GraphQL through Hasura and understand the deeper concepts. I also had a great time using a PostgreSQL database, learning more about relational data. It is crazy powerful!

## ✨ Conclusion
Over the past month, I have worked on XdoX and have been exploring and learning a LOT of new things. I'm quite excited to see how XdoX does in the real world!

Bye, and have a nice day 😁🤞

## 🔗 Important Links
- [XdoX](https://www.xdox.me/)
- [XdoX GitHub Repository](https://github.com/AnishDe12020/xdox)
- [My profile on XdoX](https://www.xdox.me/@anishde12020)

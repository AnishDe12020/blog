## Easy Comments - An easy way to add comments functionality to your site

# 👨 Firstly a little bit about myself
I am a 14-year-old Developer, YouTuber, Blogger, and of course a student. Though I have been coding for quite a long time, I started web development about 5 months ago. I learned Javascript, React, Redux, NextJS, various styling libraries, and a lot more in this course of time. Hashnode has now given me an opportunity to show and test my skills through this hackathon.

# 🛡 A few words on [Auth0](https://auth0.com/)
As a part of this hackathon, I am using the popular authentication provider, [Auth0](https://auth0.com/) for user authentication on my application. Auth0 is great to get started (especially with their [quickstarts](https://auth0.com/docs/quickstarts/)) and has a quite generous free tier. The [NextJS SDK](https://github.com/auth0/nextjs-auth0) provides all the basic features along with some advanced ones too and is quite easy to implement and use. There is a Universal Login Page which means one can get started quickly without the need of developing components for that (though you have the option to).

# 🤔 So what have I built?
I started quite late, the 19th of August and I didn't have a lot of time but I was successful in making a Web Application!!! So my app is called [Easy Comments](https://easycomments.anishde.dev/) and it allows you to easily allow comments functionality to your site by adding a simple embed. 

I started doing some mock-ups in my brain. Then I recreated some of them on Figma and then decided to start building. I started with [OpenChakra](https://openchakra.app/) (because I am using [Chakra UI](https://chakra-ui.com/), more on that later).

<details>
<summary>Screenshots</summary>
  <img src="https://i.imgur.com/T7FOqZz.png" alt="Home Page Screenshot" />
  <img src="https://i.imgur.com/avdZnni.png" alt="Sites Page Screenshot" />
  <img src="https://i.imgur.com/S4La8wt.png" alt="Manage Comments Page Screenshot" />
  <img src="https://i.imgur.com/V7Zbzpa.png" alt="My Comments Page Screenshot" />
  <img src="https://i.imgur.com/kbu0jtt.png" alt="Leave a Comment Page Screenshot" />
</details>

## 📚 The stack
I had learned React over the course of over 4 months and also NextJS so I thought of going with NextJS for this project. I also had experience with Chakra UI and found it to be awesome so that is what I am using for styling. 

- [NextJS](https://nextjs.org/)
- [Chakra UI](https://chakra-ui.com/) for styling
- [Firebase](https://firebase.google.com/) for storing data
- [Auth0](https://auth0.com/) for user authentication
- [React Icons](https://react-icons.github.io/react-icons/) and [Chakra Icons](https://chakra-ui.com/docs/media-and-icons/icon#all-icons) for icons
- [React Markdown](https://www.npmjs.com/package/react-markdown) and [Remark GFM](https://github.com/remarkjs/remark-gfm) for markdown supports in comments
- [React Syntax Highligher](https://github.com/react-syntax-highlighter/react-syntax-highlighter) for syntax highlighting of code in comments.
- [Iframe Resizer](https://github.com/davidjbradshaw/iframe-resizer) support
- [Formik](https://formik.org/) for forms
- [Vercel](https://vercel.com/) for hosting

## 👀 The reason
> Why did I make this?

There are many ways of integrating comments onto your site, [Disqus](https://disqus.com/) being a popular option but there is one big issue, trackers. Most of us don't like to be tracked around the web and hence I felt like we need a tracker-free alternative. 

## Features
- No Ads. No Trackers.
- Free and Open Source (Licensed under [MIT](https://opensource.org/licenses/MIT))
- Unlimited Sites
- Unlimited Comments
- Approval stage for Comments (optional)
- Route wise comments
- Ability to edit and delete a Comment
- Markdown support
- Customization of Comments 
- Ability to Self-Host

## ⚙️ How do you use it?
I have written a [quickstart guide](https://github.com/AnishDe12020/easycomments#-guide) on GitHub - https://github.com/AnishDe12020/easycomments#-guide


## 🖧 How does it work?
Once you create a site on the [sites page](https://easycomments.anishde.dev/sites), you get an embed URL upon clicking the "See Embed URL" button (refer the [quickstart](https://github.com/AnishDe12020/easycomments#get-the-embed-url) for more information).

Then it is quite simple, you just need to embed that link on your site but how will you do it?

The embed supports [Iframe Resizer](https://github.com/davidjbradshaw/iframe-resizer) so it is quite simple.

For React - 
```js
<IframeResizer
  style={{
    width: "1px",
    minWidth: "100%",
    height: "1px",
    minHeight: "100%",
  }}
  src="<Your embed url goes here>"
  title="Comments"
/>
```

For Vue refer to this [guide](https://github.com/davidjbradshaw/iframe-resizer/blob/master/docs/use_with/vue.md)

For Angular, you can refer to this [comment](https://github.com/davidjbradshaw/iframe-resizer/issues/478#issuecomment-347958630)

You can refer to the Iframe Resizer [getting started guide](https://github.com/davidjbradshaw/iframe-resizer#getting-started) for more information.

> A sneak peek behind the curtains

```js
<ReactMarkdown
    remarkPlugins={[remarkGfm]}
    components={{
        code({ node, inline, className, children, ...props }) {
        const match = /language-(\w+)/.exec(className || "");
        return !inline && match ? (
            <SyntaxHighlighter
            language={match[1]}
            style={colorMode === "light" ? solarizedlight : dracula}
            PreTag="div"
            {...props}
            >
            {String(children).replace(/\n$/, "")}
            </SyntaxHighlighter>
        ) : (
            <code className={className} {...props}>
            {children}
            </code>
        );
        },
    }}
    >
    {comment}
</ReactMarkdown>;
```

Here [React Markdown](https://www.npmjs.com/package/react-markdown), [React Syntax Highlighter](https://github.com/react-syntax-highlighter/react-syntax-highlighter) and the [Remark GFM](https://github.com/remarkjs/remark-gfm) plugin is used. React Markdown helps with parsing markdown and Remark GFM adds support for GitHub Flavoured Markdown. React Syntax Highlighter does syntax highlighting for code snippets in a comment. 

> How is the embed URL structured?

A sample embed URL - 
```
https://easycomments.anishde.dev/embed/EwI3VgCSuJkl85wh18Ru/
```

Firstly we have the domain, `https://easycomments.anishde.dev`. Then we have the embed route which is a [dynamic route](https://nextjs.org/docs/routing/dynamic-routes) and hence the `siteId` is put as a parameter. We can also add a route, for example - 
```
https://easycomments.anishde.dev/embed/EwI3VgCSuJkl85wh18Ru/easy-comments/
```
Here, comments are stored route-specific. For example, you have a blog, `blog.com`. You can have an embed with the route as `/` (default) for comments left on the home page. Then you can have a route for each blog post with a route, for example, `how-to-add-auth0-to-nextjs` and only comments for that specific blog post will show up when queried with that route.

You can also specify a preferred color mode. By default, the comments widget defaults to the system color mode but this can be overwritten with the `colorMode` parameter in the URL.

Example - 

```
https://easycomments.anishde.dev/embed/EwI3VgCSuJkl85wh18Ru/easy-comments?colorMode=dark
```

The available parameters are `light` and `dark` as of now

# ❓ Some FAQ

> How does one leave a comment?

Each embed has got a "Leave a Comment" link. This redirects the users to a page where one can sign in (if not already signed in) and then leave a comment. 

Example - 
```
https://easycomments.anishde.dev/comments/EwI3VgCSuJkl85wh18Ru
```

> How do comment approvals work?

Comments need to be approved by the site owner unless he/she explicitly enabled auto-approvals of comments when setting up the site or later on through the [sites page](https://easycomments.anishde.dev/sites). If a comment is not approved, the comment won't show up for everyone except the author (who will see a pending badge). The site owner can also remove the comment which then changes the comment status to removed and the comment author sees a removed badge. The site owner can do such comment management via the [manage comments page](https://easycomments.anishde.dev/comments). There is a global manage comments page for all sites the site owner owns and one for each site he/she owns. 

> How can I see comments I have left on other's sites?

The comment will be visible on the site you have left the comment on (along with the status). You can also view all comments that you have left at the [my comments page](https://easycomments.anishde.dev/my-comments) from where you can edit as well as delete a comment (this can be done from the leave a comment page as well)

> What site settings can a site owner change

Right now Show Date, Show Time, Show Avatar and Automatically Approve Comments are the available settings that can be changed by the site owner. In the future, I plan to add support for custom colors and more!!! You can keep an I on the [to-do list](https://github.com/AnishDe12020/easycomments#%EF%B8%8F-to-do). 

# 🎁 Wrapping up

You can see the site live on https://easycomments.anishde.dev/

Source code - https://github.com/AnishDe12020/easycomments

### ⭐ If you liked the project, a star on GitHub would be amazing!!! 🤩
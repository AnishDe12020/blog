## Powerful Code Blocks with Code Hike and MDX

[MDX](https://mdxjs.com/) is a format that combines markup in markdown along with JSX code to embed components into markdown documents. It is used in documentation, blog posts, and much more as one can add interactive examples with JSX. You can learn more about it [here](https://mdxjs.com/docs/what-is-mdx/).

Today, we are going to look at a library called [Code Hike](https://codehike.org/) that provides exceptional features on markdown code blocks. These includes [focussing code](https://codehike.org/demo/code), [adding filenames and displaying them as tabs](https://codehike.org/demo/filenames), [annotations](https://codehike.org/demo/meta-annotations), [linking text to code](https://codehike.org/demo/sections), and much more! It also has in-built support for syntax highlighting 🤩

Let us look at adding Code Hike to a Next.js application. Do note that although MDX is supported by a number of frameworks like Vue, Svelte, etc, Code Hike only works with React.

[Live Demo](https://code-hike-example.vercel.app/) / [GitHub Repository](https://github.com/AnishDe12020/code-hike-example)

## Setting up Code Hike in a Next.js application 
First of all, let us create a new Next.js application - 
```
npx create-next-app code-hike-example
# OR
yarn create next-app code-hike-example
```

Now, open up the project in your favorite text editor.

### Setting up MDX

Next, we need to add MDX to our Next.js application. For this, we are going to be following the [official guide on adding MDX to a Next.js application](https://nextjs.org/docs/advanced-features/using-mdx).

Do note that Code Hike also works with [Next MDX Remote](https://github.com/hashicorp/next-mdx-remote) and [MDX Bundler](https://github.com/kentcdodds/mdx-bundler) however, we are going to look at a simple example with the [official MDX plugin for Next.js](https://www.npmjs.com/package/@next/mdx).

First of all, let us install the required packages - 
```
npm install @next/mdx @mdx-js/loader
# OR
yarn add @next/mdx @mdx-js/loader 
```

Now, open up `next.config.js` and replace it with the following code - 
```js
const withMDX = require("@next/mdx")({
  extension: /\.mdx?$/,
  options: {
    remarkPlugins: [],
    rehypePlugins: [],
  },
});

module.exports = withMDX({
  pageExtensions: ["ts", "tsx", "js", "jsx", "md", "mdx"],
})
```

We are simply telling our bundler to treat `.md` and `.mdx` files as pages as well when they are in the `pages` directory. This also takes care of compiling our MDX.

Now, let us setup Code Hike

### Setting up Code Hike
First of all, let us install the [Code Hike Package](https://www.npmjs.com/package/@code-hike/mdx)

```
npm install @code-hike/mdx@next
# OR
yarn add @code-hike/mdx@next
```

Now, we must add Code Hike as a [Remark](https://remark.js.org/) plugin. Remark is a simple markdown processor that has a huge ecosystem of plugins.

```js 
const { remarkCodeHike } = require("@code-hike/mdx");

const withMDX = require("@next/mdx")({
  extension: /\.mdx?$/,
  options: {
    remarkPlugins: [[remarkCodeHike]],
    rehypePlugins: [],
  },
});

module.exports = withMDX({
  pageExtensions: ["ts", "tsx", "js", "jsx", "md", "mdx"],
});
```

Code Hike uses [Shiki](https://github.com/shikijs/shiki) under the hood to provide syntax highlighting. We can find a list of all the supported themes [here](https://github.com/shikijs/shiki/blob/main/docs/themes.md#all-themes). Let us go with Monokai for this tutorial.
```js
const { remarkCodeHike } = require("@code-hike/mdx");
const theme = require("shiki/themes/monokai.json");

const withMDX = require("@next/mdx")({
  extension: /\.mdx?$/,
  options: {
    remarkPlugins: [[remarkCodeHike, { theme }]],
    rehypePlugins: [],
  },
});

module.exports = withMDX({
  pageExtensions: ["ts", "tsx", "js", "jsx", "md", "mdx"],
});
```

There is one last thing to do. We need to add the Code Hike CSS to our application. Open up `_app.js` and add this one line of code to the top
```js
import "@code-hike/mdx/dist/index.css"
```

## Testing out Code Hike
Let us make a new file called `code-hike.mdx` under the `pages` directory. Add the following mdx markup in there - 
````md
# Just testing out [Code Hike](https://codehike.org/)

Some normal `markdown`

## Annotation Example
```js index.js box=1[25:39]
console.log("Some code. I am annotated!")
```

## Focus Example
```js next.config.js focus=1:2,7
const { remarkCodeHike } = require("@code-hike/mdx");
const theme = require("shiki/themes/monokai.json");

const withMDX = require("@next/mdx")({
  extension: /\.mdx?$/,
  options: {
    remarkPlugins: [[remarkCodeHike, { theme }]],
    rehypePlugins: [],
  },
});

module.exports = withMDX({
  pageExtensions: ["ts", "tsx", "js", "jsx", "md", "mdx"],
});
```

<CH.Section>

## Code Links Example

We are looking at the [console.log](focus://console.js#2) function today

<CH.Code>
```js console.js
console.table(["Hello", "World"])
console.log("Hello World")
```
</CH.Code>

</CH.Section>
````

Here, we are writing some basic markdown at first and then adding 3 code blocks. In all 3 of them, I have provided a filename just after specifying the language (`js` in these 3 cases).

In the first code block, we pass in the `box` attribute after the filename. We set it to `1[25:39]` where `1` indicated the line number and `25:39` indicates the range of characters to annotate on that line.

Similarly, in the second code block, we pass in the `focus` attribute and set it to `1:2,7`. Here `1:2` indicates a range of lines to be put on focus. We also add line 7 by adding it as a comma-separated value.

For the third code block, we have to wrap the content and code block in the `CH.Section` tag. We must also wrap the code block in the `CH.Code` tag. This is so that Code Hike knows which file we are going to be referring to through the code links when we specify the filename.

We have `console.log` as a code link here that points to `focus://console.js#2`. This indicates that whenever we hover over that code link, it will focus the second line in the  `console.js` code block.

At last, this is what it should look like when we navigate to [`/code-hike`](http://localhost:3000/code-hike)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1646557043098/Zgwdl-v55.png)

Yes, those box shadows are cool 👀

## Conclusion
That was a brief overview of Code Hike. Code Hike supports many more things like [Scrollycoding](https://codehike.org/demo/scrollycoding) and previews as well. Code Hike is still in a beta stage and many features are still experimental.

Hope everything went well so far and now you can use Code Hike in your blog or documentation to achieve extremely powerful code blocks!

See you in the next one 😁🤞

## 🔗 Important Links
- [Code Hike](https://codehike.org/)
- [Code Hike GitHub Repository](https://github.com/code-hike/codehike)
- [GitHub Repository for this tutorial](https://github.com/AnishDe12020/code-hike-example)
- [Deployed Preview for this tutorial](https://code-hike-example.vercel.app/)
## Create an NPX CLI Portfolio under 5 minutes

![npx-cli-portfolio.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1632121300335/gd5ezLkxf.gif)

Want something like this? This is the article you are looking for. Let me show you how you can make an NPX CLI Portfolio under 5 minutes

# How I made it
I am mainly using [React Ink](https://github.com/vadimdemedes/ink) for this project. I have also written a [Getting started with React Ink](https://blog.anishde.dev/getting-started-with-react-ink) article which you can check out. The goal was to make a portfolio that can be viewed in the terminal. At first, I just did a console log which logged out information about me but once I found out about React Ink, I thought of using that and making it better. The advantage of using React Ink is that it is way more flexible than simple console logs and hence I was able to put custom colors (theoretically you can apply a color to a console log but options are quite limited). Using React also allowed me to make a reusable component and hence the number of fields showing up and the contents are dynamic, based on a `data.json` file.

# How you can make it as well
I have made a template in GitHub (which you can find [here](https://github.com/AnishDe12020/cli-portfolio-template)) which you can use. You can find a detailed guide [here](https://github.com/AnishDe12020/cli-portfolio-template#how-to-use-this-template).

# Things to keep in mind
- If someone has already made a package with the same name on NPM, then you need to choose something else
- NPM version 5.2 is needed at a minimum to use NPX (it can be used as a standalone package though)
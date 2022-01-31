## TwNFT - Mint your tweets as NFTs easily and for free

![let-us-get-started-minions](https://cdn.hashnode.com/res/hashnode/image/upload/v1643621521059/4bLysGMEz.gif)

## 🤔 What is TwNFT?

TwNFT is a simple web application that allows you to mint your tweets as **NFTs** for free.

It is my submission for the [Thirdweb x Hashnode Hackathon](https://townhall.hashnode.com/thirdweb-hackathon).

[Live Demo](https://twnft.vercel.app/) / [GitHub Repository](https://github.com/AnishDe12020/twnft)

## 🌐 What is Thirdweb?

Getting started with web3 can be difficult even though it is the hype nowadays. We need to write something called a smart contract, which is required to perform actions on the blockchain. To write smart contracts on the Ethereum blockchain, we need to learn a new programming language called [Solidity](https://soliditylang.org/).

[Thirdweb](https://thirdweb.com/) provides us with smart contracts which have been written by professionals in the field. They also provide us SDKs which makes using these easy. This allows people with basic programming knowledge to make web3 applications with ease. Thirdweb also takes care of deploying these smart contracts to the blockchain.

Let us now go back to TwNFT

## 💡Where did the idea come from?
This hackathon was announced back on the 5th of January, 2022 but I didn't get a solid idea until the 18th of January. So where did it come from?

I came across an application called [GitNFT](https://gitnft.quine.sh/) from one of @[Chris Bongers](@dailydevtips)'s articles. GitNFT lets you mint git commits as NFTs and that is when I thought, "How about minting tweets as NFTs?". 

I did some research and didn't find any application that did this so it was a golden opportunity for me 🤩


## 📚 The tech stack
What technologies did I use for TwNFT?
- [NextJS](https://nextjs.org/) for the website
- [TailwindCSS](https://tailwindcss.com/) for styling
- [Firebase](https://firebase.google.com/) for Twitter authentication and data storage
- [Vercel](https://vercel.com/) for deploying the frontend
- [Express](https://www.npmjs.com/package/express) for the backend API
- [Heroku](https://dashboard.heroku.com/apps) to deploy the backend

and of course...
- [Thirdweb](https://thirdweb.com/) for web3 authentication and minting the NFT

## 🧐 How does TwNFT work?

One needs to first sign in with Twitter and then put in the tweet URL for the tweet they want to mint. Before minting, the image that will be minted can also be customized. One needs to assign a name to the NFT and optionally add a description (or else, the tweet's content will be used).

Before minting, we have 2 checks to ensure that the person minting the NFT owns that tweet (this is why they are asked to log in with Twitter) and if the tweet has been minted before or not. We don't allow minting the same tweet multiple times, and this is to ensure that every NFT minted is unique. 

Now let us take a deeper dive into the web3 part

### A deeper dive into web3 authentication with Thirdweb

Setting up authentication with Thirdweb is as easy as adding ~10 lines of code. I am using the [`@3rdweb/hooks`](https://www.npmjs.com/package/@3rdweb/hooks) package for this application and it is a breeze. The [`@3rdweb/react`](https://www.npmjs.com/package/@3rdweb/react) package is easier to implement as it also packs in the UI. However, if you want a custom UI (which I wanted), the hooks package is a better choice.

Do note that you need to be using [ReactJS](https://reactjs.org/) to use any of the aforementioned packages.

Coming to the code, firstly, you need to add the Thirdweb Provider to the application - 
```jsx
import { ThirdwebWeb3Provider } from "@3rdweb/hooks";

const connectors = {
  injected: {},
  walletconnect: {},
};

const supportedChainIds = [1, 4, 137, 250, 43114, 80001];

function MyApp({ Component, pageProps }) {
  return (
    <ThirdwebWeb3Provider
      connectors={connectors}
      supportedChainIds={supportedChainIds}
    >
      <Component {...pageProps} />
    </ThirdwebWeb3Provider>
  );
}
```

Then, it is as easy of using the `useWeb3()` hook provided to us by either packages to retrieve the `connectWallet` function. We have to now just call this function with the wallet type - 
```jsx
<button
  onClick={() => {
    connectWallet("injected");
  }}
  >
  Login with Metamask
</button>
```

Here `injected` is for the wallet injected in the browser. This is [Metamask](https://metamask.io/) in most cases.

For a detailed guide on implementing web3 authentication with Thirdweb, check out their [official guide](https://thirdweb.com/portal/guides/sign-in-with-ethereum-using-thirdweb-connectwallet).

### A deeper dive into minting the NFT with Thirdweb
I am using the [Thirdweb Typescript SDK](https://www.npmjs.com/package/@3rdweb/SDK) for minting the NFT on the server-side. Minting should take place on the server-side for security reasons.

Minting with the Thirdweb SDK is extremely easy. Let us see how it works - 

First, we initialize the SDK with our private key. Do keep this secret as anyone who has your private key can gain access to your wallet. I am using [`ethers`](https://www.npmjs.com/package/ethers) for initializing a wallet here.
```ts
const SDK = new ThirdwebSDK(
  new ethers.Wallet(
    process.env.PRIVATE_KEY,
    ethers.getDefaultProvider("https://rinkeby-light.eth.linkpool.io/")
  )
);
```

Next, we initialize the NFT Module that will let us mint the NFT - 
```ts
const nftModule = sdk.getNFTModule(process.env.NFT_MODULE_ADDRESS);
```

At last, we call the `mintTo` function asynchronously - 
```ts
const result = await nftModule.mintTo(
  payload.receiverAddress,
  nftMedatada
);
```

Here the result gives us the NFT's `tokenId`. The `tokenId` is a unique identifier for the NFT in that collection. 

Now, that is it. We have minted an NFT!!!

For a more detailed guide, you can check out Thirdweb's [official guide on minting an NFT](https://thirdweb.com/portal/guides/mint-nft-collection-using-typescript-sdk).

### ❓ What was this NFT Module?
Thirdweb provides us with many modules and the NFT Collection module is one of them. It allows you to mint an NFT in an NFT collection and that is what we just did!!! 
The official collection for this project can be found on OpenSea [here](https://testnets.opensea.io/collection/twnft).

## 🖱️ Using TwNFT

To get started, log in with Twitter and head over to the [/mint](https://twnft.vercel.app/mint) page. 

Next, put in the URL to the tweet you want to mint in the textbox on the top and click the arrow -

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643624998718/ui-X376Lf.png)

You should now see a preview of the NFT, something a bit like this - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643625030434/G2CF1HC0ZQ.png)

Feel free to customize the image by clicking on the buttons on the options bar - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643625193144/G3fFrq2n1.png)

Next, click on the "Connect Wallet" button and connect your Metamask wallet. Walletconnect support is coming soon.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643625230012/X2U4fiR74.png)

You should now see a button saying "Mint NFT" instead of "Connect Wallet" on the options bar. Clicking that should bring up this modal where you can fill out the name of the NFT, and optionally add a description - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643625284907/1qDxme8Wh.png)
 
After some time, you should get the option to go to the tweet page - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643625434052/po2NcD7zd.png)

The tweet page will look somewhat like this (do give the image some time to load for the first time) - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643625465700/gVijzcG5w.png)

Notice that it says the NFT is still being minted and it is going to take 5-10 minutes. Check back after 5-10 minutes and this is what the page should look like - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1643625506211/EFaHw8vDeU.png)

The NFT is now under your wallet and you can do anything with it, including listing it for sale, selling it, and even transferring it to another wallet. 

## 🖊️ Sidenote
Currently, TwNFT is running on the Rinkeby Test Network. This means all NFTs minted will be on the test network and not on the main network.

However, this is subject to change in the future.

## ✨ Conclusion
It has been a great journey over the last 13 days making TwNFT, squashing bugs, and implementing features. Excited to see how it goes 😆

Bye, and have a nice day 😁🤞

## 🔗 Important Links
- [TwNFT](https://twnft.vercel.app/)
- [TwNFT GitHub Repository](https://github.com/AnishDe12020/twnft)
- [TwNFT Backend GitHub Repository](https://github.com/AnishDe12020/twnft-backend)
- [TwNFT OpenSea collection](https://testnets.opensea.io/collection/twnft)
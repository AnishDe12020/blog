## How to quickly create a Gasless NFT Collection on Solana with CandyPay

Let's say you are an NFT creator and want to publish your NFT onto the Solana blockchain quickly. This can be time-consuming as it involves creating the collection, setting up a minting website, etc. It also requires you to be familiar with all the technologies and as a creator, you may not be familiar with all the development stuff. 

That is where [CandyPay](https://candypay.fun/) comes in. CandyPay lets you create NFTs with a no-code builder and also lets users easily claim them via [Solana Pay](https://solanapay.com/) on mobile without worrying about installing any browser extension or connecting their wallet.

Additionally, we are going to be looking at gasless NFTs which do not cost any SOL to the receiver to claim. Instead, we, the creator of the NFT pre-pay the gas. Note that we can get back our SOL if any of the pre-paid SOL remains unused.

## Prerequisites
All of these don't require you to pay any real money.
- A Solana wallet with Solana pay support. You can use [Phantom](https://phantom.app/) or [Solflare](https://solflare.com/), both of which are available for Android, iOS, and as a browser extension as well although you will need the mobile app for Solana pay.
- An image to upload as an NFT (you can use anything for this as we are going to be doing it on the devnet anyways). I am going to be using this one, feel free to use it for this tutorial - 

![The NFT.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661607325449/5kqGckuOX.png)

- Some devnet SOL. You can get it from [a Solana faucet](https://solfaucet.com/) (it is free and no signup is required)

## Creating a Gasless NFT collection with CandyPay
First of all, we need to create a CandyPay account. Head over to [the CandyPay web app](https://candypay.fun/) and sign up for an account. 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661599679040/kIXFWJYte.png)

Next, select "Gasless Collection" under the "Create New" dropdown

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661600362928/NwPTXXPiT.png)

Here, we have to provide some details about the NFT, and of course, the image itself. Here is an explanation of the various fields - 
- NFT Name (required) - The name of the NFT
- NFT Description - You may want to add a description describing what the NFT is about, its importance, etc.
- Wallet Address - Your Solana wallet address
- Symbol - You can provide a symbol for your NFT. This is usually shown in marketplaces and wallet apps
- Royalty Fee - For any subsequent sales after the first one, this much percent of the amount will be given to you as royalty
- Collection size (required) - The number of NFTs the collection is going to have
- External URL - Any URL which you want to associate with your NFT
- Network - The Solana network you want to publish your collection to. When building a production app, you should choose "Mainnet" (and it will cost some real money in the form of real SOL to publish the collection and pre-pay the gas) but for the purpose of this tutorial, we are choosing "Devnet" (we are going to be using the devnet SOL we got from the faucet, which didn't cost us any real money)
- NFT Image (required) - The image that will be used for the NFT

I have entered the values for these fields as follows - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661669840416/U31BTyY4f.png)

Now click on "Continue". In the next page, we can customize our CandyPay QR code. This will be the QR Code that the receiver of the NFT will scan in order to get the NFT, so let us try to make it beautiful :)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661609022601/Hf9MSuH1F.png)

I have changed some of the shapes, and also changed the black CandyPay logo to one with the CandyPay accent color :)

Now again click "Continue". In the next step, we have to pay some SOL to create the collection as well as the gas for the 10 NFTs. Note that we can redeem any unused funds later on. 

Scan this QR Code with your mobile wallet app and you should see a Solana Pay popup. If you see an error in Phantom which looks like this, try using Solflare (in Solflare, it is a 2 step process and the UI is a little different but the result is the same) -  

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661669446505/wEIPvotEW.png)

After scanning the QR Code, you should see something like this on your mobile wallet app - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661669794663/tpyrLNLTS.png)

Pay the devnet SOL and let the transaction succeed (shouldn't take more than 10 seconds). After that, you should see a success message in CandyPay - 

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661670086416/9OQ4F3BPU.png)

On the collection dashboard, you will be able to see the QR code one can scan to redeem the NFT. There is a link as well which one can open on their phone to redeem the NFT. 

Oh, by the way, that QR code in the screenshot actually works so you can try to scan the QR code to get this NFT until supply lasts of course.

## Claiming an NFT using the CandyPay QR Code
If I now scan the QR Code, I will be prompted to confirm a transaction but notice that no SOL is getting deducted from my side, so it is gasless! (I had to do it with Solflare this time as Phantom errored out)

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661672602690/d0D4Oq1Mt.png)

Now if I go back to the dashboard, I can see that 1 NFT has been redeemed (ignore the cancelled ones as it was just Phantom being buggy). The gas has been deducted as well!

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661672708481/kRz7UFp2b.png)

For more clarity on if I had to pay gas or not, if I check the [transaction on Solscan](https://solscan.io/tx/3z5U4gmVJUtPVe4YuFKj29A1JJZiqY4MtLy4pokzJ2DKZ8vi7ibCTcuU78jtqqcdfw49qKH7Wxg9WbB8tJ9rEJHh?cluster=devnet), under the "SOL Balance Change" tab, I can see that there was no change in my SOL balance.

![image.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1661673463418/0YgBR6q9q.png)

## Conclusion
Now it's time for you to ship your gasless NFT collections! Feel free to share them down below, really excited to see what y'all build :)

## Important Links
- [CandyPay](https://candypay.fun/)
- [CandyPay Discord Server](https://discord.com/invite/VGjPXWUHGT) (you can get support here)
- [Solana Pay](https://solanapay.com/)
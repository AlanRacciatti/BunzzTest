This is a [Next.js](https://nextjs.org/) project bootstrapped with 
[`create-next-app`](https://github.com/vercel/next.js/tree/canary/packages/create-next-app).

## Getting Started

First, run the development server:

```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) with your browser to see the result.

You can start editing the page by modifying `pages/index.js`. The page auto-updates as you edit the file.

[API routes](https://nextjs.org/docs/api-routes/introduction) can be accessed on [http://localhost:3000/api/hello](http://localhost:3000/api/hello). This endpoint can be edited in `pages/api/hello.js`.

The `pages/api` directory is mapped to `/api/*`. Files in this directory are treated as [API routes](https://nextjs.org/docs/api-routes/introduction) instead of React pages.

## Learn More

To learn more about Next.js, take a look at the following resources:

- [Next.js Documentation](https://nextjs.org/docs) - learn about Next.js features and API.
- [Learn Next.js](https://nextjs.org/learn) - an interactive Next.js tutorial.

You can check out [the Next.js GitHub repository](https://github.com/vercel/next.js/) - your feedback and contributions are welcome!

## Deploy on Vercel

The easiest way to deploy your Next.js app is to use the [Vercel Platform](https://vercel.com/new?utm_medium=default-template&filter=next.js&utm_source=create-next-app&utm_campaign=create-next-app-readme) from the creators of Next.js.

Check out our [Next.js deployment documentation](https://nextjs.org/docs/deployment) for more details.
### Welcome
This document was made in order to keep track of my whole experience 
working with Bunzz. It might include bugs found and things that (in my 
opinion) can be improved. Although it is possible that I report bugs not 
related with the job I was encommend to do, my focus will be in **make a 
DApp following ONLY the documentation provided by Bunzz**

### Working in the Grouped NFT Project

##### Improvement proposal #1
In the **create dapp page**, when you are creating the app and it asks to 
put a initCost, it is in WEI, so it would be really hard to put 0.1 ETH as 
the price for example.

Recommendation: It would be great that people can select the unit of 
measure to be used. Like remix
![[Screen Shot 2022-10-19 at 18.31.52.png]]

##### Bug found #1
In the **create dapp page**, when clicking the deploy button to deploy the 
contract. If the wallet isn't connected, nothing happens.

Recommendation: When clicking the deploy button, if there isn't an account 
connected, it should throw an error alert that a wallet must be connected. 

##### Improvement proposal #2
When deploying the contract (in the moment when you accept the tx and the 
loader starts spinning), it would be great if there was a button to the 
transaction in etherescan so people can see it, otherwise, they will have 
to wait for some minutes just watching the loader and can think that the 
app crashed

##### Bug found #2
I first connected to a wallet (from now wallet 1), but after creating the 
app, I switched to other wallet (now wallet 2) because it had goerli eth, 
and deployed the contract with it. I've checked and the owner of the 
contract is wallet 2, but it is showing me a error that I'm connected to a 
different wallet that deployed the contract (it shows wallet 1)

Recommendation: I don't know how you manage the wallet owner of a project, 
but it would be good if it is defined based on the address that actually 
made the deploy of the contract.

##### Improvement proposal #3
After making the deploy, the deploy button is still available to click, 
and when you click it, the modal for deploying the contract appears with 
the data that the contract has already been deployed.

Recommendation: If the contract is deployed, remove the deploy button

##### Improvement proposal #4
When you deployed the contract, it is possible to copy the contract 
address, but there isn't any link to go to it in the block explorer on 
etherscan for example.

Recommendation: Add a button that sends you to the contract that you 
deployed in the block explorer

##### Improvement proposal #5
Events listener are a must for most of the DApps and Bunzz doesn't seem to 
support them. This is really useful for developers to improve the UX

Recommendation: Contracts should have a `to` method that allows to handle 
events. Example below
```js
contract.on("mint", (args) => {
	alert(`You have minted the NFT with id ${args.id}`)
})

// Other solution can be this
contract.mint.addEventListener(args => {
	alert(`You have minted the NFT with id ${args.id}`)
})
```

Improvement proposal #6
Currently, when you want to put the value to be sent when making a 
transaction, the unique unit of measure is wei, making it hard for 
beginner how much ETH it is exactly

Recommendation: Create a unit parser function, or even use the web3 or 
ethers one, that works like this:
`ethers.utils.parseEther("1") // Equals to 1000000000000000000 WEI

Improvement proposal #7
In the dapp page, where you can interact with the contract with the 
buttons, for a non-solidity developer it can be hard to understand what 
those functions do

Recommendation: Add a description of the function when clicking the arrow 
for interacting with the contract

### Documentation
##### Improvement proposal #1
Both the Transaction and ReadResponse pages, don't start telling where the 
object is get. 

Recommendation: At the beginning of the page, explain that 
transaction/ReadResponse objects are get when it is called an update/read 
method method of a contract



### Other bugs

#### Sign up page (bug found)
If you go to the [sign up page](https://app.bunzz.dev/signup), when you 
try to create a new account, and the username is already taken, it just 
changes the border of the input to red and shows the error in console.

![[Screen Shot 2022-10-19 at 16.13.23.png]]
![[Screen Shot 2022-10-19 at 16.14.05.png]]

##### Recommendations
- **Useful**: When the error is thrown, change the help text color to red 
and the text to _Username already taken_ 
- **Best UX**: Check if the username (and email probably) already exist 
and show the error if it already does. _Note: To not make a request in 
every input, it would be a good idea to use a 
[debounce](https://www.freecodecamp.org/news/javascript-debounce-example/) 
function_


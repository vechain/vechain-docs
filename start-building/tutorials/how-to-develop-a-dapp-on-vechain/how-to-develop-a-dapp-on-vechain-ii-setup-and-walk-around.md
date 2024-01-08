# How To Develop a dApp on vechain (II): Setup & Walk Around

Sync: Desktop vechain DApp environment.

### Setup in 3 minutes <a href="#setup-in-3-minutes" id="setup-in-3-minutes"></a>

Great! I see you have survived the last tutorial, now it is time to start programming. The first thing we need is a [Sync ](https://env.vechain.org/)environment.

![](https://cdn-images-1.medium.com/max/2000/1\*7FfxBwANrBsplfl3DYzDgw.jpeg)

Okay now let’s clone the Sync project source code in a terminal and spin it up in _**dev mode**_:

```bash
mkdir playgrounds

cd playgrounds/

git clone [git@github.com](mailto:git@github.com):vechain/thor-sync.electron.git

cd thor-sync.electron/

node -v # Make sure you have node.js >V10.0.0 installed

npm install # Install dependencies

npm run dev # Boot the Sync in dev mode
```

When you see the Sync electron window popping up, we are all set!

<figure><img src="https://cdn-images-1.medium.com/max/4744/1*FacLnaprgduDltjvHP4w_w.png" alt=""><figcaption><p><em>Boot up: npm run dev</em></p></figcaption></figure>

### Poke around: Familiar with Sync <a href="#poke-around-familiar-with-sync" id="poke-around-familiar-with-sync"></a>

Okay, now let us put aside the terminal and focus more on the GUI window. Sync is a browser-like wallet that embedded with Connex.js library which can offer the web page running inside it the ability to communicate with VechainThor blockchain.

#### Create a Testing Wallet <a href="#create-a-testing-wallet" id="create-a-testing-wallet"></a>

First, Let us set up a testing wallet for ourselves:

<figure><img src="https://cdn-images-1.medium.com/max/7080/1*vfVH2dlr_32_sno4-0HZLg.jpeg" alt=""><figcaption><p><em>Go to wallet panel to view existing wallets.</em></p></figcaption></figure>

Great, now click on the upper-right “**wallets**” icon, if you are on test net, there are already 3 wallets available for testing: “Foo”, “Baz” and “Bar”. Leave them alone, let us click the “**Create**” button to create a fresh one.

![](https://cdn-images-1.medium.com/max/6400/1\*etIhDSEXvDyHw1FpSY-vqA.jpeg)

<figure><img src="https://cdn-images-1.medium.com/max/6400/1*UOXWEwByxWJPIOaLlkwq5A.jpeg" alt=""><figcaption><p><em>Create a new wallet for our testing</em></p></figcaption></figure>

Follow the instructions on Sync now I have a wallet with a public address, it currently contains 0 VET and 0 VTHO：

> 0xa7a609b928c4eac077d0e5640f3fa650746c4fcf

#### Fuel the wallet with VTHO <a href="#fuel-the-wallet-with-vtho" id="fuel-the-wallet-with-vtho"></a>

**Next**, we fill up the newly created wallet by adding some VTHO funds to it. VTHO is used as the fee fuelling the transactions and on test net. Where to get it? The vechain core team’s dApp demo: **VET/VTHO faucet**!

Go on, visit the web URL: [https://faucet.vecha.in ](https://faucet.vecha.in/)in Sync, and you will see an interesting web page that gives out VTHO on test net for free:

![](https://cdn-images-1.medium.com/max/7272/1\*ZgEaFQRNUevnW0VWE6TuDA.jpeg)

<figure><img src="https://cdn-images-1.medium.com/max/7320/1*nNP5RYNvqjgEsJpSo78QPw.jpeg" alt=""><figcaption><p><em>Get free VET/VTHO on test net</em></p></figcaption></figure>

Follow the “**Claim Tokens**” button in the middle of the web page and let’s get some free VET/VTHO for testing. Do remember to choose the wallet you created, and input the password accordingly to claim the tokens. I have already claimed 500 VET with 500 VTHO. 😉

![](https://cdn-images-1.medium.com/max/2000/1\*tMo5kR-BoY9ATD7AEb1XxA.jpeg)

### **Play with Connex.js APIs** <a href="#play-with-connex-js-apis" id="play-with-connex-js-apis"></a>

Now that we have money on test net, let's move on to explore the blockchain functionalities provided by Sync, the **connex.js** library. Let us **open up a new blank tab**, then toggle the developer tools to see what is connex used for:

![](https://cdn-images-1.medium.com/max/3540/1\*hFt55F2\_aQAvRs6FhOgpng.png)

<figure><img src="https://cdn-images-1.medium.com/max/6968/1*ewTOVmlV7wzA4khlgxN-7Q.jpeg" alt=""><figcaption><p><em>Open Developer Tools to visit Connex.</em></p></figcaption></figure>

Once on the console of the developer tools (Just like Chrome developer tools), type in following code:

```bash
    connex

     {version: "1.2.0", thor: {…}, vendor: {…}}
    thor:{ticker: ƒ, account: ƒ, block: ƒ, …}
    vendor:{sign: ƒ, owned: ƒ}
    version:"1.2.0"
    __proto__:Object
```

Yep, each and every window **has already implanted** **the connex object** in the web page. And this connex object can do a lot of things with VeChain network, Let us explore some simple ones:

#### Play with account() <a href="#play-with-account" id="play-with-account"></a>

```javascript
var acc = connex.thor.account('0xa7a609b928c4eac077d0e5640f3fa650746c4fcf')

acc.get().then(info=>{console.log(info)})

Promise {<pending>}
{balance: "0x1b1ae4d6e2ef500000", energy: "0x1b1af7398584067000", hasCode: false}

parseInt('0x1b1ae4d6e2ef500000') 

500000000000000000000

parseInt('0x1b1af7398584067000')

500005175000000000000
```

Here I just queried my newly created wallet, which results in a response object of “balance”, “energy” and “hasCode” fields. “balance” is the VET this account holds, and “energy” is the VTHO amount.

#### Play with ticker() <a href="#play-with-ticker" id="play-with-ticker"></a>

In vechain network, we don’t know exactly _**when**_ a new block is produced, but we surely want to be notified when it is produced. ticker gives us this peek hole to get notified. We still use the debug console in Sync:

```javascript
var t = connex.thor.ticker()
undefined

t.next().then(()=>{console.log('new block!')})
new block!
```

Cool right? After around 3–10 seconds this “new block!” message is printed and we know there is a new block added to the top of the chain.

> ticker is a Promise that is never rejected, so we only need to supply a resolve function. We no longer need setTimeout function!

#### Play with call() <a href="#play-with-call" id="play-with-call"></a>

Actually, the \*\*VTHO contract itself is an [ERC20 ](https://en.wikipedia.org/wiki/ERC-20)/[VIP180 ](https://github.com/vechain/VIPs/blob/master/VIP-180-EN.md)compatible contract \*\*living on the VeChain! And you know what, I happen to know the address of it on the testnet: 😜

> ### 0x0000000000000000000000000000456e65726779 <a href="#_0x0000000000000000000000000000456e65726779" id="_0x0000000000000000000000000000456e65726779"></a>

For those who don’t understand ERC20/VIP180, a contract is a long living object on the blockchain. Thinking of it as a set of program instructions and a simple free-form permanent storage that the program controls it. ERC20/VIP180 contracts are simple “virtual bank” program which keeps track on each client and his balance of a specific virtual coin/token.

So, we have the address of a contract, how do we call it? Very simple.

```javascript
const balanceOfABI = {
   'constant': true,
   'inputs': [
     { 
       'name': '_owner',
       'type': 'address'
     }
   ],    
   'name': 'balanceOf',
   'outputs': [
     { 
      'name': 'balance',
      'type': 'uint256'
     }
   ],
   'payable': false,
   'stateMutability': 'view',
   'type': 'function'
}

const balanceOfMethod = connex.thor.account('0x0000000000000000000000000000456e65726779').method(balanceOfABI)

const balanceInfo = await balanceOfMethod.call('0xa7a609b928c4eac077d0e5640f3fa650746c4fcf')

console.log(balanceInfo)
{data: "0x00000000000000000000000000000000000000000000001b1b428acf29437000", events: Array(0), transfers: Array(0), gasUsed: 870, reverted: false, …}
```

We first supply the contract method ABI (function signature) and then create a handler with the contract deploy address. Finally, we call the contract method with call() and supply it with a parameter, an address of the account we are interested. Great! Now we have the result!

### Summary <a href="#summary" id="summary"></a>

Enough for today’s study!

To recap, we have:

1. Walked you through the installation of Sync.
2. Run an example dApp in Sync and get some free VET/VTHO.
3. Play with vechain blockchain with the pre-implanted connex javascript object.

Starting from the next tutorial, we will use our knowledge learned today and build a web page (front-end) of _**an existing smart contract**_, VTHO contract (Yes, some good guy has done it for us, we simply borrow it). Be ready and let’s go!

![](https://cdn-images-1.medium.com/max/2000/1\*4qhRKktZlKxSxo70EH78Gw.jpeg)

# How To Develop a dApp on vechain (I)：Intro

Recently I have been working on a dApp tool on vechain. However, I searched a lot but couldn't find any hands-on tutorial for developers. I decided to go for it and shed some light on this topic. In this tutorial, I will walk through with you guys about _how to_ build up an ERC20/VIP180 standard token transfer web page\*\* on vechain.

This tutorial splits into 3 parts, the topics are:

* [Intro](how-to-develop-a-dapp-on-vechain-i-intro.md).
* [Setup & Walk Around](how-to-develop-a-dapp-on-vechain-ii-setup-and-walk-around.md).
* [Components & Coding](how-to-develop-a-dapp-on-vechain-iii-components-and-coding.md).

Ready? Let us get our hands dirty! 😉

### What is dApp? <a href="#what-is-dapp" id="what-is-dapp"></a>

![](https://cdn-images-1.medium.com/max/2000/1\*qpy5NueXgD2PJFJWupJP5g.jpeg)

Many people ask me as a blockchain developer, what is a **d**_**App**_? In one of my simpler version of the answers, “**dApp = Web + Blockchain**”. Yep, the current web technologies are still heavily used. We simply move some data and authentication onto the blockchain, that’s it. It’s the same idea behind [Web3.js](https://github.com/ethereum/web3.js/), as well as the [Connex.js ](https://www.npmjs.com/package/@vechain/connex)we will be talking about later.

To answer that, we first look at what a traditional _**web application**_ looks like:

<figure><img src="https://cdn-images-1.medium.com/max/3528/1*tY6R3nkcaTEEDNFR4RD49g.jpeg" alt=""><figcaption><p><em>Web app: client, server and database.</em></p></figcaption></figure>

#### What’s Web Application? <a href="#what-s-web-application" id="what-s-web-application"></a>

A _**web application**_ in a simplified scenario is a typical client-server application. It contains several critical parts:

* **Client**: web browsers.
* **Server**: operates the database, serves the clients data.
* **Database**: stores the data as valuable assets. 😛

Interestingly, in a web application, _**data is at the core heart**_. It flows, displayed, transformed and stored in the system. End users view the data from the web pages on the browsers.

A web application also has several characteristics in common:

* The server interfaces with the database, _**not**_ clients.
* The database is hidden and holds _**valuable**_ assets.
* The user has\*\* _no direct control_\*\* of the data, only the server can. 😛

So blockchain promises the future of “**Users in charge of their data**”, what does a dApp look like exactly?

Simple. It looks like a web app, except we have one add-on: Blockchain.

<figure><img src="https://cdn-images-1.medium.com/max/3536/1*2AOjTQhr1lRlXs7JQiQ9YA.jpeg" alt=""><figcaption><p><em>DApp: Web + Blockchain</em></p></figcaption></figure>

#### What is a dApp? <a href="#what-is-dapp-2" id="what-is-dapp-2"></a>

_**dApp**_ is an application that is backed up by a distributed blockchain service. To make an analog to the web apps we use today, **d**_**App relies partially on blockchain data**_ but still is a web application (or web page).

* Client: Browser/IoT devices.
* Server: Serves code fragments or static assets like images.
* Blockchain: **Partial replacement** of database, stores/processes critical user data.

> A public blockchain is a openly readable, slow, expensive database running by a network consists of hundreds of nodes.

_**dApp**_ also has several characteristics in common:

* dApp interfaces with **both** blockchain and traditional server.
* The blockchain **cannot** be easily shut down as it contains multiple nodes.
* The user can **directly control** data on the blockchain via dApp.

Great, now you know what does a dApp do and where the data is coming from, let us focus on how to write one.

### Write a dApp: Sync and Connex <a href="#write-a-dapp-sync-and-connex" id="write-a-dapp-sync-and-connex"></a>

<figure><img src="https://cdn-images-1.medium.com/max/4256/1*rbq_5MkZBujA3qDGsvsvWw.png" alt=""><figcaption><p><em>Sync: Browser of VeChain apps.</em></p></figcaption></figure>

> _**dApp**_ shall both know how to communicate with traditional server backend as well as read/write from a blockchain network. **Connex.js** helps with the blockchain part, makes the developer life easier.

Vechain published **Connex.js** to substitute **Web3.js** in Ethereum. It is a huge step from Web3 and I am glad to use it in my first vechain project:

* [**Sync**](https://env.vechain.org/): Web browser of vechain apps.
* [**Connex.js**](https://www.npmjs.com/package/@vechain/connex): Standard Javascript library that helps to communicate with VeChain, _**included**_ in Sync.

### Token Transfer: A Simple dApp in Javascript <a href="#token-transfer-a-simple-dapp-in-javascript" id="token-transfer-a-simple-dapp-in-javascript"></a>

Starting from the next article, we will start to build a demo dApp named as “Token Transfer”. We will use an existing smart contract on vechain as the data source\*\*. **And I will help you to familiar with the environment** 😗

1. How to read data from a vechain blockchain smart contract.
2. How to display data to the user.
3. How to update data on blockchain via Javascript calls.

With the help of **Connex** in the **Sync** browser, we will do it in the blink of an eye! Follow the hands-on tutorials below to start coding! 😝

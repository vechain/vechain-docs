---
description: You are in the right place to start your journey with vechain DApps
---

# Getting started

## What is a DApp?

A DApp, or decentralized application, is a type of software application that operates on a decentralized network of computers, typically leveraging blockchain technology. Unlike traditional applications that are centralized and rely on a single server or a group of servers to function, DApps operate on a peer-to-peer network of computers, often using smart contracts on a blockchain.

## Prerequisites

Before you start developing your DApp, ensure you have the following prerequisites:

* Basic understanding of [blockchain](../core-concepts/blockchain-a-crash-course/) concepts
* Development experience with languages like Solidity (for smart contracts) and JavaScript (for front-end development)
* A [wallet](../core-concepts/wallets/) for testing purposes

## Steps

#### 1. Design your DApp

Outline the functionality, user interface, and features of your DApp.

#### 2. **Write Smart Contracts**

Develop smart contracts using Solidity that define the logic of your DApp.&#x20;

Our [Remix plugin ](sdks-and-providers/vechain-and-remix.md)and [Hardhat plugin ](sdks-and-providers/hardhat-and-vechain/)allow our vechain community to use Remix and Hardhat when developing and deploying smart contracts on vechain.

Use our [Built-in Contracts](built-in-contracts.md) to enhance your smart contract.

#### 3. **Front-End Development**

Create a user interface for your DApp using JavaScript, HTML, and CSS. &#x20;

Easily create a login button with vechain wallets using the [dappKit](sdks-and-providers/dapp-kit/) with a seamless DevEx, it will handle the login logic to connect with all vechain wallets.&#x20;

DappKit uses [Connex](sdks-and-providers/connex/) under the hood, Connex is the standard interface to connect DApps with the vechain blockchain. Our [Web3-Providers-Connex](sdks-and-providers/usage.md) library implements a provider on top of connex defined in [EIP-1193](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1193.md) compatible with [web3.js](https://github.com/ChainSafe/web3.js) and [ethers.js](https://github.com/ethers-io/ethers.js)

Use the [Thor DevKit](sdks-and-providers/thor-devkit/) which contains a lot of utils to work with transactions, certificates, cryptography, and much more.

Check our mainnet and testnet [node endpoints](nodes.md), a gateway to interacting with the VechainThor blockchain.

#### 4. **Testing**

Deploy and test your DApp on the [VeChainThor Solo Node](../core-concepts/networks/thor-solo-node.md) before going live. This ensures that everything functions as expected and allows for debugging if needed. [Here](tutorials/how-to-run-a-thor-solo-node/) you can find a tutorial to run a Solo Node.

Use [Devpal](sdks-and-providers/devpal.md), a set of tools to help your development and testing.

#### 5. **Submit the Dapp**

Let us know about your DApp!&#x20;

After you create the DApp, you can submit it in the [Vechain App Hub Repo](https://github.com/vechain/app-hub#vechain-app-hub---submit-form) to let it be visible in the [Vechain App Hub](https://apps.vechain.org/#all)

## Tutorials

you can also use our tutorials to get started:

* [How to run a Thor Solo Node](tutorials/how-to-run-a-thor-solo-node/)
* [How to connect the Sync2 wallet to a Thor Solo Node](tutorials/how-to-connect-the-sync2-wallet-to-a-thor-solo-node.md)
* [How to Develop a dApp on vechain](tutorials/how-to-develop-a-dapp-on-vechain/)
* [Build a dApp by using Connex](tutorials/useful-tips-for-building-a-dapp-by-using-connex.md)
* [Integrate VIP-191: Designated Gas Payer](tutorials/vip-191-designated-gas-payer/)
* [Integrate Account Abstraction](tutorials/account-abstraction/)

## Looking for no-code solution?

Take a look at [VORJ](vorj.md)

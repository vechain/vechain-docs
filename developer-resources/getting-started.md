---
description: You are in the right place to start your journey with vechain dApps
---

# Getting Started

## What is a dApp?

A dApp, or decentralized application, is a type of software application that operates on a decentralized network of computers, typically leveraging blockchain technology. Unlike traditional applications that are centralized and rely on a single server or a group of servers to function, dApps operate on a peer-to-peer network of computers, often using smart contracts on a blockchain.

## Prerequisites

Before you start developing your dApp, ensure you have the following prerequisites:

* Basic understanding of blockchain concepts
* Development experience with languages like Solidity (for smart contracts) and JavaScript (for front-end development)
* A [wallet](../core-concepts/wallets/) for testing purposes

## Steps

#### 1. Design your dApp

Outline the functionality, user interface, and features of your dApp.

#### 2. **Write Smart Contracts**

Develop smart contracts using Solidity that define the logic of your dApp.

Our [Remix plugin](frameworks-and-ides/vechain-and-remix/) and [Hardhat plugin](frameworks-and-ides/hardhat-and-vechain/) allow our vechain community to use Remix and Hardhat when developing and deploying smart contracts on vechain.

Use our [Built-in Contracts](built-in-contracts.md) to enhance your smart contract.

#### 3. **Front-End Development**

Create a user interface for your dApp using JavaScript, HTML, and CSS.

Easily create a login button with vechain wallets using the [dappKit](sdks-and-providers/dapp-kit/dapp-kit-1/) with a seamless DevEx, it will handle the login logic to connect with all vechain wallets.

Use the [SDK](./sdks-and-providers/sdk/README.md) to streamline blockchain development on the VeChainThor platform. The SDK offers a wealth of functionalities, including transaction management, certificate handling, cryptographic operations and  smart contract deployment. By utilizing the vechain SDK, developers can build sophisticated decentralized applications (dApps) with ease, leveraging its comprehensive suite of tools to create secure, scalable, and feature-rich solutions on the VeChainThor blockchain.

Check our mainnet and testnet [node endpoints](nodes.md), a gateway to interacting with the VechainThor blockchain.

#### 4. **Testing**

Deploy and test your dApp on the [VeChainThor Solo Node](../core-concepts/networks/thor-solo-node.md) before going live. This ensures that everything functions as expected and allows for debugging if needed. [Here](../core-concepts/networks/thor-solo-node.md) you can find a tutorial to run a Solo Node.

Use [Devpal](sdks-and-providers/devpal.md), a set of tools to help your development and testing.

#### 5. **Submit the Dapp**

Let us know about your dApp!

After you create the dApp, you can submit it in the [Vechain App Hub Repo](https://github.com/vechain/app-hub#vechain-app-hub---submit-form) to let it be visible in the [Vechain App Hub](https://apps.vechain.org/#all)

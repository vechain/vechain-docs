---
description: Your gateway to developing VeChain dApps
---

# Getting Started

## What is a dApp?

A dApp (decentralized application) is a software application that operates on a distributed network, typically using blockchain technology. Unlike traditional centralized applications, dApps run on a peer-to-peer network of computers, often utilizing smart contracts on a blockchain for enhanced security and transparency.

## Prerequisites

Before diving into dApp development, ensure you have:

* A solid understanding of blockchain fundamentals.
* Experience with Solidity (for smart contracts) and JavaScript (for front-end development).
* A VeChain-compatible [wallet](../core-concepts/wallets/) for testing.

## Quick Start with VeChain Templates

Jump-start your development with our pre-built templates:

```bash
npm create vechain-dapp
```

or

```bash
yarn create vechain-dapp
```

or

<pre class="language-bash"><code class="lang-bash"><strong>npx create-vechain-dapp@latest
</strong></code></pre>

## Development Roadmap

#### 1. Design your dApp

Outline your dApp's functionality, user interface, and key features.

#### 2. **Develop Smart Contracts**

Create Solidity smart contracts to define your dApp's core logic.

* Utilize our [Remix plugin](frameworks-and-ides/remix.md) or [Hardhat plugin](frameworks-and-ides/hardhat/) for a seamless development experience.
* Leverage [Built-in Contracts](built-in-contracts.md) to enhance functionality.

#### 3. **Build the Front-End**

Craft an intuitive user interface using modern web technologies.

* Implement easy wallet login with [dappKit](sdks-and-providers/dapp-kit/dapp-kit-1/).
* Use our comprehensive [SDK](sdks-and-providers/sdk/) for efficient blockchain interactions.
* Connect to VeChainThor via our [node endpoints](https://docs.vechain.org/core-concepts/nodes).

#### 4. **Test Thoroughly**

* Deploy and test on the [VeChainThor Solo Node](../core-concepts/networks/thor-solo-node.md) before going live.
* Utilize [Devpal](sdks-and-providers/devpal.md)for streamlined development and testing.

#### 5. **Launch Your dApp**

Submit your dApp to the [VeChain App Hub](https://apps.vechain.org/#all) for increased visibility.

By following this guide, you'll be well-equipped to create robust, scalable dApps on the VeChainThor blockchain. Happy coding!

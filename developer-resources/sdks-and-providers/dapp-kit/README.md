# DApp Kit

The VeChain dApp kit is a frontend library designed to make it easy to build dApps on the VeChainThor blockchain. This documentation provides a comprehensive guide to using the dApp kit library, including installation, usage instructions, and details about its key features and methods.

## Repo

[https://github.com/vechain/vechain-dapp-kit](https://github.com/vechain/vechain-dapp-kit)

## Libraries

* `@vechain/dapp-kit` - A library to provide a layer on top of Connex, which makes wallet management easier.
* `@vechain/dapp-kit-ui` - A library of UI components to make it easy to select and connect to a wallet.
* `@vechain/dapp-kit-react` - A library of React hooks and components to make it easy to use the dApp kit with React.

## React and other Frameworks

{% hint style="warning" %}
Please note that server-side rendering (SSR) must be disabled when using the dApp kit libraries.
{% endhint %}

**React** is our favourite library but the dApp kit library has been made to be used with every JavaScript framework.\
You can **start** with these **sample apps**:

* [React](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-react-app)
* [Next.js](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-next-app)
* [Remix.run](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-remix-app)
* [Vanilla JS](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-vanilla-app)
* [Vue](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-vue-app)
* [Angular](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-angular-app)
* [Svelte](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-svelte-app)

you can use both JavaScript and TypeScript

## Key Features

The VeChain dApp kit is designed to make it easy to interact with all VeChainThor compatible wallets

1. **Wallet Management**: Connex was designed with Sync / Sync2 in mind, so this library provides an additional layer on top, making it easier to manage multiple wallets.
2. **Wallet Selection**: The `@vechain/dapp-kit-ui` library provides multiple components to make it easy to select and connect to a wallet.
3. **React**: The `@vechain-dapp-kit-react` library provides several hooks and components to make it easy to use the dApp kit with React.

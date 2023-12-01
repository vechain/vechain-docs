# DApp Kit

The vechain dApp kit is a frontend library designed to make it easy to build dApps on the VechainThor blockchain. This documentation provides a comprehensive guide to using the dApp kit library, including installation, usage instructions, and details about its key features and methods.

## Libraries

* `@vechain/dapp-kit` - A library to provide a layer on top of Connex, which makes wallet management easier.
* `@vechain/dapp-kit-ui` - A library of UI components to make it easy to select and connect to a wallet.
* `@vechain/dapp-kit-react` - A library of React hooks and components to make it easy to use the dApp kit with React.

## Languages & Frameworks

{% hint style="info" %}
Please note that server-side rendering (SSR) must be disabled when using the dApp kit libraries.
{% endhint %}

The dApp kit library is available in the following languages & frameworks:

* TypeScript
* Vanilla JS
* React
* Vue
* Angular
* Svelte
* Next.js

{% hint style="info" %}
For an example of how to use the dApp kit libraries please refer to these [examples](https://github.com/vechainfoundation/vechain-dapp-kit/tree/main/apps)
{% endhint %}

## Key Features

The vechain dApp kit is designed to make it easy to interact with all vechain thor compatible wallets

1. **Wallet Management**: Connex was designed with Sync / Sync2 in mind, so this library provides an additional layer on top, making it easier to manage multiple wallets.
2. **Wallet Selection**: The `@vechain/dapp-kit-ui` library provides multiple components to make it easy to select and connect to a wallet.
3. **React**: The `@vechain-dapp-kit-react` library provides several hooks and components to make it easy to use the dApp kit with React.
4.

***

## Adding your Wallet

Since the DApp Kit is designed to work with 1 to many wallets, you can create a pull request and configure your wallet in the DApp Kit.

1. Clone the repo \[here]\([https://github.com/vechainfoundation/vechain-dapp-kit](https://github.com/vechainfoundation/vechain-dapp-kit))
2. Inside `./packages/dapp-kit`&#x20;
   1. Modify `WalletSource` in `src/types.d.ts`
   2. Modify the `createWallet` function in `src/create-wallet.ts`
3. Add your wallet details in: `./packages/dapp-kit-ui/src/constants/sources.ts`
4. Test you that can successfully integrate with your wallet
5. Add unit tests
6. Create your pull request

# Installation

check the [example app](https://github.com/vechain/vechain-dapp-kit/tree/main/examples/sample-react-app) for a quick start

## Installation

{% hint style="warning" %}
dApp-kit has been built on top of Connex, which will require crypto, buffer, http, https and some other node polyfills, check [example app](https://github.com/vechain/vechain-dapp-kit/tree/main/examples) configuration files if you are stuck. Check also [Node Polyfills page](https://app.gitbook.com/s/HKk8xWsgscVhGUM2fb7S/developer-resources/sdks-and-providers/dapp-kit/dapp-kit-1/node-polyfills).
{% endhint %}

```bash
npm i @vechain/dapp-kit-react
```

Upon installation, you may utilize the subsequent code snippet to verify the proper functioning within your TypeScript project:

```typescript
import { DAppKitProvider } from '@vechain/dapp-kit-react';
```

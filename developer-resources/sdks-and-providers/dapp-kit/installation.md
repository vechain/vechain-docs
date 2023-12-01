---
description: How to install dApp kit in order to use it with TypeScript or Javascript.
---

# Installation

If using TypeScript follow the NPM installation steps, for JavaScript follow the CommonJS (CJS) installation steps.

{% hint style="info" %}
Should you wish to implement this in a pure JavaScript project, it is recommended to use CommonJS (CJS) imports. Potential complications might arise with ES Module (ESM) imports.
{% endhint %}

## NPM

```bash
npm i @vechain/dapp-kit
```

Upon installation, you may utilize the subsequent code snippet to verify the proper functioning within your TypeScript project:

```typescript
const connex = new MultiWalletConnex({
  //Required
  nodeUrl: 'https://sync-testnet.vechain.org/', 
  // Required if not connecting to the mainnet
  genesis: 'test', 
});
```

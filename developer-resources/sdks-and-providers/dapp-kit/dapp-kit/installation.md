---
description: >-
  How to install `@vechain/dapp-kit` in order to use it with TypeScript or
  Javascript.
---

# Installation

If using TypeScript follow the installation steps, for JavaScript follow the CommonJS (CJS) installation steps.

{% hint style="info" %}
Should you wish to implement this in a pure JavaScript project, it is recommended to use CommonJS (CJS) imports. Potential complications might arise with ES Module (ESM) imports.
{% endhint %}

## NPM

{% tabs %}
{% tab title="npm" %}
```
npm i @vechain/dapp-kit
```
{% endtab %}

{% tab title="yarn" %}
```
yarn add @vechain/dapp-kit
```
{% endtab %}

{% tab title="pnpm" %}
```
pnpm i @vechain/dapp-kit
```
{% endtab %}
{% endtabs %}

Upon installation, you may utilize the subsequent code snippet to verify the proper functioning within your TypeScript project:

```typescript
import { DAppKit } from "@vechain/dapp-kit"

const dappKit = new DAppKit({
  //Required
  nodeUrl: 'https://sync-testnet.vechain.org/', 
  // Required if not connecting to the mainnet
  genesis: 'test', 
});
```

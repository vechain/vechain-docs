---
description: Using the vechain dApp kit in react
---

## Initialization

#### 1. Create the node options

```typescript jsx
import type { Options } from '@vechain/connex';

const nodeOptions: Omit<Options, 'signer'> = {
    node: 'https://testnet.vechain.org/', //Required
    network: 'test', // Required if connecting to a network other than mainnet
};
```

#### 2. Optional: Wallet Connect Options

```typescript
import type { WalletConnectOptions } from '@vechainfoundation/dapp-kit';

const walletConnectOptions: WalletConnectOptions = {
    projectId: '<PROJECT_ID>', // Create your project here: https://cloud.walletconnect.com/sign-up
    metadata: {
        name: 'My dApp',
        description: 'My dApp description',
        url: window.location.origin, // Your app URL
        icons: [`${window.location.origin}/images/my-dapp-icon.png`], // Your app Icon
    },
};
```


#### 3. Initialise the `Connex` instance

{% hint style="info" %}
For more information on using connex, please refer to the [Connex documentation](../../connex/api-specification.md).
{% endhint %}

```typescript jsx
import { MultiWalletConnex } from '@vechainfoundation/dapp-kit';

const {thor, vendor, wallet} = new MultiWalletConnex({
  nodeUrl: "https://sync-testnet.vechain.org/", // Required - The URL of the node to connect to
  genesis: "test", // Optional - "main" | "test" | Connex.Thor.Block
  walletConnectOptions: walletConnectOptions, // Optional - Wallet connect options
  customWcModal: undefined, // Optional - A custmod modal for displaying wallet connect QR codes
  usePersistence: true, // Optional - Defaults to false. If true, account and source will be persisted in local storage
});
```

#### 4. Set the wallet to connect use

```typescript
import type { WalletSource } from '@vechainfoundation/dapp-kit';

const mySource: WalletSource = 'veworld';

wallet.setSource('veworld');
```

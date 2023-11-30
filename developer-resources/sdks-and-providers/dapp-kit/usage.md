---
description: Using the vechain dApp kit
---

# Usage

### 1. Optional: Wallet Connect Options

```typescript
import type { WalletConnectOptions } from '@vechainfoundation/dapp-kit';

const walletConnectOptions: WalletConnectOptions = {
    // Create your project here: https://cloud.walletconnect.com/sign-up
    projectId: '<PROJECT_ID>', 
    metadata: {
        name: 'My dApp',
        description: 'My dApp description',
        // Your app URL
        url: window.location.origin, 
        // Your app Icon
        icons: [`${window.location.origin}/images/my-dapp-icon.png`], 
    },
};
```

### 2. Initialise the `Connex` instance

{% hint style="info" %}
For more information on using connex, please refer to the [Connex documentation](../../connex/api-specification.md).
{% endhint %}

```typescript
import { DAppKit } from '@vechainfoundation/dapp-kit';

const {thor, vendor, wallet} = new DAppKit({
  // Required - The URL of the node to connect to
  nodeUrl: "https://sync-testnet.vechain.org/", 
  // Optional - "main" | "test" | Connex.Thor.Block
  genesis: "test", 
  // Optional - Wallet connect options
  walletConnectOptions: walletConnectOptions, 
  // Optional - Defaults to false. If true, account and source will be persisted in local storage
  usePersistence: true, 
  // Optional - Use the first available wallet
  useFirstDetectedSource: false,
  // Optional - Log Level - To debug the library
  logLevel: "DEBUG",
});
```



***

### Setting the Walet

* If you provided `useFirstDetectedSource` as true, then you don't need to do anything. You can start using the `thor` and `vendor` instances.
* Otherwise, you will have to set the wallet source. This is usually chosen by the user, but it can be done manually too:

```typescript
import type { WalletSource } from '@vechainfoundation/dapp-kit';

// type WalletSource = 'wallet-connect' | 'veworld' | 'sync2' | 'sync';
const mySource: WalletSource = 'veworld';

wallet.setSource('veworld');
```

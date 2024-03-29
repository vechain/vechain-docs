---
description: Using the vechain dApp kit
---

# Usage

### 1. Optional: Wallet Connect Options

```typescript
import type { WalletConnectOptions } from '@vechain/dapp-kit';

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

### 2. Initialise the `DAppKit` instance

{% hint style="info" %}
For more information on using connex, please refer to the [Connex documentation](../../../connex/).
{% endhint %}

```typescript
import { DAppKit } from '@vechain/dapp-kit';

const {thor, vendor, wallet} = new DAppKit({
  // Required - The URL of the node to connect to
  nodeUrl: "https://sync-testnet.vechain.org/", 
  // OPTIONAL: "main" | "test" | Connex.Thor.Block
  genesis: "test", 
  // OPTIONAL: Wallet connect options
  walletConnectOptions: walletConnectOptions, 
  // OPTIONAL: Defaults to false. If true, account and source will be persisted in local storage
  usePersistence: true, 
  // OPTIONAL: Use the first available wallet
  useFirstDetectedSource: false,
  // OPTIONAL: Log Level - To debug the library
  logLevel: "DEBUG",
  // OPTIONAL: every wallet has a connection certificate, but wallet connect doesn't connect with a certificate, it uses a session; if required, with this option, we will force the user to sign a certificate after he finishes the connection with wallet connect
  requireCertificate=false;
});
```

***

## Wallet Manager

The wallet manager is the layer provided on top of `connex` . It can be created following the usage above.

```typescript
const {wallet, thor, connex} = new DAppKit(...)
```

***

### Set the wallet source

* Set the current wallet source. This step is necessary if `useFirstDetectedSource` was not provided as true.

```typescript
import type { WalletSource } from '@vechain/dapp-kit';

// type WalletSource = 'wallet-connect' | 'veworld' | 'sync2' | 'sync';
const mySource: WalletSource = 'veworld';

wallet.setSource('veworld');
```

***

### Connect

* Connect to the selected wallet. The purpose of this is to improve the UX. For example, connecting a wallet via Wallet Connect involves switching applications multiple times. This will reduce the friction and create a better experience for the user.
* This will connect to the user's wallet and return its address.
  * For certificate-based wallets, (eg. Sync2), this involves signing a signature
  * For other wallets, such as those using Wallet Connect, it will fetch the address without signing a certificate
* The response will contain `verified` equal to true if the user signed a certificate

```typescript
import { ConnectResponse } from '@vechain/dapp-kit'

const res: ConnectResponse = await wallet.connect()

console.log(res)
// { "address": "0x995711ADca070C8f6cC9ca98A5B9C5A99b8350b1","verified": true}
```

***

### State

* The wallet manager will have some fields in state for ease of use.
  * `address` will be whatever address was retrieved when connecting, signing a certificate, or sending a transaction.

```typescript
import { WalletManagerState } from '@vechain/dapp-kit'

const state: WalletManagerState = wallet.state
```

#### WalletManagerState:

* `account` - the address of the connected wallet. Null if not connected
* `source` - the source of the currently selected wallet. Null if not selected
* `connectionCertificate` - certificate signed during connection
* `availableWallets` - A list of available wallet sources

***

### Subscribe to State

* You can subscribe to state changes:

```typescript
import { WalletManagerState } from '@vechain/dapp-kit'

const myListener = (newState: WalletManagerState) => {
    console.log(newState)
}

//Start the subscription
const subscription = wallet.subscribe(myListener)

//End the subscription
subscription()

```

***

### Subscribe to a single value in the state

* You can also subscribe to a single value in the state:

```typescript
import { WalletSource } from '@vechain/dapp-kit'

const myListener = (newWalletSource: WalletSource) => {
    console.log(newWalletSource)
}

//Start the subscription
const subscription = wallet.subscribeToKey('source', myListener)

//End the subscription
subscription()
```

---
description: Using the vechain dApp kit in react
---

# Usage

***

### Initialization

**1. Create the node options**

```typescript
import type { Options } from '@vechain/connex';

const nodeOptions: Omit<Options, 'signer'> = {
    node: 'https://testnet.vechain.org/', //Required
    network: 'test', // Required if connecting to a network other than mainnet
};
```

**2. Optional: Wallet Connect Options**

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

**3. Initialise the `ConnexVendor`**

{% code overflow="wrap" %}
```typescript
import { ConnexProvider } from '@vechainfoundation/dapp-kit-react';

export const App = (): JSX.Element => {
    return (
        <>
            <ConnexProvider
                nodeOptions={nodeOptions}
                // Optional - defaults to false. If true, account and source will be persisted in local storage
                persistState={false} 
                walletConnectOptions={walletConnectOptions}
            >
                <YourApp />
            </ConnexProvider>
        </>
    );
};
```
{% endcode %}

***

### Hooks

#### `useWallet`

```typescript
import { useWallet } from '@vechainfoundation/dapp-kit-react';

const {
    // The current connected account
    account, 
    // The current wallet source
    source, 
    // Set the wallet source
    setSource, 
    // Connect to the wallet
    connect, 
    // A list of available wallets
    availableWallets, 
    // Disconnect from the wallet
    disconnect, 
} = useWallet();
```

#### `useConnex`

* This hook exposes the `thor` and `vendor` instances of `@vechain/connex`. To interact with a wallet, you must `useWallet` and call `setSource` first.

{% hint style="info" %}
For more information on using connex, please refer to the [Connex documentation](../../connex/api-specification.md).
{% endhint %}

```typescript
import { useConnex } from '@vechainfoundation/dapp-kit-react';

const { thor, vendor } = useConnex();
```

#### `useModal`

* This hook can be used to open and close the wallet modal.
* The modal will display the available wallets and allow the user to connect to one of them.

```typescript
import { useWalletModal } from '@vechainfoundation/dapp-kit-react';

const { open, close } = useWalletModal();
```



***

### UI Components

#### `ConnectWalletButton`

* This component mounts a button inside your component that will open a modal with the available wallets when clicked.
* The user can then select a wallet of their choice and connect to it.
* Once connected,  `account` and `source` will be available via the `useWallet` hook.

```typescript
import { ConnectWalletButtonWithModal } from '@vechainfoundation/dapp-kit-react';

const MyComponent = (): JSX.Element => {

  const { account, source } = useWallet();

  useEffect(() => {
    console.log(account, source);
  }, [account, source]);

  return (
    <>
      <ConnectWalletButtonWithModal/>
    </>
  );
};
```

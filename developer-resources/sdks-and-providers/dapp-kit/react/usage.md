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


#### 3. Initialise the `ConnexVendor`

```typescript jsx
import { ConnexProvider } from '@vechainfoundation/dapp-kit-react';

export const App = (): JSX.Element => {
    return (
        <>
            <ConnexProvider
                nodeOptions={nodeOptions}
                persistState={false} // Optional - defaults to false. If true, account and source will be persisted in local storage
                walletConnectOptions={walletConnectOptions}
            >
                <YourApp />
            </ConnexProvider>
        </>
    );
};
```


## Hooks

### `useWallet`

```typescript jsx
import { useWallet } from '@vechainfoundation/dapp-kit-react';

const {
    account, // The current connected account
    source, // The current wallet source
    setSource, // Set the wallet source
    connect, // Connect to the wallet
    availableWallets, // A list of available wallets
    disconnect, // Disconnect from the wallet
} = useWallet();
```

### `useConnex`

- This hook exposes the `thor` and `vendor` instances of `@vechain/connex`. To interact with a wallet, you must `useWallet` and call `setSource` first.

{% hint style="info" %}
For more information on using connex, please refer to the [Connex documentation](../../connex/api-specification.md).
{% endhint %}

```typescript jsx
import { useConnex } from '@vechainfoundation/dapp-kit-react';

const { thor, vendor } = useConnex();
```

### `useModal`

- This hook can be used to open and close the wallet modal.
- The modal will display the available wallets and allow the user to connect to one of them.

```typescript jsx
import { useWalletModal } from '@vechainfoundation/dapp-kit-react';

const { open, close } = useWalletModal();
```

## UI Components

### `ConnectWalletButton`

- This component mounts a button inside your component that will open a modal with the available wallets when clicked.
- The user can then select a wallet of their choice and connect to it.
- Once connected, the `account` and `source` will be available via the `useWallet` hook.

```typescript jsx
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

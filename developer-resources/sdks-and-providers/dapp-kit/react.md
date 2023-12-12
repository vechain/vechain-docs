---
description: DApp kit for React apps
---

# React

## Installation

```typescript
import { DAppKitProvider } from '@vechain/dapp-kit-react';
```

Upon installation, you may utilize the subsequent code snippet to verify the proper functioning within your TypeScript project:

```bash
npm i @vechain/dapp-kit-react
```

{% hint style="info" %}
Should you wish to implement this in a pure JavaScript project, it is recommended to use CommonJS (CJS) imports. Potential complications might arise with ES Module (ESM) imports.
{% endhint %}

If using TypeScript follow the NPM installation steps, for JavaScript follow the CommonJS (CJS) installation steps.

## Usage

**1. Optional: Wallet Connect Options**

```tsx
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

**2. Initialise the**`DAppKitProvider`

{% code overflow="wrap" %}
```tsx
import { DAppKitProvider } from '@vechain/dapp-kit-react';

ReactDOM.createRoot(document.getElementById('root')!).render(
    <React.StrictMode>
        <DAppKitProvider
            // REQUIRED: The URL of the node you want to connect to
            nodeUrl={'https://testnet.vechain.org/'}
            // OPTIONAL: Required if you're not connecting to the main net
            genesis={'test'}
            // OPTIONAL: Whether or not to persist state in local storage (account, wallet source)
            usePersistence={true}
            // OPTIONAL: Options to enable wallet connect
            walletConnectOptions={walletConnectOptions}
            // OPTIONAL: A log level for console logs
            logLevel="DEBUG"
        >
            <App />
        </DAppKitProvider>
    </React.StrictMode>,
);
```
{% endcode %}

***

### Hooks

#### `useWallet`

```tsx
import { useWallet } from '@vechain/dapp-kit-react';
  
const MyComponent: React.FC = () => {

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
  
  return <div>...</div>;
}
```

#### `useConnex`

* This hook exposes the `thor` and `vendor` instances of `@vechain/connex`. To interact with a wallet, you must `useWallet` and call `setSource` first.

{% hint style="info" %}
For more information on using connex, please refer to the [Connex documentation](../connex/api-specification.md).
{% endhint %}

```typescript
import { useConnex } from '@vechain/dapp-kit-react';

const MyComponent: React.FC = () => {

  const { thor, vendor } = useConnex();
  
  return <div>...</div>;
}

const { thor, vendor } = useConnex();
```

#### `useModal`

* This hook can be used to open and close the wallet modal.
* The modal will display the available wallets and allow the user to connect to one of them.
* Once the user has connected, the modal will close itself

```typescript
import { useWalletModal, useWallet } from '@vechain/dapp-kit-react';

const MyComponent = () => {
    const { open, close } = useWalletModal();
    const { account } = useWallet();

    useEffect(() => {
        if (account) {
            console.log(`Account connected: ${account}`);
        }
    }, [account]);

    return <button onClick={open}>Open Modal</button>;
};

```

***

### UI Components

#### `ConnectWalletButton`

* This component mounts a button that will open a modal with the available wallets when clicked.
* The user can then select a wallet of their choice and connect to it.
* Once connected, `account` and `source` will be available via the `useWallet` hook.

```typescript
import { ConnectButtonWithModal } from '@vechain/dapp-kit-react';

const MyComponent = (): JSX.Element => {

  const { account, source } = useWallet();

  useEffect(() => {
    console.log(account, source);
  }, [account, source]);

  return (
    <>
      <ConnectButtonWithModal/>
    </>
  );
};
```

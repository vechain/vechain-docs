# Usage

### Initialization

**1. Optional: Wallet Connect Options**

```tsx
import type { WalletConnectOptions } from '@vechain/dapp-kit-react';

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

<pre class="language-tsx" data-overflow="wrap"><code class="lang-tsx">import { DAppKitProvider } from '@vechain/dapp-kit-react';

 return (
      &#x3C;DAppKitProvider
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
            // OPTIONAL: theme mode 'LIGHT' or 'DARK'
            themeMode='LIGHT'
            // OPTIONAL: theme variables (check theme variables section)
            themeVariables={ThemeVariables}
            // OPTIONAL: app current language
            language="en"
            // OPTIONAL: i18n default object (check i18n section)
            i18n={defaultI18n}
            // OPTIONAL: where to render the modal, document.body is the default
            modalParent={document.body}
            // OPTIONAL: handle source click to customise wallet connect
            onSourceClick={source => void}
            // OPTIONAL: every wallet has a connection certificate, but wallet connect doesn't connect with a certificate, it uses a session; if required, with this option, we will force the user to sign a certificate after he finishes the connection with wallet connect
            requireCertificate=false
            // OPTIONAL: certificate to be signed during the login, otherwise a standard one will be used
            connectionCertificate={defaultContract}
            //OPTIONAL: you can choose witch wallet to be allowed between 'wallet-connect', 'veworld', 'sync2' or 'sync'. default: all
<strong>            allowedWallets={[ 'veworld', 'wallet-connect' ]}
</strong>        >
        &#x3C;App />
    &#x3C;/DAppKitProvider>
);
</code></pre>

***

### UI Components

#### `WalletButton`

* This component mounts a button that will open a modal with the available wallets when clicked.
* The user can then select a wallet of their choice and connect to it.
* Once connected, `account` and `source` will be available via the `useWallet` hook.

```typescript
import { WalletButton } from '@vechain/dapp-kit-react';

const MyComponent = (): JSX.Element => {

  const { account, source } = useWallet();

  useEffect(() => {
    console.log(account, source);
  }, [account, source]);

  return (
    <>
      <WalletButton/>
    </>
  );
};
```

***

### Hooks

#### `useWallet`

```tsx
import { useWallet } from '@vechain/dapp-kit-react';
  
const MyComponent: React.FC = () => {

  const {
    // The current connected account
    account,
    // The account vechain domain if present
    accountDomain,
    // Whether the account domain is loading
    isAccountDomainLoading,
    // The current wallet source
    source,
    // certificate created during connection 
    connectionCertificate,
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
For more information on using connex, please refer to the [Connex documentation](../../../connex/api-specification.md).
{% endhint %}

```typescript
import { useConnex } from '@vechain/dapp-kit-react';

const MyComponent: React.FC = () => {

  const { thor, vendor } = useConnex();
  
  return <div>...</div>;
}

const { thor, vendor } = useConnex();
```

#### `useWalletModal`

* This hook can be used to open and close the wallet modal.
* The modal will display the available wallets and allow the user to connect to one of them.
* Once the user has connected, the modal will close itself and it will call the onConnected function2

```typescript
import { useWalletModal, useWallet } from '@vechain/dapp-kit-react';

const MyComponent = () => {
    const { open, close, onConnected } = useWalletModal();
    const { account } = useWallet();

    useEffect(() => {
        if (account) {
            console.log(`Account connected: ${account}`);
        }
    }, [account]);

    return <button onClick={open}>Open Modal</button>;
};
```

#### useVechianDomain

This hook can fetch a vechain domain from an address and an address from a vechian domain.

```typescript
import { useVechainDomain } from '@vechain/dapp-kit-react';

// usage:

// with an address
const {
    domain,
    isLoading
} = useVechainDomain({ domainOrAddress: '0xasdfasdfa' })

// or with a domain
const {
    address,
    isLoading
} = useVechainDomain({ domainOrAddress: 'cleanify.vet' })
```

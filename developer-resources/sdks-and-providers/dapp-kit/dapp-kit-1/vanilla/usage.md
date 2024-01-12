---
description: Using the vechain dApp kit UI components
---

# Usage

### Initialization

```typescript
import { DAppKitUI } from '@vechain/dapp-kit-ui';
import type { WalletConnectOptions } from '@vechain/dapp-kit';
import type { DAppKitOptions } from '@vechain/dapp-kit-ui';

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

const vechainWalletKitOptions: DAppKitOptions = {
    // Required - The URL of the node to connect to
    node: 'https://testnet.vechain.org/', 
    // Optional - "main" | "test" | Connex.Thor.Block
    network: 'test', 
    // Optional - Wallet connect options
    walletConnectOptions, 
    // Optional - Defaults to false. If true, the account and source will be persisted in local storage
    usePersistence: true, 
    // Optional - Defaults to the first available wallet. Default value is false
    useFirstDetectedSource: true,
    // Optional - Set a log level to debug the library
    logLevel: 'DEBUG',
    // OPTIONAL: theme variables (check theme variables section)
    themeVariables={ThemeVariables}
    // OPTIONAL: app current language
    language="en";
    // OPTIONAL: i18n default object (check i18n section)
    i18n={defaultI18n}
    // OPTIONAL: where to render the modal, document.body is the default
    modalParent={document.body}
    // OPTIONAL: handle source click to customise wallet connect
    onSourceClick={source => void}
    // OPTIONAL: every wallet has a connection certificate, but wallet connect doesn't connect with a certificate, it uses a session; if required, with this option, we will force the user to sign a certificate after he finishes the connection with wallet connect
    requireCertificate=false;
};

const dappKit = DAppKitUI.configure(vechainWalletKitOptions);

console.log(`DAppKit configured`, dappKit.thor.genesis.id);
```

### Place the custom element in your HTML

```html
<body>
    <vwk-button></vwk-button>
</body>
```

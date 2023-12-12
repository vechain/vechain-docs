# Vanilla (UI)

## Installation

If using TypeScript follow the NPM installation steps, for JavaScript follow the CommonJS (CJS) installation steps.

{% hint style="info" %}
Should you wish to implement this in a pure JavaScript project, it is recommended to use CommonJS (CJS) imports. Potential complications might arise with ES Module (ESM) imports.
{% endhint %}

## NPM

```bash
npm i @vechain/dapp-kit-ui
```

Upon installation, you may utilize the subsequent code snippet to verify the proper functioning within your TypeScript project:

```typescript
import { DAppKitUI } from '@vechain/dapp-kit-ui';
```

## Usage

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
    logLevel: 'DEBUG'
};

const dappKit = DAppKitUI.configure(vechainWalletKitOptions);

console.log(`DAppKit configured`, dappKit.thor.genesis.id);
```

### Place the custom element in your HTML

```html
<body>
    <vwk-vechain-dapp-connect-kit mode="DARK"></vwk-vechain-dapp-connect-kit>
</body>
```

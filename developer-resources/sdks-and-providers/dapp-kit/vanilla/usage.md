---
description: Using the vechain dApp kit UI components
---

# Usage

#### Initialization

```typescript
import { DAppKit } from '@vechainfoundation/dapp-kit-ui';
import type { WalletConnectOptions } from '@vechainfoundation/dapp-kit';
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
    // Optional - If false/undefined, the default Wallet Connect model will be used
    useWalletKitModal: true, 
    // Optional - Defaults to false. If true, the account and source will be persisted in local storage
    usePersistence: true, 
};

const connex = DAppKit.configure(vechainWalletKitOptions);

console.log(`Connex configured`, connex.thor.genesis.id);
```

#### Place the custom element in your HTML

```html
<body>
    <vwk-vechain-dapp-connect-kit mode="DARK"></vwk-vechain-dapp-connect-kit>
</body>
```

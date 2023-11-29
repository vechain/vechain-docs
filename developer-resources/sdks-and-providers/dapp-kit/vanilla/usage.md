---
description: Using the vechain dApp kit UI components
---

### Initialization

```typescript
import { DAppKit } from '@vechainfoundation/dapp-kit-ui';
import type { WalletConnectOptions } from '@vechainfoundation/dapp-kit';
import type { DAppKitOptions } from '@vechain/dapp-kit-ui';

const walletConnectOptions: WalletConnectOptions = {
    projectId: '<PROJECT_ID>', // Create your project here: https://cloud.walletconnect.com/sign-up
    metadata: {
        name: 'My dApp',
        description: 'My dApp description',
        url: window.location.origin, // Your app URL
        icons: [`${window.location.origin}/images/my-dapp-icon.png`], // Your app Icon
    },
};

const vechainWalletKitOptions: DAppKitOptions = {
    node: 'https://testnet.vechain.org/', // Required - The URL of the node to connect to
    network: 'test', // Optional - "main" | "test" | Connex.Thor.Block
    walletConnectOptions, // Optional - Wallet connect options
    useWalletKitModal: true, // Optional - If false/undefined, the default Wallet Connect model will be used
    usePersistence: true, // Optional - Defaults to false. If true, account and source will be persisted in local storage
};

const connex = DAppKit.configure(vechainWalletKitOptions);

console.log(`Connex configured`, connex.thor.genesis.id);
```


### Place the custom element in your HTML

```html
<body>
    <vwk-vechain-dapp-connect-kit mode="DARK"></vwk-vechain-dapp-connect-kit>
</body>
```

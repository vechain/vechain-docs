# Network Configuration

## Overview

The `@vechain/react-native-wallet-link` library allows you to connect your dApp to **any VeChain network** — including **Mainnet**, **Testnet**, or a **custom node** (e.g., for local development or staging).  
The network node is passed as the `node` prop in the `VeWorldProvider` component.

---

## Supported Networks

You can import VeChain’s default node URLs directly from `@vechain/sdk-network`:

```ts
import { MAINNET_URL, TESTNET_URL } from '@vechain/sdk-network';
```

### 🟢 Mainnet

Use when deploying your app to production.

```tsx
<VeWorldProvider
  appName="My VeChain App"
  appUrl="https://myvechainapp.com"
  redirectUrl={Linking.createURL('/', { scheme: 'myvechainapp' })}
  node={MAINNET_URL}
  config={/* event handlers */}
>
  {/* App */}
</VeWorldProvider>
```

- **Purpose:** Real VeChain transactions  
- **Network ID:** 1  
- **Explorer:** https://explore.vechain.org

---

### 🧪 Testnet

Use during development and testing.

```tsx
<VeWorldProvider
  appName="My Test App"
  appUrl="https://mytestapp.com"
  redirectUrl={Linking.createURL('/', { scheme: 'mytestapp' })}
  node={TESTNET_URL}
  config={/* event handlers */}
>
  {/* App */}
</VeWorldProvider>
```

- **Purpose:** Safe test environment with free tokens  
- **Network ID:** 100009  
- **Explorer:** https://explore-testnet.vechain.org

---

### ⚙️ Custom Node

You can also connect to your own VeChain Thor node or a private network.

```tsx
<VeWorldProvider
  appName="Custom Node App"
  appUrl="https://customapp.com"
  redirectUrl={Linking.createURL('/', { scheme: 'customapp' })}
  node="https://my-custom-vechain-node.com"
  config={/* event handlers */}
>
  {/* App */}
</VeWorldProvider>
```

> 💡 Tip: Always ensure your custom node supports HTTPS and CORS for mobile app communication.

---

## Environment Management

You can dynamically switch networks at runtime based on environment variables.

Example using `react-native-dotenv`:

```tsx
import { MAINNET_URL, TESTNET_URL } from '@vechain/sdk-network';
import { VeWorldProvider } from '@vechain/react-native-wallet-link';

const NODE_URL = process.env.NODE_ENV === 'production' ? MAINNET_URL : TESTNET_URL;

<VeWorldProvider
  appName="Dynamic Network App"
  appUrl="https://dynamicapp.com"
  redirectUrl={Linking.createURL('/', { scheme: 'dynamicapp' })}
  node={NODE_URL}
  config={/* event handlers */}
>
  {/* App */}
</VeWorldProvider>
```

This ensures that your test builds use Testnet and production builds automatically connect to Mainnet.

---

[← Back: Error Handling](./06-error-handling.md)
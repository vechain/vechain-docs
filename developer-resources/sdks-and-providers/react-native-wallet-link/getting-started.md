# Getting Started

## Installation

Install the SDK from npm or yarn:

```bash
npm install @vechain/react-native-wallet-link
```

or

```bash
yarn add @vechain/react-native-wallet-link
```

### Peer Dependencies

Make sure to also install VeChain’s SDK dependencies:

```bash
npm install @vechain/sdk-core @vechain/sdk-network
```

or

```bash
yarn add @vechain/sdk-core @vechain/sdk-network
```

---

## Environment Requirements

- React Native ≥ **0.71**  
- Node.js ≥ **16**  
- VeWorld mobile app installed on the user’s device  
- Expo (optional but supported)  
- Access to VeChain node (Mainnet, Testnet, or custom)

---

## Project Setup

### 1) Wrap your app in `VeWorldProvider`

To enable wallet functionality globally, wrap your root component with `VeWorldProvider`:

```tsx
import React from 'react';
import { VeWorldProvider } from '@vechain/react-native-wallet-link';
import { TESTNET_URL } from '@vechain/sdk-network';
import * as Linking from 'expo-linking';

export default function App() {
  return (
    <VeWorldProvider
      appName="My VeChain App"
      appUrl="https://myvechainapp.com"
      redirectUrl={Linking.createURL('/', { scheme: 'myvechainapp' })}
      node={TESTNET_URL}
      config={{
        onVeWorldConnected: (response) => {
          console.log('Connected to VeWorld:', response);
        },
        onVeWorldDisconnected: () => {
          console.log('Disconnected from VeWorld');
        },
      }}
    >
      {/* Your app components go here */}
    </VeWorldProvider>
  );
}
```
### With Expo router
After you wrapped the app with the provider at the root level of your **App** folder create a new file named `+native-intent.tsx` since Expo router don't allow to use deep links to a route that doesn't exists and add the following content:
```ts
import { LinkEvent, isVeWorldResponse, processResponse } from "@vechain/react-native-wallet-link"

export function redirectSystemPath({
  path,
}: {
  path: string;
  initial: boolean;
}) {
  try {
    if (isVeWorldResponse(path)) {
      return processResponse(path)
        .then((response) => {
          switch (response.event) {
            case LinkEvent.OnVeWorldConnected:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldDisconnected:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldSignedTransaction:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldSignedCertificate:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldSignedTypedData:
              return "/your-custom-route";
            default:
              return "/your-custom-route";
          }
        })
        // Will throw error if the response from veworld is an error
        .catch((err) => {
          switch (err.event) {
            case LinkEvent.OnVeWorldConnected:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldDisconnected:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldSignedTransaction:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldSignedCertificate:
              return "/your-custom-route";
            case LinkEvent.OnVeWorldSignedTypedData:
              return "/your-custom-route";
            default:
              return "/error-or-custom-route";
          }
        });
    }
    return path;
  } catch {
    return "/error-or-custom-route";
  }
}
```
This file will handle the redirect to a specific route inside the app. You can take a look at [Expo docs](https://docs.expo.dev/router/advanced/native-intent/#rewrite-incoming-native-deep-links) for further details

*Inside here you can also manipulate/read data that you got from VeWorld the response.*

### 2) Configure Deep Linking

Your app needs to handle redirects from VeWorld using **deep links**.

For **Expo** (recommended):

```json
{
  "expo": {
    "scheme": "myvechainapp",
    "linking": {
      "prefixes": ["myvechainapp://", "https://myvechainapp.com"]
    }
  }
}
```

For **iOS**, update `Info.plist` with your URL scheme.  
For **Android**, define intent filters in `AndroidManifest.xml`.

> 💡 Tip: Use a unique app scheme to prevent collisions with other apps.

### 3) Verify Installation

After setup, rebuild your app and run it on a physical device with VeWorld installed.  
You should now be able to trigger VeWorld from your app and receive connection callbacks.

> 🧪 Try calling `connect(publicKey)` from `useVeWorldWallet()` — VeWorld should open and prompt for connection approval.

---

[← Back to Overview](./01-overview.md) · [Next → Integration Guide](./03-integration-guide.md)
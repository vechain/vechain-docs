# Integration Guide

## Overview

Once the SDK is installed and `VeWorldProvider` is configured, the next step is to **connect your app to VeWorld** and manage wallet interactions.

This section walks through:

- Setting up deep linking correctly  
- Managing encryption keys and session state  
- Connecting and disconnecting from VeWorld  
- Handling signed messages and transactions

By the end, your app will be able to securely sign and send transactions via the user’s VeWorld wallet.

---

## 1️⃣ Setup Deep Linking (Recap)

Your app and VeWorld communicate via **deep links**. This allows app-to-app navigation and encrypted data transfer.

For **Expo apps**, define your scheme in `app.json`:

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

For **bare React Native projects**:

- **iOS:** Add a URL Type to your `Info.plist`.  
- **Android:** Add an `<intent-filter>` in `AndroidManifest.xml`.

Make sure the `redirectUrl` you pass to `VeWorldProvider` matches your scheme exactly.

**With Expo:**

```tsx
redirectUrl={Linking.createURL('/', { scheme: 'myvechainapp' })}
```

**Bare RN (Universal Links, recommended):**

```tsx
redirectUrl={"https://myvechainapp.com"}
```

**Bare RN (Deep Links):**

```tsx
redirectUrl={"myvechainapp://"}
```

---

## 2️⃣ Manage Wallet State

The SDK requires you to manage a few essential data items in your app’s state.

```ts
interface VeWorldState {
  keyPair: {
    secretKey: string;
    publicKey: string;
  } | null;
  veWorldPublicKey: string | null;
  address: string | null;
  session: string | null;
}
```

You can manage this state however you prefer — using **React Context**, **Zustand**, or **Redux**.

> 💡 Tip: Persist this data with `AsyncStorage` so users stay connected between sessions.

---

## 3️⃣ Connect to VeWorld

Use the `connect` method from `useVeWorldWallet()` to initiate a secure handshake with VeWorld.

```tsx
const { generateKeyPair, connect } = useVeWorldWallet();
const [keyPair, setKeyPair] = useState<{ secretKey: string; publicKey: string } | null>(null);

// Generate key pair once on mount
useEffect(() => {
  if (!keyPair) {
    const newKeys = generateKeyPair();
    setKeyPair({
      secretKey: encodeBase64(newKeys.secretKey),
      publicKey: encodeBase64(newKeys.publicKey),
    });
  }
}, [keyPair, generateKeyPair]);

const handleConnect = () => {
  if (keyPair) {
    connect(keyPair.publicKey);
  }
};
```

When the user approves in VeWorld, the `onVeWorldConnected` event is triggered, returning encrypted session data.

---

## 4️⃣ Handle Connection Event

Example event handler for wallet connection:

```ts
onVeWorldConnected: (response) => {
  if ('errorCode' in response) {
    console.error(response.errorMessage);
    return;
  }

  const payload = decryptPayload<OnVeWorldConnectedData>(
    keyPair.secretKey,
    response.publicKey,
    response.nonce,
    response.data
  );

  setAddress(payload.address);
  setSession(payload.session);
  setVeWorldPublicKey(response.publicKey);
}
```

> ⚠️ Always check for `errorCode` before decrypting.  
> 💾 Store the `session`, `address`, and `veWorldPublicKey` securely for reuse.

---

## 5️⃣ Disconnecting

You can safely terminate a session and notify VeWorld:

```ts
disconnect(keyPair, veWorldPublicKey, session, "User manually disconnected");
```

After disconnection, clear all stored session data.

---

## 6️⃣ Signing and Sending Transactions

You can sign transactions or typed data directly from your app.

### Sign a Certificate

```ts
const certificate = {
  purpose: 'identification',
  payload: { type: 'text', content: 'Hello, VeWorld!' }
};
signCertificate(keyPair, veWorldPublicKey, session, certificate);
```

### Sign Typed Data (EIP-712)

```ts
const typedData = {
  domain: { name: 'MyApp', version: '1.0.0', chainId: 1 },
  origin: 'https://myapp.com',
  types: {
    Person: [
      { name: 'name', type: 'string' },
      { name: 'wallet', type: 'address' }
    ]
  },
  value: { name: 'Alice', wallet: '0x123...' }
};
signTypedData(keyPair, veWorldPublicKey, session, typedData);
```

### Send a Transaction

```ts
import { Clause, VET, Address } from '@vechain/sdk-core';

const tx = [
  Clause.transferVET(
    Address.of('0x9199828f14cf883c8d311245bec34ec0b51fedcb'),
    VET.of(0.1)
  )
];
signAndSendTransaction(keyPair, veWorldPublicKey, session, tx);
```

---

[← Back: Getting Started](./02-getting-started.md) · [Next → Wallet Hook](./04-wallet-hook.md)
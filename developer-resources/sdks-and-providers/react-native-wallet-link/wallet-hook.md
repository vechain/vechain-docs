# ⚙️ The `useVeWorldWallet` Hook

## Overview

The `useVeWorldWallet()` hook is your main interface for managing wallet interactions.  
It provides helper functions for generating keys, connecting, signing, and disconnecting — all while handling encryption internally.

---

## API Summary

| Method | Description |
|---|---|
| `generateKeyPair()` | Generates a new NaCl key pair |
| `connect(publicKey)` | Initiates a secure connection with VeWorld |
| `disconnect(keyPair, veWorldPublicKey, session, description?)` | Disconnects the wallet session |
| `signCertificate(keyPair, veWorldPublicKey, session, certificate, description?)` | Signs a plain-text message or structured payload |
| `signTypedData(keyPair, veWorldPublicKey, session, typedData, description?)` | Signs structured EIP-712 style data |
| `signAndSendTransaction(keyPair, veWorldPublicKey, session, transaction, description?)` | Signs and sends a transaction to the VeChain network |

---

## Example Usage

```tsx
import { useVeWorldWallet } from '@vechain/react-native-wallet-link';
import { encodeBase64 } from 'tweetnacl-util';

export const WalletComponent = () => {
  const {
    generateKeyPair,
    connect,
    disconnect,
    signCertificate,
    signTypedData,
    signAndSendTransaction
  } = useVeWorldWallet();

  const [keyPair, setKeyPair] = useState<any>(null);

  useEffect(() => {
    const keys = generateKeyPair();
    setKeyPair({
      secretKey: encodeBase64(keys.secretKey),
      publicKey: encodeBase64(keys.publicKey)
    });
  }, []);

  return (
    <>
      <Button title="Connect" onPress={() => connect(keyPair.publicKey)} />
      <Button title="Sign Data" onPress={() => signCertificate(keyPair, veWorldPublicKey, session, myCert)} />
    </>
  );
};
```

---

## Response Handling

All event responses follow a common structure:

```ts
type VeWorldResponse = {
  data: string;
  nonce: string;
  publicKey: string;
};

type VeWorldError = {
  errorCode: string;
  errorMessage: string;
};
```

Always validate before decrypting:

```ts
if ('errorCode' in response) {
  console.error('VeWorld Error:', response.errorMessage);
} else {
  const payload = decryptPayload(...);
}
```

---

## Example Flow Diagram

```
App (React Native)
   ↓ generateKeyPair()
   ↓ connect(publicKey)
→  VeWorld App (user approval)
   ↓ returns encrypted session
→  onVeWorldConnected()
   ↓
[Use session for signing & transactions]
```

---

[← Back: Integration Guide](./03-integration-guide.md) · [Next → Event Handlers](./05-event-handlers.md)
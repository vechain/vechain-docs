# Event Handlers

## Overview

`@vechain/react-native-wallet-link` uses event-driven callbacks to handle communication from the VeWorld wallet back to your application.  
Each event is triggered after a wallet action — connection, disconnection, signing, or transaction submission.  
These callbacks allow you to decrypt the returned payload, update your app state, and handle any potential errors gracefully.

You define these handlers inside the `config` prop of the `VeWorldProvider`.

---

## Example Configuration

```tsx
<VeWorldProvider
  appName="My VeChain App"
  appUrl="https://myvechainapp.com"
  redirectUrl={Linking.createURL('/', { scheme: 'myvechainapp' })}
  node={TESTNET_URL}
  config={{
    onVeWorldConnected,
    onVeWorldDisconnected,
    onVeWorldSignedCertificate,
    onVeWorldSignedTypedData,
    onVeWorldSentTransaction,
  }}
>
  {/* App components */}
</VeWorldProvider>
```

---

## onVeWorldConnected

Triggered when the user connects their VeWorld wallet successfully.

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

  console.log('Connected to wallet:', payload.address);
};
```

**Notes**

- Always check for `errorCode` before decryption.  
- Save the returned `session` and `publicKey` securely.  
- Once connected, your app can initiate signing and transaction requests.

---

## onVeWorldDisconnected

Triggered when the user disconnects from the wallet or the session is invalidated.

```ts
onVeWorldDisconnected: (response) => {
  if (response && 'errorCode' in response) {
    console.error(response.errorMessage);
    return;
  }

  setAddress(null);
  setSession(null);
  setVeWorldPublicKey(null);

  console.log('Disconnected from VeWorld');
};
```

**Notes**

- Clear all wallet-related state after disconnection.  
- Use this event to reset your app’s UI or session context.

---

## onVeWorldSignedCertificate

Triggered when the wallet signs a plain-text or certificate message.

```ts
onVeWorldSignedCertificate: (response) => {
  if ('errorCode' in response) {
    console.error(response.errorMessage);
    return;
  }

  const payload = decryptPayload<OnVeWorldSignedData>(
    keyPair.secretKey,
    response.publicKey,
    response.nonce,
    response.data
  );

  console.log('Certificate Signature:', payload.signature);
};
```

**Notes**

- Use this event for user authentication, message attestation, or identity verification.

---

## onVeWorldSignedTypedData

Triggered after a successful EIP-712 typed data signing operation.

```ts
onVeWorldSignedTypedData: (response) => {
  if ('errorCode' in response) {
    console.error(response.errorMessage);
    return;
  }

  const payload = decryptPayload<OnVeWorldSignedData>(
    keyPair.secretKey,
    response.publicKey,
    response.nonce,
    response.data
  );

  console.log('Typed Data Signature:', payload.signature);
};
```

**Notes**

- Useful for DApps using structured data (EIP-712) for verifiable off-chain signatures.

---

## onVeWorldSentTransaction

Triggered when a transaction is signed and submitted by the wallet.

```ts
onVeWorldSentTransaction: (response) => {
  if ('errorCode' in response) {
    console.error(response.errorMessage);
    return;
  }

  const payload = decryptPayload<OnVeWorldSignedTransactionData>(
    keyPair.secretKey,
    response.publicKey,
    response.nonce,
    response.data
  );

  console.log('Transaction ID:', payload.transaction.id);
};
```

**Notes**

- The payload contains the transaction ID and clause details.  
- You can track this transaction using a VeChain explorer.

---

[← Back: Wallet Hook](./04-wallet-hook.md) · [Next → Error Handling](./06-error-handling.md)
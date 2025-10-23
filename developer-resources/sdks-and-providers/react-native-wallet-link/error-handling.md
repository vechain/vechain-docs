# 🧰 Error Handling & Security

## Overview

The VeWorld Wallet Link SDK uses encrypted communication for every message exchange.  
This section covers how to handle errors properly and secure sensitive data (keys, sessions, and payloads).

---

## Common Error Structure

Every event can return either a success or an error response.

```ts
type VeWorldResponse = {
  data: string;
  nonce: string;
  publicKey: string;
};

type VeWorldError = {
  errorCode: VeWorldErrorCode;
  errorMessage: string;
};
```

Before decrypting, **always check** whether the response contains an `errorCode`.

```ts
if ('errorCode' in response) {
  console.error('VeWorld Error:', response.errorCode, response.errorMessage);
  return;
}

const payload = decryptPayload(/* ... */);
```

---

## Error Codes

When making requests to VeWorld—establishing a connection, sending a transaction, or signing a message—VeWorld may respond with an error.  
These codes are inspired by Ethereum’s EIP‑1474 and EIP‑1193.

| Error Code | Error Name | Error Description |
|---:|---|---|
| 4100 | Unauthorized | The requested method and/or account has not been authorized by the user. |
| 4001 | User rejected connection | The user rejected the request through VeWorld. |
| 4900 | Disconnected | VeWorld could not connect to the network. |
| -32002 | Resource Not Available | A new request was sent while an approval dialog is already open. Wait for the current approval to finish. |
| -32003 | Transaction Rejected | VeWorld does not recognize a valid transaction. |
| -32600 | Invalid Payload | The payload is invalid. |
| -32601 | Method Not Found | VeWorld does not recognize the requested method. |
| -32602 | Invalid Parameters | Missing or invalid parameters. |
| -32603 | Internal Error | Something went wrong within VeWorld. |

> 💡 Tip: Keep a human-readable mapping of these errors for UI display (e.g., “Please approve connection in VeWorld”).

---

## Key Storage Guidelines

- **Never store keys in plain text.**  
  Use secure storage modules such as **Expo SecureStore** or **react-native-keychain**.  
- **Generate keys once per installation.**  
  A key pair should be created once and reused until manually reset.  
- **Do not log keys or decrypted data.**  
  Avoid logging payloads that contain private or sensitive information.  
- **Encrypt or obfuscate storage where possible.**  
  Even temporary storage (`AsyncStorage`) should be considered untrusted.

---

## Session Management

- Each connection establishes a **session token** for communication.  
- Sessions **do not expire automatically** but can be invalidated manually.  
- On logout or disconnect, always clear:

```ts
setSession(null);
setVeWorldPublicKey(null);
setAddress(null);
```

Treat session data like an authentication token — store securely.

---

## Troubleshooting Common Issues

| Issue | Possible Cause | Fix |
|---|---|---|
| Deep links not working | Scheme not registered or redirect URL mismatch | Verify `scheme` and `redirectUrl` configuration |
| VeWorld app not opening | Incorrect deep link or app missing | Test link manually on device |
| Connection fails | Invalid public key or network error | Regenerate keys and retry |
| Decryption fails | Key mismatch between app and VeWorld | Ensure same key pair used for connect + decrypt |
| Transaction rejected | User denied request | Handle gracefully and provide retry option |

---

## Security Checklist ✅

- Keys stored in SecureStore or Keychain  
- Error handling checks `errorCode` before decrypting  
- Session cleared on logout/disconnect  
- Logging sanitized of sensitive data  
- Deep link scheme unique to the app

---

[← Back: Event Handlers](./05-event-handlers.md) · [Next → Network Configuration](./07-network-configuration.md)
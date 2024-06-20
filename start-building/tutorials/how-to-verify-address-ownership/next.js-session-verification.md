---
description: >-
  By using certificate signing, you can implement stateless session management
  in applications like Next.js.
---

# Next.js Session Verification

## Browser Sign In with VeWorld

With `useWallet()` and the `WalletButton`, users can be prompted to sign into an application.

When signing in, users are asked to sign a message. The signed message and signature can then be used to verify ownership of a specific address.

### Enable Certificate Sharing with dApp-Kit

The `DAppKitProvider` needs to have `requireCertificate` enabled to share it with the application:

```tsx
<DAppKitProvider
  nodeUrl="https://mainnet.vechain.org/"
  requireCertificate
  usePersistence
>
  {children}
</DAppKitProvider>
```

### Harden With Server-side Challenges

To make sign-in more secure, you can use custom challenges. These challenges are shown to the user during sign-in. You can set a custom certificate in the `DAppKitProvider`. This certificate can come from a server-side generated message:

```tsx
<DAppKitProvider
  nodeUrl="https://mainnet.vechain.org/"
  requireCertificate
  usePersistence
  connectionCertificate={{
    message: {
      purpose: "identification",
      payload: {
        type: "text",
        content: sessionChallenge,
      },
    },
  }}
>
  {children}
</DAppKitProvider>
```

### Access Certificate

When `requireCertificate` is enabled, you can get the `connectionCertificate` from the `useWallet()` hook. After the user connects their wallet with the `WalletButton`, you can use the certificate for verification.

```tsx
"use client"; // This is a client component
import { type ReactElement, useEffect, useState } from "react";
import { WalletButton, useWallet } from "@vechain/dapp-kit-react";

const Button = (): ReactElement => {
  const { connectionCertificate } = useWallet();

  useEffect(() => {
    // handle certificate
  }, [connectionCertificate]);

  return (
    <div className="container">
      <WalletButton />
    </div>
  );
};

const HomePage = (): ReactElement => {
  return <Button />;
};

// eslint-disable-next-line import/no-default-export
export default HomePage;
```

## Backend Verification

### Send to Backend

A common way to pass authentication to backends is by using the `authorization` header.

You can Base64 encode the received certificate to easily send it to an API:

```ts
const encodedCertificate = btoa(JSON.stringify(connectionCertificate));
fetch("/api/verify", {
  method: "GET",
  headers: {
    authorization: encodedCertificate,
  },
})
```

### Verify Certificate

To verify the certificate, you need to decode it from base64 and parse it back to a JSON object.

You can use `certificate.verify()` to check if the certificate is valid. If the certificate has been tampered with, it will throw an error.

The certificate contains important information for access control in the application. Key attributes include:

* `signer`: the address that signed the message (in lower case)
* `payload`: the message signed by the user
* `domain`: the domain where the wallet signed the message
* `timestamp`: the unix timestamp when the message was signed

Here is an example API function that verifies a received certificate:

```ts
import type { NextApiRequest, NextApiResponse } from "next";
import { certificate } from "@vechain/sdk-core";
export default function handler(
  req: NextApiRequest,
  res: NextApiResponse<object>
) {
  const authHeader = req.headers.authorization;
  const decodedAuthHeader = atob(authHeader ?? "");
  const decodedCertificate = JSON.parse(decodedAuthHeader);

  if (!decodedCertificate) {
    return res.json({
      status: "missing",
      authHeader,
      decodedAuthHeader,
      decodedCertificate,
    });
  }

  try {
    // verify it
    certificate.verify(decodedCertificate);

    // further verify attributes like signer, domain or payload of the decodedCertificate
    // verify timestamp/max. validity

    return res.json({
      status: "verified",
      authHeader,
      certificate,
      user: decodedCertificate.signer,
    });
  } catch (err: any) {
    return res.json({
      status: "failed",
      authHeader,
      decodedAuthHeader,
      decodedCertificate,
      errorMessage: err.message,
    });
  }
}
```

## Example Project

A Next.js example is available on StackBlitz:

[https://stackblitz.com/edit/nextjs-dappkit-certificate?file=pages%2Fapi%2Fverify.ts](https://stackblitz.com/edit/nextjs-dappkit-certificate?file=pages%2Fapi%2Fverify.ts)

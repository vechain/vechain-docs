# 🧭 Overview

## Introduction

`@vechain/react-native-wallet-link` is a React Native SDK that enables seamless integration between native applications and VeChain’s VeWorld wallet.  
It allows developers to easily connect, sign messages, and send transactions securely — all through VeWorld’s mobile app.  
With this library, your app can initiate deep links to VeWorld, exchange encrypted messages, and manage authenticated sessions with minimal setup.

[View on npm](https://www.npmjs.com/package/@vechain/react-native-wallet-link)

---

## Key Features

| Feature | Description |
|---|---|
| 🔑 **Wallet Connection** | Establishes a secure session with the VeWorld wallet via deep links |
| ✍️ **Message Signing** | Supports signing of certificates and typed data (EIP-712) |
| 💸 **Transaction Signing** | Allows users to sign and broadcast transactions on VeChain mainnet or testnet |
| 🔐 **Secure Communication** | Built on NaCl cryptography for end-to-end encrypted communication |
| 🔗 **Deep Link Integration** | Enables smooth app-to-app interactions between your dApp and VeWorld |
| 🌐 **Network Flexibility** | Easily switch between Mainnet, Testnet, or a custom node |

---

## When to Use

Use this SDK if you are building:

- A React Native app that needs to interact with VeWorld wallet  
- An app that requires secure signing of transactions or message authentication  
- A VeChain-powered experience that benefits from native-level UX and secure wallet linking

---

## Architecture Overview

The SDK leverages **deep linking** and **NaCl-based encryption** to create a secure, encrypted communication channel between your app and VeWorld.

**How it works:**

1. Your app generates a key pair (`generateKeyPair()`).  
2. The app opens VeWorld via deep link, passing the public key.  
3. VeWorld responds with an encrypted payload containing session details and wallet address.  
4. All subsequent requests (signing, transactions, etc.) use this encrypted session.

> 🧩 This ensures **no private keys ever leave VeWorld**, while maintaining full message integrity between your app and the wallet.

---

[Next → Getting Started](./02-getting-started.md)
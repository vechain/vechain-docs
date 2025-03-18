# Fee Delegation

Gas fees are usually paid by the address that signs the transaction. VeChain's fee delegation allows you to pass on this payment to another wallet, which can either reside as private key in your realm or shielded by a web service.

To use fee delegation, you can need to:

1. Enable it while building the transaction object
2. Provide information about the delegator during transaction signing

## Enable Fee Delegation

To enable fee delegation as feature, you need to set `isDelegated` to `true` while building the transaction body:

```js
const tx = await thor.transactions.buildTransactionBody(clauses, gas,
  { isDelegated: true }
);
```

## Sign with Fee Delegation

To get the fee delegator involved, you'll pass either `delegatorPrivateKey` or `delegatorUrl` to the signing wallet:

```js
const walletWithUrlSponsor = new ProviderInternalBaseWallet(
  [{ privateKey, address: senderAddress }],
  {
    delegator: {
      delegatorUrl: 'https://sponsor-testnet.vechain.energy/by/90',
    },
  }
);

const walletWithAccountSponsor = new ProviderInternalBaseWallet(
  [{ privateKey, address: senderAddress }],
  {
    delegator: {
      delegatorPrivateKey: delegatorAccount.privateKey,
    },
  }
);
```

### Example Project

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/transaction-execute?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

## Sign as Delegator Service

To shield your private key for paying gas fees into a backend service, you can setup a web-service that receives a raw transaction and co-signs it to confirm gas payment (based on [VIP-201](https://github.com/vechain/VIPs/blob/master/vips/VIP-201.md)).

The process requires you to rebuilt a transaction object from a hex encoded version:

```javascript
const transactionToSign = TransactionHandler.decode(
  Buffer.from(req.body.raw.slice(2), 'hex')
);
```

Afterwards a unique hash is calculated for the given transaction, only valid if a specific origin will sign it:

```javascript
const delegatedHash = transactionToSign.getSignatureHash(req.body.origin);
```

The resulting hash is signed and then returned as hex string for further processing on the client side:

```javascript
const signature = `0x${Buffer.from(
    secp256k1.sign(delegatedHash, delegatorPrivateKey)
  ).toString('hex')}`;
```

### Example Project

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/delegation-service?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

# VET Transfers

## Connection

The connection is managed using WebSockets, which connect directly to a VeChain node.

A simple connection can be established with this snippet:

```js
import WebSocket from 'ws';
const ws = new WebSocket('wss://mainnet.vechain.org/subscriptions/transfer');
ws.onmessage = (message) => {
    console.log('New transfer', message.data);
}
```

This will receive all transfers on the blockchain as JSON-encoded strings.

## Filter Specific Transfers

The VeChain SDK facilitates the construction of filters to retrieve only the desired data by generating a subscription URL with specified parameters. Using the `subscriptions` helper, you can create a custom subscription URL that listens exclusively to the specified event.

All options are optional, and a transfer must match all specified criteria:

```js
const wsUrl = subscriptions.getVETtransfersSubscriptionUrl(
  'https://mainnet.vechain.org',
  {
    blockID: undefined, // block id to start from, defaults to the best block.
    signerAddress: undefined, // The address of the signer/origin of the transaction to filter transfers by.
    sender: undefined, // The sender address to filter transfers by.
    recipient: undefined, // The recipient address to filter transfers by.
  }
);
```

## Transfer Details

The transfers are received as JSON-encoded strings. These strings must be parsed into usable objects, resulting in an object of type [`TransferLogs`](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.TransferLogs.html#meta).

An example result is:

```json
{
  "sender": "0xff5ba88a17b2e16d23ff6647e9052e937acb1406",
  "recipient": "0xf1663a96eb4760d74a3084636b25eac161c238ed",
  "amount": "0xa7b7a750ac2f0400",
  "meta": {
    "blockID": "0x0117dfcc79e6cfd0002a99aca8af0123cf1b1f3c67df7d3eb1e22aaf286088b2",
    "blockNumber": 18341836,
    "blockTimestamp": 1713946150,
    "txID": "0xb5dc022265321a2bc3aef9faf9224544b0ff54fcaf1d4f5846fc6caee0187009",
    "txOrigin": "0xff5ba88a17b2e16d23ff6647e9052e937acb1406",
    "clauseIndex": 0
  },
  "obsolete": false
}
```

The amount is a hexlified BigInt that can be converted into a BigInt using `BigInt(transferLog.amount)`.

## Example Project

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/listen-transfers?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

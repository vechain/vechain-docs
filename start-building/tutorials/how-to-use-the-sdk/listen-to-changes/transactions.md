# Transactions

## Connection

The connection is managed using WebSockets, which connect directly to a Vechain node.

A simple connection can be established with this snippet:

```js
import WebSocket from 'ws';
const ws = new WebSocket('wss://mainnet.vechain.org/subscriptions/txpool');
ws.onmessage = (message) => {
    console.log('New pending transaction', message.data);
}
```

This will receive all new entries added to the transaction pool in the form of JSON-encoded strings.

Subscriptions only receive the transaction ID as soon as it is added to the transaction pool. A transaction may either be successfully included in a block, reverted, or expire in the future.

To obtain detailed information about a transaction, you will need to make a second request, either directly from the node or by using a Thor client.

```js
await fetch(`https://mainnet.vechain.org/transactions/${txId}?pending=true`).then(res => res.json())
```

```js
const tx = await thor.transactions.getTransaction(addedTx.id, {
  pending: true,
});
```

## Example Project

{% embed url="https://stackblitz.com/edit/vechain-sdk-listen-transactions?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

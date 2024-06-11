# Blocks

## Connection

The connection is managed using WebSockets, which connect directly to a VeChain node.

A simple connection can be established with this snippet:

```js
import WebSocket from 'ws';
const ws = new WebSocket('wss://mainnet.vechain.org/subscriptions/block');
ws.onmessage = (message) => {
    console.log('New block', message.data);
}
```

This will receive a new block as soon as it is added to the blockchain, in the form of JSON-encoded strings.

## Options

To resume listening from a specific block position, the options can include a `blockID` to continue from where a previous listener may have disconnected.

For additional details on the options, refer to the documentation of [`BlockSubscriptionOptions`](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.BlockSubscriptionOptions.html).

## Block Details

The blocks are received as JSON-encoded strings. These strings must be parsed into usable objects, resulting in an object of type [`BlockDetail`](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.BlockDetail.html#meta).

An example result is:

```json
{
  number: 18342166,
  id: '0x0117e116630b0db7c0208cf0e01d9dfefcc400310e75e738ebafaeca221ae31d',
  size: 684,
  parentID: '0x0117e115cc9e7eab70f4513ab8d82517c2d6e5dee3c121f5caba9dbfe517587f',
  timestamp: 1713949450,
  gasLimit: 29999972,
  beneficiary: '0x0ffb1cbc86b3ad0a17292b7fda577d59c0d7aed9',
  gasUsed: 57454,
  totalScore: 1787902837,
  txsRoot: '0x00a3024aac1092060e5f9368dd364f9eb9918eddc2d5ecfd92c64faf506c5176',
  txsFeatures: 1,
  stateRoot: '0x3ffc3fecb7d43d982b712f38ea5c9324375bc0c8db9f54dae91bd07777905b9e',
  receiptsRoot: '0x186a987d166ec60daf5a54ef97344a47d5c6e5f816b51e8ae49b14a332aebbb1',
  com: true,
  signer: '0x9e1c86df9e17451c0177544aa9a55edb3e0581b0',
  transactions: [
    '0xecc1a99b0afcf25c3283babc91641ed57d7dd3e6ae9e78058c439ae8c476f543',
    '0x27af83997e4b045024eafdb6041a97097de8cd528a22176056d0652f81a98fc4'
  ],
  obsolete: false
}
```

## Example Project

{% embed url="https://stackblitz.com/edit/vechain-sdk-listen-blocks?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

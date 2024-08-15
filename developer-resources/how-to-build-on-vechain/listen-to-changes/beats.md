# Beats

Beats are messages that are sent on each new block, containing tiny bits of data that can be used to detect changes happening on the blockchain. Beats provide as little data as possible to remove the need to load full block and receipt data every time.

## Connection

The connection is managed using WebSockets, which connect directly to a VeChain node.

A simple connection can be established with this snippet:

```js
import WebSocket from 'ws';
const ws = new WebSocket('wss://mainnet.vechain.org/subscriptions/beat2');
ws.onmessage = (message) => {
    console.log('New block', message.data);
}
```

This will receive a new block as soon as it is added to the blockchain, in the form of JSON-encoded strings with a bloom filter which can be used to check if the block contains an account.

## Options

To resume listening from a specific block position, the options can include a `blockID` to continue from where a previous listener may have disconnected.

For additional details on the options, refer to the documentation of [`BlockSubscriptionOptions`](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.BlockSubscriptionOptions.html).

## Block Details

The blocks are received as JSON-encoded strings. These strings must be parsed into usable objects.

An example result is:

```json
{
  number: 18342209,
  id: '0x0117e1411afb526f813370417d23d1757e03c47887d73de999bb178919d41f96',
  parentID: '0x0117e1408ea3161e8561868dbae1828841588954bd71ae845866d9b67ec07e83',
  timestamp: 1713949880,
  txsFeatures: 1,
  gasLimit: 30146568,
  bloom: '0x990c2f3331b75f955af09180665aadf3f017',
  k: 13,
  obsolete: false
}
```

## Bloom Filter

{% hint style="info" %}
[You can find more information about the Bloom Filter in another section of the documentation.](../../sdks-and-providers/sdk/bloom-filter.md)
{% endhint %}

It enables the verification of interactions involving a specific address, potentially eliminating the need for further transaction or block lookups if the block lacks information related to that address.

The `bloomUtils` offer a straightforward test function to determine whether an address has had interactions within a block:

```js
import { bloomUtils } from '@vechain/sdk-core'

const addressToTest = '0x0000000000000000000000000000000000000000'
console.log('Interaction found', bloomUtils.isAddressInBloom(block.bloom, block.k, addressToTest))
```

The bloom filter is used for testing and includes:

* The Gas Payer of a transaction
* The emitters of all events within transactions
* The topics of all events in transactions that include an address or shorter than an address
* The sender and receiver of transfers
* The origin of the transaction
* The signer of the block
* The beneficiary of the block

{% hint style="info" %}
For more details on the implementation, you can view the [node's code on GitHub](https://github.com/vechain/thor/blob/d847c4683469a8ccffb4e472ca7449059b3ceefc/api/subscriptions/beat2\_reader.go#L29-L90).
{% endhint %}

`bloomUtils.isInBloom` provides an additional filter to check for the presence of non-address data, such as numbers emitted within events. It can also be used to check for the VTHO contract, whose address is a special one because its the bytes32-encoded version of the word "Energy" (`0x456e65726779`).

```javascript
const dataToTest = "0x456e65726779"
console.log('Data found', bloomUtils.isInBloom(block.bloom, block.k, dataToTest))
```

## Example Project

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/listen-beats?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

Another example can be found on GitHub using a React Hook that listens and provides state updates when information is found in a new block. For example, transaction IDs or addresses:

[https://github.com/ifavo/example-buy-me-a-coffee/blob/main/src/hooks/useBeats.ts](https://github.com/ifavo/example-buy-me-a-coffee/blob/main/src/hooks/useBeats.ts)

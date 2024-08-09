# Events

## Example Data

This example used below will utilize the VTHO contract, which manages VeChain's VTHO Token.

* Smart Contract Address: `0x0000000000000000000000000000456e65726779`
* The contract's source code can be found on GitHub at: [https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol](https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol)
* Its Application Binary Interface (ABI) is shared on b32, a repository that gathers publicly available interfaces for VeChain projects: [https://github.com/vechain/b32/blob/master/ABIs/energy.json](https://github.com/vechain/b32/blob/master/ABIs/energy.json)

## Connection

The connection is managed using WebSockets, which connect directly to a VeChain node.

A simple connection can be established with this snippet:

```js
import WebSocket from 'ws';
const ws = new WebSocket('wss://mainnet.vechain.org/subscriptions/event');
ws.onmessage = (message) => {
    console.log('New event', message.data);
}
```

This will receive all events on the blockchain as JSON-encoded strings.

## Filter Specific Events

The VeChain SDK assists in constructing filters to retrieve only the desired data by creating a subscription URL with the specified parameters.

A helper utility, `coder`, generates ethers compatible interfaces that can be utilized to construct the encoded filters.

The following snippet demonstrates how to set up the interface:

```js
import { coder } from '@vechain/sdk-core';

// create an interface for the contract events to listen
const contractInterface = coder.createInterface([
  'event Transfer (address indexed from, address indexed to, uint256 value)',
]);
```

Once the interface is available, it can be used to obtain encoded event information:

```js
contractInterface.getEvent('Transfer')
```

Using the `subscriptions` helper, a custom subscription URL can be built that listens only to the specified event:

```js
const wsUrl = subscriptions.getEventSubscriptionUrl(
  'https://mainnet.vechain.org',
  contractInterface.getEvent('Transfer')
);
```

### Event Parameters

Filters can be adjusted to only show events that meet specific criteria. These parameters must be `indexed` and are given as a list.

The transfer event uses two indexed parameters: `from` and `to`.

For instance, to filter all transfers originating from a specific address, you would supply that address as the first parameter:

```js
const wsUrl = subscriptions.getEventSubscriptionUrl(
  'https://mainnet.vechain.org',
  contractInterface.getEvent('Transfer'),
  ['0x0000000000000000000000000000456e65726779']
);
```

To filter for all transfers to a specific address, provide only the second value in the list:

```js
const wsUrl = subscriptions.getEventSubscriptionUrl(
  'https://mainnet.vechain.org',
  contractInterface.getEvent('Transfer'),
  [null, '0x0000000000000000000000000000456e65726779']
);
```

When using filters, all provided values must match for the filters to apply.

### Blockchain Parameters

#### Emitter

Many contracts emit similar events, which sometimes necessitates restricting listening to a specific contract. An optional `options` argument can be used to filter for a particular contract address.

For example, to listen exclusively for VTHO transfers from the VTHO contract at `0x0000000000000000000000000000456e65726779`, it would be defined as follows:

```js
const wsUrl = subscriptions.getEventSubscriptionUrl(
  'https://mainnet.vechain.org',
  contractInterface.getEvent('Transfer'),
  [],
  { address: '0x0000000000000000000000000000456e65726779' }
);
```

#### Blocks

To resume listening from a specific block position, the options can define a `blockID` to continue from where a previous listener may have disconnected.

{% hint style="info" %}
For additional details on the options, check out the documentation of [`EventSubscriptionOptions`](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.EventSubscriptionOptions.html).
{% endhint %}

## Decoding Events

The events are received as JSON-encoded strings. These strings must be parsed and decoded into usable objects.

Using the contract interface defined earlier, you can decode these events with the `parseLog()` function:

```js
ws.onmessage = (message) => {
  // data is received as text and needs to be converted into an object first
  console.log('Received data', message.data);
  const eventLog = JSON.parse(message.data);

  const decoded = contractInterface.parseLog(eventLog);
  if (!decoded || decoded?.name !== 'Transfer') {
    throw new Error('Unknown Event');
  }

  // decoded.args will have the following attributes:
  // decoded.args.from, decoded.args.to, decoded.args.value
  // and
  // decoded.args[0], decoded.args[1], decoded.args[2]
}
```

{% hint style="info" %}
Generic transaction details such as ID, block information, or the origin of the transaction are available in the object as well. Check `eventLog.meta` from the example. Learn more about the message type definition in the documentation of [`EventLogs`](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.EventLogs.html#meta).
{% endhint %}

## Example Project

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/listen-events?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

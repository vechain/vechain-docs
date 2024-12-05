---
description: How to connect with to VeChainThor blockchain using @vechain/sdk-network
---

# Connect to the Network

Interacting with VeChainThor requires only an instance of `ThorClient` that is configured for the relevant network. Once the connection is established, this instance can be utilized to interact in an asynchronous manner. Below is a snippet that demonstrates importing the library and initializing a client:

```js
import { ThorClient } from "@vechain/sdk-network";
const thor = ThorClient.at("https://mainnet.vechain.org");
```

The snippet connects to the MainNet, where all production related activity is found.

Additionally there is a TestNet available for testing and development purposes. This allows developers to experiment without risking real assets.

To connect to the TestNet use `https://testnet.vechain.org` as URL. If you have deployed a  [solo node of VeChain](../../how-to-run-a-node/how-to-run-a-thor-solo-node.md), it is normally available on `http://localhost:8669`.

{% hint style="info" %}
The `ThorClient` uses a `HttpClient` underneath to communicate with the VeChain nodes with a [JSON API](https://mainnet.vechain.org/doc/swagger-ui/).

The default [`HttpClient` is an Axios implementation](https://github.com/vechain/vechain-sdk-js/blob/v1.0.0/packages/network/src/utils/http/http-client.ts) and can be replaced with any custom implementation as long as the interfaces are met. Example use cases for custom implementations can be custom headers to access protected nodes.
{% endhint %}

To test the connectivity we'll get request the first and last block from the chain and output their number & id:

```js
// get the current latest & best block from the chain
const bestBlock = await thor.blocks.getBestBlockCompressed();
console.log("Best Block:", bestBlock.number, bestBlock.id);

// get the first and genesis block from the chain
const genesisBlock = await thor.blocks.getBlockCompressed(0);
console.log("Genesis Block:", genesisBlock.number, genesisBlock.id);
```

You can test the above snippet here:

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/connect?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

{% hint style="info" %}
The `ThorClient` provides a multitude of properties with access to all relevant functionality on VeChain. You can find examples and details about all of them in the [Thor Client docs](../../../developer-resources/sdks-and-providers/sdk/thor-client.md).
{% endhint %}

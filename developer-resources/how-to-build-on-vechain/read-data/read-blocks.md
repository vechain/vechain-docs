# Read Blocks

A block is a change to the blockchain storage with a batch of changes that happen simultaneously. With VeChain, every \~10s a new block is generated, even if no transaction has been published.

The most relevant information for interacting with Blocks includes:

* **number**: the number of the block
* **id**: a unique id representing the block
* **parentID**: the previous block the block is based on
* **timestamp**: the unix time at which the block was stored
* **isFinalized**: is the block securely finalized in a snapshot
* **transactions**: contain either all transaction ids or full transaction details including receipts

There are two methods to obtain block details:

1. The _compressed_ version, which includes all data and only the transaction IDs.
2. The _expanded_ version, which also encompasses full transaction details along with the generated outputs.

A block can be requested as number, id and additionally the reserved words "best" and "finalized" reference the latest or epoch ending blocks.

```js
const blockNumber = 12345678;

// get the block and transaction ids within it
const compressed = await thor.blocks.getBlockCompressed(blockNumber);
console.log(compressed);

// get the block and transaction data including receipts
const expanded = await thor.blocks.getBlockExpanded(blockNumber);
console.log(expanded);
```

Test it yourself:

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/read-block?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

Type definition and documentation of all attributes:

* [Compressed Block Detail](https://vechain.github.io/vechain-sdk-js/classes/_vechain_sdk_network.BlocksModule.html#getBestBlockCompressed)
* [Expanded Block Detail](https://vechain.github.io/vechain-sdk-js/classes/_vechain_sdk_network.BlocksModule.html#getBestBlockExpanded)

The same information is available using the JSON-API:

* [GET /blocks/{block}](https://mainnet.vechain.org/blocks/12345678)
* [GET /blocks/{block}?expanded=true](https://mainnet.vechain.org/blocks/12345678?expanded=true)

### **Special Blocks**

There are specific keywords associated with special blocks:

* **Genesis** refers to the initial block (number `0`) on a chain, serving also to identify the chain (chain ID) in the ecosystem and among similar networks (EVMs).
* **Best** represents the most recent block, typically having a maximum age of 10 seconds, as a new block is added every 10 seconds.
* **Final** denotes the most recent finalized block, marking the end of an epoch. It is guaranteed that there will be no further re-ordering or changes. A checkpoint happens every 180 blocks and finalization of a checkpointed block occurs again after 180 blocks.

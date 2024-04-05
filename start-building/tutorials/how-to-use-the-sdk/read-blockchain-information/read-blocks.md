# Read Blocks

A block is a change to the blockchain storage with a batch of changes that happen simultaneously. With Vechain, every \~10s a new block is generated, even if no transaction has been published.

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

{% embed url="https://stackblitz.com/edit/vechain-sdk-read-block?embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

The same information is available using the JSON-API:

* [https://mainnet.vechain.org/blocks/12345678](https://mainnet.vechain.org/blocks/12345678)
* [https://mainnet.vechain.org/blocks/12345678?expanded=true](https://mainnet.vechain.org/blocks/12345678?expanded=true)

### **Special Blocks**

There are specific keywords associated with special blocks:

* **Genesis** refers to the initial block (number `0`) on a chain, serving to identify the available chain on a network.
* **Best** represents the most recent block, typically having a maximum age of 10 seconds, as a new block is added every 10 seconds.
* **Final** denotes the most recent finalized block, marking the end of an epoch. It is guaranteed that there will be no further re-ordering or changes. This usually occurs every 180 blocks.
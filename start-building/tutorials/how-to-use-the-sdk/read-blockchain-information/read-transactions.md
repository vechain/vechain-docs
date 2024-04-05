# Read Transactions

A transaction is a request for a change on the blockchain, which can either be a transfer of VET or the execution of a contract's function. Each transaction is signed and submitted by a single entity and may contain multiple instructions, known as multi-clause, to interact with various recipients on the blockchain.

The most relevant information of a transaction includes:

* **id**: The unique identifier of the transaction.
* **chainTag**: Identifies the chain to which the transaction belongs.
* **blockRef**: The block on which the call was based.
* **expiration**: The maximum number of blocks within which the transaction must be included in the blockchain (based on `blockRef`), or it will fail.
* **dependsOn**: Requires this transaction id to be successful first before being included in the blockchain.
* **origin**: The sender of the transaction.
* **meta**: Information about the block where this transaction was included, providing more details about time and block through **blockID**, **blockNumber**, and **blockTimestamp**.
* **reverted**: Indicates whether the transaction failed.
* **clauses**: The instructions to be executed, including a list of the recipients to be called, the data sent, and potential VET transfer values.
* **outputs**: Events that have been emitted as a result of the executed instructions.

A transaction's complete details are comprised of two main components:

1. The basic version, which includes all input data and details on how the transaction is stored.
2. The receipt, which lists all changes emitted by the blockchain, including:
   * the reverted flag,
   * the address of a newly deployed contract,
   * VET transfers,
   * events initiated by contracts.

Example snippet to access transaction details:

```js
// get a single transaction
const txId =
  '0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07';
const tx = await thor.transactions.getTransaction(txId);
console.log(tx);

// load effected changes & outputs with the transaction
const txReceipt = await thor.transactions.getTransactionReceipt(txId);
console.log(txReceipt);
```

Test it yourself:

{% embed url="https://stackblitz.com/edit/vechain-sdk-read-transaction?embed=1&hideExplorer=1&hideNavigation=1&view=editor" %}

The same information is available using the JSON-API:

* Successful Transaction: [https://mainnet.vechain.org/transactions/0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07](https://mainnet.vechain.org/transactions/0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07)
* Successful Transaction Receipt: [https://mainnet.vechain.org/transactions/0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07/receipt](https://mainnet.vechain.org/transactions/0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07/receipt)
* Unsuccessful Transaction: [https://mainnet.vechain.org/transactions/0xae4a0ce2423c49cdb286cdde6691bdc77e9d06e2f5a4d0c3205c79af7d89bf7b](https://mainnet.vechain.org/transactions/0xae4a0ce2423c49cdb286cdde6691bdc77e9d06e2f5a4d0c3205c79af7d89bf7b)
* Unsuccessful Transaction Receipt: [https://mainnet.vechain.org/transactions/0xae4a0ce2423c49cdb286cdde6691bdc77e9d06e2f5a4d0c3205c79af7d89bf7b/receipt](https://mainnet.vechain.org/transactions/0xae4a0ce2423c49cdb286cdde6691bdc77e9d06e2f5a4d0c3205c79af7d89bf7b/receipt)

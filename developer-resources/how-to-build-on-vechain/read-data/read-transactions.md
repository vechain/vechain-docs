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
if your transaction is still pending, the receipt will be `null`, so if you wish to wait for your transaction receipt you will need to use waitForTransactionReceipt instead.

```ts
// load effected changes & outputs with the transaction
const txReceipt = await thor.transactions.waitForTransactionReceipt(txId);
console.log(txReceipt);
```

Test it yourself:

{% embed url="https://stackblitz.com/edit/vechain-academy-read-transaction?embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

Type definition and documentation of all attributes:

* [Transaction Body](https://vechain.github.io/vechain-sdk-js/interfaces/_vechain_sdk_network.TransactionBodyOptions.html)
* [Transaction Receipt](https://vechain.github.io/vechain-sdk-js/interfaces/_vechain_sdk_network.TransactionReceipt.html)

The same information is available using the JSON-API:

* Successful Transaction: [GET /transactions/{transactionId}](https://mainnet.vechain.org/transactions/0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07)
```
{
  "id": "0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07",
  "type": 0,
  "chainTag": 74,
  "blockRef": "0x00bc614dda10f9e1",
  "expiration": 720,
  "clauses": [
    {
      "to": "0x0000000000000000000000000000456e65726779",
      "value": "0x0",
      "data": "0xa9059cbb00000000000000000000000011e1b586dd371471d0b52046ee3d4309a6c29c6c0000000000000000000000000000000000000000000000009087b2e881f47600"
    }
  ],
  "gasPriceCoef": 0,
  "gas": 90000,
  "origin": "0x2d7c8293b20344223668ed3fd88301381dc35ce0",
  "delegator": null,
  "nonce": "0xe83fd778763a5360",
  "dependsOn": null,
  "size": 193,
  "meta": {
    "blockID": "0x00bc614e285d68f8819b6dfdd729dad6fafbed9d2fdd65b57e4001a47d7f280c",
    "blockNumber": 12345678,
    "blockTimestamp": 1653978240
  }
}
```
* Successful Transaction Receipt: [GET /transactions/{transactionId}/receipt](https://mainnet.vechain.org/transactions/0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07/receipt)
```
{
  "gasUsed": 36582,
  "gasPayer": "0x2d7c8293b20344223668ed3fd88301381dc35ce0",
  "paid": "0x513a75a0fbbc000",
  "reward": "0x185e567d1852000",
  "reverted": false,
  "meta": {
    "blockID": "0x00bc614e285d68f8819b6dfdd729dad6fafbed9d2fdd65b57e4001a47d7f280c",
    "blockNumber": 12345678,
    "blockTimestamp": 1653978240,
    "txID": "0xfc99fe103fccbe61b3c042c1da3499b883d1b17fb40160ed1170ad5e63751e07",
    "txOrigin": "0x2d7c8293b20344223668ed3fd88301381dc35ce0"
  },
  "outputs": [
    {
      "contractAddress": null,
      "events": [
        {
          "address": "0x0000000000000000000000000000456e65726779",
          "topics": [
            "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
            "0x0000000000000000000000002d7c8293b20344223668ed3fd88301381dc35ce0",
            "0x00000000000000000000000011e1b586dd371471d0b52046ee3d4309a6c29c6c"
          ],
          "data": "0x0000000000000000000000000000000000000000000000009087b2e881f47600"
        }
      ],
      "transfers": []
    }
  ]
}
```
* Unsuccessful Transaction Receipt: [GET /transactions/{transactionId}/receipt](https://mainnet.vechain.org/transactions/0xae4a0ce2423c49cdb286cdde6691bdc77e9d06e2f5a4d0c3205c79af7d89bf7b/receipt)
```
{
  "gasUsed": 170831,
  "gasPayer": "0x9bb6c24707fc314a3b01324df2841cf61fec58a5",
  "paid": "0x17b522e4dc3f6000",
  "reward": "0x71cbdab0edfd000",
  "reverted": true,
  "meta": {
    "blockID": "0x01155656478ea00e7fd4f55a15cbb8124e504b7a874c0309b24dd90db2e5d500",
    "blockNumber": 18175574,
    "blockTimestamp": 1712283390,
    "txID": "0xae4a0ce2423c49cdb286cdde6691bdc77e9d06e2f5a4d0c3205c79af7d89bf7b",
    "txOrigin": "0x9bb6c24707fc314a3b01324df2841cf61fec58a5"
  },
  "outputs": []
}
```
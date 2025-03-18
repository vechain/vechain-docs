# Debug Reverted Transactions

## Failing to submit with `insufficient energy`

The message indicates that the gas payer does not have enough VTHO to cover the gas fees defined for the transaction.

Add VTHO to the transaction gas payer's VTHO balance or, if possible, reduce the amount of gas you are paying for the transaction.

## Transaction Reverts with `Out of Gas`

The message indicates that the transaction attempted execution but failed due to insufficient gas provided.

Increase the amount of gas you're willing to pay for the transaction. You can use `transactionUtils.intrinsicGas(clauses)` and add a buffer.

The buffer might become relevant because if your contract undergoes changes between the gas calculation and transaction execution, it can increase the gas cost for your transaction. If you approve a higher gas price, you will only be charged the actual costs.

## Decode Revert Reason

Once your transaction is submitted and it shows a "reverted" flag, debugging the reasons can be challenging. Having a contract that throws meaningful errors can greatly aid in debugging.

The initial step to identify the error is to run the transaction through a simulation to find the revert reason.

This can be accomplished by loading the original transaction and extracting data for the simulation:

```js
const transaction = await thor.transactions.getTransaction(txId)
const simulation = await thor.transactions.simulateTransaction(
  transaction.clauses,
  {
    revision: transaction.meta.blockID,
    gas: transaction.gas,
    caller: transaction.origin,
    gasPayer: transaction.delegator ?? transaction.origin,
    expiration: transaction.expiration,
    blockRef: transaction.blockRef,
  }
);
```

The simulation will return a result for each clause until the first clause fails. For successful simulations, the length of the simulation list will equal the number of clauses.

You can loop through the results to find the first clause that reverted:

```js
simulation.forEach((clause, clauseIndex) => {
  if (!clause.reverted) {
    return console.log(`Clause #${clauseIndex} was successful`);
  }

  console.log(`Clause #${clauseIndex} reverted (${clause.vmError})`);
});
```

The error is contained in the `data` attribute, which you can decode using your ABI, for example:

```js
import { ThorClient } from '@vechain/sdk-network';
import { coder } from '@vechain/sdk-core';

const contractInterface = coder.createInterface(['Error(string)']);

//.. simulate

simulation.forEach((clause, clauseIndex) => {
  if (!clause.reverted) {
    return console.log(`Clause #${clauseIndex} was successful`);
  }

  const revertReason = contractInterface.parseError(clause.data);

  console.log(`Clause #${clauseIndex} reverted with`);
  console.log(' VM Error:', clause.vmError);
  console.log(' Revert Reason:', revertReason.args);
});
```

The example interface `Error(string)` is typically used when throwing a regular error. It functions well in most standard situations.

### Example Snippet

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/transaction-debug?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

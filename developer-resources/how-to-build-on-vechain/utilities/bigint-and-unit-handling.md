# BigInt and Unit-Handling

Numbers in smart contracts are usually stored without decimals as big numbers, and a second variable contains information about the amount of decimals.

Some utility functions can help ease the handling of these numbers, especially with the `bigint` support now being natively available:

## Convert Token Balance to Human-Readable Version

For example, reading the balance of VTHO and turning it into a readable version:

```ts
import { ThorClient, Contract } from '@vechain/sdk-network';
const thor = ThorClient.at('https://mainnet.vechain.org');

const contract = new Contract('0x0000000000000000000000000000456e65726779', [
  'function balanceOf(address _owner) returns (uint256)',
  'function decimals() returns (uint256)',
]);

const [[balance], [decimals]] = await thor.contracts.executeMultipleClausesCall(
  [
    contract.clause.balanceOf('0x0000000000000000000000000000000000000000'),
    contract.clause.decimals(),
    
<strong>    contract.clause.setValue(123)
</strong>  ]
);
console.log(balance, decimals, '=>', unitsUtils.formatUnits(balance, decimals));
</code></pre>

Using `unitsUtils.formatUnits(number, decimals)`, the number is turned into a string with the decimal right where a human needs it.

## Convert Human Inputs to BigInts

When building user interfaces, numbers are entered as strings and need to be turned into BigInts for interaction with the blockchain.

`unitsUtils.parseUnits(string, decimals)` helps in that way. For example:

```ts
unitsUtils.parseUnits('5', 18)   // => turns into 5000000000000000000n
unitsUtils.parseUnits('0.1', 18) // => turns into 100000000000000000n
```

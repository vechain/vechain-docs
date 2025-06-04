# BigInt and Unit-Handling

Numbers in smart contracts are usually stored without decimals as big numbers, and a second variable contains information about the amount of decimals.

Some utility functions can help ease the handling of these numbers, especially with the `bigint` support now being natively available:

## Convert Token Balance to Human-Readable Version

For example, reading the balance of VTHO and turning it into a readable version:

```ts
// Example 1: multicall 
import { ThorClient, TESTNET_URL } from '@vechain/sdk-network';
import { ERC20_ABI} from '@vechain/sdk-core'

const thor = ThorClient.at(TESTNET_URL+'/');
const contract = thor.contracts.load('0x0000000000000000000000000000456e65726779', ERC20_ABI );

let clauses = [];

clauses.push(contract.clause.balanceOf('0x0000000000000000000000000000456e65726779'));
clauses.push(contract.clause.decimals());

const response = await thor.contracts.executeMultipleClausesCall(clauses);

console.log("Balance:", Number(response[0].result.plain)/(10**Number(response[1].result.plain)), "VTHO");

```

## Convert Human Inputs to BigInts

When building user interfaces, numbers are entered as strings and need to be turned into BigInts for interaction with the blockchain.

`unitsUtils.parseUnits(string, decimals)` helps in that way. For example:

```ts
unitsUtils.parseUnits('5', 18)   // => turns into 5000000000000000000n
unitsUtils.parseUnits('0.1', 18) // => turns into 100000000000000000n
```


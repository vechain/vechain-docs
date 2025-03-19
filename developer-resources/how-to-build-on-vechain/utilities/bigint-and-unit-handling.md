# BigInt and Unit-Handling

Numbers in smart contracts are usually stored without decimals as big numbers, and a second variable contains information about the amount of decimals.

Some utility functions can help ease the handling of these numbers, especially with the `bigint` support now being natively available:

## Convert Token Balance to Human-Readable Version

For example, reading the balance of VTHO and turning it into a readable version:

```ts
// Example 1: simulate multicall 
import { ThorClient, TESTNET_URL } from '@vechain/sdk-network';
import { ERC20_ABI} from '@vechain/sdk-core'

const thor = ThorClient.at(TESTNET_URL+'/');
const contract = thor.contracts.load('0x0000000000000000000000000000456e65726779', ERC20_ABI );

let clauses = [];

clauses.push(contract.clause.balanceOf('0x0000000000000000000000000000456e65726779'));
clauses.push(contract.clause.decimals());

const response = await thor.contracts.executeMultipleClausesCall(clauses);

console.log(response);

// Example 2: execute multicall (with signer)
import { ThorClient, TESTNET_URL, Contract, VeChainAbstractSigner , VeChainProvider, ProviderInternalBaseWallet } from '@vechain/sdk-network';
import { HexUInt , ERC20_ABI} from '@vechain/sdk-core'

const thor = ThorClient.at(TESTNET_URL+'/');
const contract = thor.contracts.load('0x0000000000000000000000000000456e65726779', ERC20_ABI );

const senderAccount = {
  privateKey:
      'f9fc826b63a35413541d92d2bfb6661128cd5075fcdca583446d20c59994ba26',
  address: '0x7a28e7361fd10f4f058f9fefc77544349ecff5d6'
};

let clauses = [];

clauses.push(contract.clause.balanceOf('0x0000000000000000000000000000456e65726779'));
clauses.push(contract.clause.decimals());

// Create the provider
const provider = new VeChainProvider(
  // Thor client used by the provider
  thor,
  // Wallets used by the provider
  new ProviderInternalBaseWallet([
      {
          privateKey: HexUInt.of(senderAccount.privateKey).bytes,
          address: senderAccount.address
      }
  ]),
  false
);

const signer = await provider.getSigner(senderAccount.address);

const response = await thor.contracts.executeMultipleClausesTransaction(clauses, signer);
console.log(response);

```


## Convert Human Inputs to BigInts

When building user interfaces, numbers are entered as strings and need to be turned into BigInts for interaction with the blockchain.

`unitsUtils.parseUnits(string, decimals)` helps in that way. For example:

```ts
unitsUtils.parseUnits('5', 18)   // => turns into 5000000000000000000n
unitsUtils.parseUnits('0.1', 18) // => turns into 100000000000000000n
```


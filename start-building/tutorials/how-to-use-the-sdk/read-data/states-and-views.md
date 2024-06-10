# States & Views

Smart Contracts have the ability to expose variables and functions for sharing their stored data publicly. In order to communicate with a contract, it is essential to have the interface definition, which can be retrieved either from a JSON file or from the function definition in the source code.

## Example Data

This example used below will utilize the VTHO contract, which manages Vechain's VTHO Token.

* Smart Contract Address: `0x0000000000000000000000000000456e65726779`
* The contract's source code can be found on GitHub at: [https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol](https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol)
* Its Application Binary Interface (ABI) is shared on b32, a repository that gathers publicly available interfaces for Vechain projects: [https://github.com/vechain/b32/blob/master/ABIs/energy.json](https://github.com/vechain/b32/blob/master/ABIs/energy.json)

## `executeCall(address, fragment, args, opts)`

Retrieving information is "calling" a function within a contract, which can be variables, view functions, and even functions that alter the state for simulation purposes.

`contracts.executeCall` is used to interact with smart contracts by providing: the contract's address as the first argument, the function fragment as the second argument, and optional function parameters as the third argument.

A fourth parameter provides the option to configure blockchain settings, such as specifying a historical revision or indicating the caller of a function.

### Without Parameters

For example, if you want to access a basic variable name from a contract, such as the name of the VTHO contract, you can utilize the code snippet below:

```js
const name = await thor.contracts.executeCall(
  '0x0000000000000000000000000000456e65726779',
  'name() returns (string)'
);
console.log('Name', name);
```

### With Parameters

When calling a function with parameters, the parameters should be passed as a list in the third argument. For instance, to check the balance of a specific address:

```js
const balanceNow = await thor.contracts.executeCall(
  '0x0000000000000000000000000000456e65726779',
  'balanceOf(address _owner) returns (uint256)',
  ['0x0000000000000000000000000000000000000000']
);
console.log('Balance Now', balanceNow);
```

### Historical Data

To retrieve data from a previous block, you can specify the block number or id by passing in a `revision` option:

```js
const balancePast = await thor.contracts.executeCall(
  '0x0000000000000000000000000000456e65726779',
  'balanceOf(address _owner) returns (uint256)',
  ['0x0000000000000000000000000000000000000000'],
  { revision: 12345678 }
);
console.log('Balance Past', balancePast);
```

### Simulate Transaction

If a function could change the state, it would require a transaction. To check the success of a transaction, you can invoke the function first and examine the output or handle any potential errors. For example, simulating a transfer that returns `true` if the caller has at least 1 VTHO:

```js
const transfer = await thor.contracts.executeCall(
  '0x0000000000000000000000000000456e65726779',
  'transfer(address _to, uint256 _amount) returns(bool success)',
  ['0x0000000000000000000000000000456e65726779', '1'],
  {
    caller: '0x0000000000000000000000000000000000000000',
  }
);
console.log('Transfer Test', transfer);
```

If the transaction encounters an error, the method call will also throw an error which needs to be handled appropriately.

### Example Project

{% embed url="https://stackblitz.com/edit/vechain-sdk-executecontractcall?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

## contracts.load(address, abi)

To simplify interaction a dynamic object can be created that can interact with passing less of the repeating arguments.

For example contracts.read.name() can load the name without the need to pass function signature, address and thor client every time.

### Create Contract Object

To create a contract object it needs to be created from the thor client:

```javascript
import { HttpClient, ThorClient } from '@vechain/sdk-network';
import { ErrorDecoder } from 'ethers-decode-error';
import abi from './energy.json' assert { type: 'json' };

const thor = new ThorClient(new HttpClient('https://mainnet.vechain.org'));
const vtho = thor.contracts.load(
  '0x0000000000000000000000000000456e65726779',
  abi
);

```

{% hint style="info" %}
The Contract-Loader always requires a JSON ABI Definition.

Fragments are not supported.
{% endhint %}

### Read Functions

Function calls are encapsulated within a sub-object named `read`. This enables calling the contract for variable content, viewing functions, or performing simple transaction simulations.&#x20;

```javascript
await vtho.read.name() // returns the name
await vtho.read.balanceOf(address) // returns balance of address
await vtho.read.transfer(recipient, amount) // simulates a transfer 
```

### Read Options

Custom parameters, such as `revision` or specifying the caller of a function call, can be set for all requests using `setContractReadOptions`.

```javascript
// read balance of an address
vtho.setContractReadOptions({ revision: 12345678 });
const balancePast = await vtho.read.balanceOf(
  '0x0000000000000000000000000000000000000000'
);
console.log('Balance Past', balancePast);
```

### Example Project

{% embed url="https://stackblitz.com/edit/vechain-sdk-contractloader-read?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

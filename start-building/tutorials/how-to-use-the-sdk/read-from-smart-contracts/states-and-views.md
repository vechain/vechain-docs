# States & Views

Smart Contracts have the ability to expose variables and functions for sharing their stored data publicly. In order to communicate with a contract, it is essential to have the interface definition, which can be retrieved either from a JSON file or from the function definition in the source code.

## Example Data

This example used below will utilize the VTHO contract, which manages Vechain's VTHO Token.

* Smart Contract Address: `0x0000000000000000000000000000456e65726779`
* The contract's source code can be found on GitHub at: [https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol](https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol)
* Its Application Binary Interface (ABI) is shared on b32, a repository that gathers publicly available interfaces for Vechain projects: [https://github.com/vechain/b32/blob/master/ABIs/energy.json](https://github.com/vechain/b32/blob/master/ABIs/energy.json)

## `executeContractCall(address, fragment, args, opts)`

Retrieving information is "calling" a function within a contract, which can be variables, view functions, and even functions that alter the state for simulation purposes.

`contracts.executeContractCall` is used to interact with smart contracts by providing: the contract's address as the first argument, the function fragment as the second argument, and optional function parameters as the third argument.

A fourth parameter provides the option to configure blockchain settings, such as specifying a historical revision or indicating the caller of a function.

### Without Parameters

For example, if you want to access a basic variable name from a contract, such as the name of the VTHO contract, you can utilize the code snippet below:

```js
const name = await thor.contracts.executeContractCall(
  '0x0000000000000000000000000000456e65726779',
  'name() returns (string)'
);
console.log('Name', name);
```

### With Parameters

When calling a function with parameters, the parameters should be passed as a list in the third argument. For instance, to check the balance of a specific address:

```js
const balanceNow = await thor.contracts.executeContractCall(
  '0x0000000000000000000000000000456e65726779',
  'balanceOf(address _owner) returns (uint256)',
  ['0x0000000000000000000000000000000000000000']
);
console.log('Balance Now', balanceNow);
```

### Historical Data

To retrieve data from a previous block, you can specify the block number or id by passing in a `revision` option:

```js
const balancePast = await thor.contracts.executeContractCall(
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
const transfer = await thor.contracts.executeContractCall(
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

## Example Project

{% embed url="https://stackblitz.com/edit/vechain-sdk-executecontractcall?embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

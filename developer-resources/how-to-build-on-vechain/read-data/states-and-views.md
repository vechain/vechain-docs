# States & Views

Smart Contracts have the ability to expose variables and functions for sharing their stored data publicly. In order to communicate with a contract, it is essential to have the interface definition, which can be retrieved either from a JSON file or from the function definition in the source code.

## Example Data

This example used below will utilize the VTHO contract, which manages VeChain's VTHO Token.

* Smart Contract Address: `0x0000000000000000000000000000456e65726779`
* The contract's source code can be found on GitHub at: [https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol](https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol)
* Its Application Binary Interface (ABI) is shared on b32, a repository that gathers publicly available interfaces for VeChain projects: [https://github.com/vechain/b32/blob/master/ABIs/energy.json](https://github.com/vechain/b32/blob/master/ABIs/energy.json)

## `executeCall(contractAddress, functionAbi, functionData, contractCallOptions?)`

Retrieving information is "calling" a function within a contract, which can be variables, view functions, and even functions that alter the state for simulation purposes.

`contracts.executeCall` is used to interact with smart contracts by providing: the contract's address as the first argument, the function ABI as the second argument and function data as the third argument.

A fourth parameter is optional and allows user to provide the options for executing a contract call within a blockchain environment.

### Without Parameters

To get the value stored for the variable `name` from the contract, the VTHO token name in this case, you can use the code below:

```js
const thor = ThorClient.at('https://mainnet.vechain.org');
// it is the ABI of the energy contract mentioned above
const contractABI = new ABIcontract ([
    {
        "constant": true,
        "inputs": [],
        "name": "name",
        "outputs": [
            {
                "name": "",
                "type": "string"
            }
        ],
        "payable": false,
        "stateMutability": "pure",
        "type": "function"
    },
    {
        "constant": false,
        "inputs": [
            {
                "name": "_spender",
                "type": "address"
            },
            {
                "name": "_value",
                "type": "uint256"
            }
        ],
        "name": "approve",
        "outputs": [
            {
                "name": "success",
                "type": "bool"
            }
        ],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [],
        "name": "totalSupply",
        "outputs": [
            {
                "name": "",
                "type": "uint256"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    },
    {
        "constant": false,
        "inputs": [
            {
                "name": "_from",
                "type": "address"
            },
            {
                "name": "_to",
                "type": "address"
            },
            {
                "name": "_amount",
                "type": "uint256"
            }
        ],
        "name": "transferFrom",
        "outputs": [
            {
                "name": "success",
                "type": "bool"
            }
        ],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [],
        "name": "decimals",
        "outputs": [
            {
                "name": "",
                "type": "uint8"
            }
        ],
        "payable": false,
        "stateMutability": "pure",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [
            {
                "name": "_owner",
                "type": "address"
            }
        ],
        "name": "balanceOf",
        "outputs": [
            {
                "name": "balance",
                "type": "uint256"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [],
        "name": "symbol",
        "outputs": [
            {
                "name": "",
                "type": "string"
            }
        ],
        "payable": false,
        "stateMutability": "pure",
        "type": "function"
    },
    {
        "constant": false,
        "inputs": [
            {
                "name": "_to",
                "type": "address"
            },
            {
                "name": "_amount",
                "type": "uint256"
            }
        ],
        "name": "transfer",
        "outputs": [
            {
                "name": "success",
                "type": "bool"
            }
        ],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "constant": false,
        "inputs": [
            {
                "name": "_from",
                "type": "address"
            },
            {
                "name": "_to",
                "type": "address"
            },
            {
                "name": "_amount",
                "type": "uint256"
            }
        ],
        "name": "move",
        "outputs": [
            {
                "name": "success",
                "type": "bool"
            }
        ],
        "payable": false,
        "stateMutability": "nonpayable",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [],
        "name": "totalBurned",
        "outputs": [
            {
                "name": "",
                "type": "uint256"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    },
    {
        "constant": true,
        "inputs": [
            {
                "name": "_owner",
                "type": "address"
            },
            {
                "name": "_spender",
                "type": "address"
            }
        ],
        "name": "allowance",
        "outputs": [
            {
                "name": "remaining",
                "type": "uint256"
            }
        ],
        "payable": false,
        "stateMutability": "view",
        "type": "function"
    },
    {
        "anonymous": false,
        "inputs": [
            {
                "indexed": true,
                "name": "_from",
                "type": "address"
            },
            {
                "indexed": true,
                "name": "_to",
                "type": "address"
            },
            {
                "indexed": false,
                "name": "_value",
                "type": "uint256"
            }
        ],
        "name": "Transfer",
        "type": "event"
    },
    {
        "anonymous": false,
        "inputs": [
            {
                "indexed": true,
                "name": "_owner",
                "type": "address"
            },
            {
                "indexed": true,
                "name": "_spender",
                "type": "address"
            },
            {
                "indexed": false,
                "name": "_value",
                "type": "uint256"
            }
        ],
        "name": "Approval",
        "type": "event"
    }
]);

const name = await thor.contracts.executeCall(
    '0x0000000000000000000000000000456e65726779', 
    contractABI.getFunction('name'), 
    []
);
console.log('Name', name.result.plain);
```

### With Parameters

When calling a function with parameters, the parameters should be passed as a list in the third argument. For instance, to check the balance of a specific address:

```js
const balanceNow = await thor.contracts.executeCall(
    '0x0000000000000000000000000000456e65726779', 
    contractABI.getFunction('balanceOf'), 
    ['0x0000000000000000000000000000000000000000']
);
console.log('Balance Now', balanceNow.result.plain / 1000000000000000000n);
```

### Historical Data

To retrieve data from a previous block, you can specify the block number or id by passing in a `revision` option:

```js
const balancePast = await thor.contracts.executeCall(
    '0x0000000000000000000000000000456e65726779', 
    contractABI.getFunction('balanceOf'), 
    ['0x0000000000000000000000000000000000000000'], 
    { revision: "12345678" }
);
console.log('Balance Past', balancePast.result.plain / 1000000000000000000n);
```

### Simulate Transaction

If a function could change the state, it would require a transaction. To check the success of a transaction, you can invoke the function first and examine the output or handle any potential errors. For example, simulating a transfer that returns `true` if the caller has at least 1 VTHO:

```js
const transfer = await thor.contracts.executeCall(
    '0x0000000000000000000000000000456e65726779', 
    contractABI.getFunction('transfer'), 
    ['0x0000000000000000000000000000456e65726779', '1'], 
    {
        caller: '0x0000000000000000000000000000000000000000',
    }
);
console.log('Transfer Test', transfer.result.plain);
```

If the transaction encounters an error, the method call will also throw an error which needs to be handled appropriately.

### Example Project



{% embed url="https://stackblitz.com/edit/vechain-energy-example-snippets-f5zzyjdv?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

## contracts.load(address, abi)

To simplify interaction a dynamic object can be created that can interact with passing less of the repeating arguments.

For example contracts.read.name() can load the name without the need to pass function signature, address and thor client every time.

### Create Contract Object

To create a contract object it needs to be created from the thor client:

```javascript
const thor = ThorClient.at('https://mainnet.vechain.org');

// contract ABI is same as in example above
const vtho = thor.contracts.load(
    '0x0000000000000000000000000000456e65726779',
    contractABI
);

```

{% hint style="info" %}
The Contract-Loader always requires a JSON ABI Definition.

Fragments are not supported.
{% endhint %}

### Read Functions

Function calls are encapsulated within a sub-object named `read`. This enables calling the contract for variable content, viewing functions, or performing simple transaction simulations.

```javascript
await vtho.read.name() // returns the name
await vtho.read.balanceOf(address) // returns balance of address
await vtho.read.transfer(recipient, amount) // simulates a transfer 
```

### Read Options

Custom parameters, such as `revision` or specifying the caller of a function call, can be set for all requests using `setContractReadOptions`.

```javascript
// read balance of an address
vtho.setContractReadOptions({ revision: "12345678" });
const balancePast = await vtho.read.balanceOf(
  '0x0000000000000000000000000000000000000000'
);
console.log('Balance Past', balancePast);
```

### Example Project

{% embed url="https://stackblitz.com/github/vechain-energy/example-snippets/tree/v1.0.0/sdk/read-contract.load?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

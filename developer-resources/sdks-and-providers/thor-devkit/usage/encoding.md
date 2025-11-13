---
description: Transaction and contract encoding
---

# Encoding

Thor DevKit extends its support to handle both Application Binary Interface (ABI) and Recursive Length Prefix (RLP) encoding.

## ABI

Thor DevKit provides functionality to interact with smart contracts on the VeChainThor blockchain using ABI's. An ABI is a standardised interface format that defines the method signatures, input parameters, and output types of smart contract functions. With Thor DevKit, developers can conveniently encode and decode data for interacting with smart contracts, making it easier to call contract functions and process their results.

```javascript
import { abi } from 'thor-devkit'

// Create a new function
const simpleAbiFunction = new abi.Function({
    "constant": false,
    "inputs": [
        {
            "name": "a1",
            "type": "uint256"
        },
        {
            "name": "a2",
            "type": "string"
        }
    ],
    "name": "f1",
    "outputs": [
        {
            "name": "r1",
            "type": "address"
        },
        {
            "name": "r2",
            "type": "bytes"
        }
    ],
    "payable": false,
    "stateMutability": "nonpayable",
    "type": "function"
})

// Encode function 
const data = simpleAbiFunction.encode(1, 'foo')
console.log(data)
// 0x1b00db7...
```

## RLP Encoding

RLP is a serialisation technique used on the VeChainThor blockchain. It is used to efficiently encode and decode data structures for storage and transmission on the blockchain. Thor DevKit includes dedicated methods for RLP encoding and decoding, enabling developers to handle data serialization and deserialization with ease.

By supporting ABI and RLP encoding handling, Thor DevKit equips developers with the necessary tools to interact with smart contracts and handle data efficiently on the VeChainThor blockchain. This further enhances the library's capabilities and contributes to the seamless development of decentralised applications on the platform.

```javascript
import { RLP } from 'thor-devkit'

// Define the profile for tx clause structure
const profile = {
    name: 'clause',
    kind: [
        { name: 'to', kind: new RLP.NullableFixedBlobKind(20) },
        { name: 'value', kind: new RLP.NumericKind(32) },
        { name: 'data', kind: new RLP.BlobKind() }
    ]
}

// Create clauses
const clause = {
    to: '0x7567d83b7b8d80addcb281a71d54fc7b3364ffed',
    value: 10,
    data: '0x'
}

// Instace RLP
const rlp = new RLP(profile)

// Encoding and Decoding
const data = rlp.encode(clause)
console.log(data.toString('hex'))
// d7947567d83b7b8d80addcb281a71d54fc7b3364ffed0a80

const obj = rlp.decode(data)
console.log(JSON.stringify(obj) === JSON.stringify(clause))
// `obj` should be identical to `clause`s -> true
```

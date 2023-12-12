# Web3-Providers-Connex

The web3-providers-connex library implements the JSON-RPC provider defined in [EIP-1193](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1193.md) for the VechainThor blockchain. The provider is compatible with [web3.js](https://github.com/ChainSafe/web3.js) and [ethers.js](https://github.com/ethers-io/ethers.js), allowing developers to use both libraries to interact with the VechainThor blockchain, via Connex.

{% hint style="info" %}
Available on GitHub [here](https://github.com/vechain/web3-providers-connex).
{% endhint %}

## Key Features

The web3-providers-connex library offers a wide range of functionalities related to the VechainThor blockchain and dApp development. Some of the key features include:

1. **web3.js support**: web3-providers-connex enables developers to interact with the VechainThor blockchain with the familiar web3.js library.
2. **ethers.js support**: web3-providers-connex enables developers to interact with the VechainThor blockchain with the familiar ethers.js library.
3. **Supports all of the key features of Connex**:
   1. **Blocks and node status**: The library enables developers to interact with and retrieve information about blocks on the VeChainThor blockchain. This includes accessing block data and querying the status of connected VeChain nodes.
   2. **Accounts**: Facilitates interactions with Externally Owned Accounts (EOAs), allowing developers to manage and transact with individual user accounts on the VeChainThor blockchain. This includes sending VET tokens and interacting with VTHO (VeThor) tokens.
   3. **Smart Contracts**: Developers can interact with and manage smart contracts deployed on the VeChainThor blockchain. This includes deploying smart contracts, invoking their functions, and retrieving contract data.
   4. **Transactions**: Create and broadcast transactions on the VeChainThor blockchain. Developers can initiate various transactions, such as token transfers, contract interactions, and asset management.
   5. **Certificates**: Manage certificates and certificate-related operations on the blockchain. Certificates are often used for identity verification and access control in dApps.
   6. **Queries**: Efficiently query the VechainThor blockchain. This includes querying transaction details, contract state, and other relevant blockchain information for dApp development.

## Online Functionality

web3-providers-connex serves as an "online" library, primarily used for dApp development and blockchain-related operations that can be performed online. For example, users can use web3-providers-connex to create, sign and broadcast transactions to the VechainThor blockchain network.

## Installation

This command will download and install the Connex provider package along with it's dependencies into your project.

```bash
npm install @vechain/web3-providers-connex
```

## Using EIP-1193 provider

### Checking account balance

```typescript
import { Provider } from '@vechain/web3-providers-connex'

// connexObj is an instance of Connex
const provider = new Provider({connex: connexObj})
const balance = await provider.request({ 
  method: 'eth_getBalance', 
  params: ['0x...'] 
})
```

### Obtaining a connex instance in Node.js

```typescript
import { Framework } from '@vechain/connex-framework'
import { Driver, SimpleNet, SimpleWallet } from '@vechain/connex-driver'

const net = new SimpleNet(url-to-thor-node)
const wallet = new SimpleWallet()
// import private key if needed
wallet.import('0x...')
const driver = await Driver.connect(net, wallet)
const connexObj = new Framework(driver)
```

### Sending VET

```typescript
const txId = await provider.request({
  method: 'eth_sendTransaction',
  params: [{ 
    from: '0x...', 
    to: '0x...', 
    value: '0x...' 
  }]
})
```

## Working with web3.js

```typescript
import { ProviderWeb3 } from '@vechain/web3-providers-connex'
import { Web3 } from 'web3' 

const provider = new ProviderWeb3({ connex: connexObj })
const web3 = new Web3(provider)
```

## Working with ethers.js

```typescript
import * as thor from '@vechain/web3-providers-connex'
import { ethers } from 'ethers'

const provider = thor.ethers.modifyProvider(
  new ethers.BrowserProvider(
    new thor.Provider({ 
      connex: connexObj,
      wallet: walletObj,	// MUST provide to call [getSigner] method 	 
    })
  )
)
```

## Obtaining a signer

```typescript
const signer = provider.getSigner(address)
```

## Deploying a contract

```typescript
const factory = thor.ethers.modifyFactory(
  new ethers.ContractFactory(abi, bin, signer)
)
const base = await factory.deploy(...args)
await base.waitForDeployment()

const contractAddress = await base.getAddress()
const contract = new ethers.Contract(contractAddress, abi, signer)
```

Methods `modifyProvider` and `modifyFactory` are used to patch the original code of [ethers.js](https://github.com/ethers-io/ethers.js) that is incompatible with the Thor protocol.

## Request at a particular block hight

APIs `eth_getBalance`, `eth_getCode`, `eth_getStorageAt` and `eth_call` allow users to specify a particular block height \[1]. To do that, we need to provide a `Net` object when creating a provider:

```typescript
import { SimpleNet } from '@vechain/connex-driver'
import * as thor from '@vechain/web3-providers-connex'
import { Web3 } from 'web3'
import { ethers } from 'ethers'

const provider = new thor.Provider({ 
  connex: connexObj,
  net: netObj
})

const web3 = new Web3(
  new thor.ProviderWeb3({ 
    connex: connexObj,
    net: netObj
  })
)

const providerEthers = thor.ethers.modifyProvider(
  new ethers.BrowserProvider(
    new thor.Provider({ 
      connex: connexObj,
      net: netObj
    })
  )
)
```

## Fee delegation

Fee delegation can be enabled by passing the delegator URL when constructing an instance of `Provider`/`ProviderWeb3`:

```typescript
import { Provider } from '@vechain/web3-providers-connex';

const provider = new Provider({
  connex: Obj,
  delegate: {
    url: url-to-delegator
  }
})
```

or calling `enableDelegate`:

```typescript
provider.enableDelegate({ url: url-to-delegator });
```

You can also disable fee delegation by

```typescript
provider.disableDelegate();
```

A delegator is a web service that co-signs and returns a signature for transactions it accepts. The gas fee would then be deducted from the delegator's account instead of the transaction sender's account. More information on fee delegation is available [fee-delegation](../../core-concepts/transactions/meta-transaction-features/fee-delegation/ "mention")

See [here](https://github.com/vechain/web3-providers-connex/blob/main/test/web3/feeDelegate.test.ts) for a demo.

## More Examples

More examples can be found [here](https://github.com/vechain/web3-providers-connex/tree/main/test).

## Supported APIs

**`eth_accounts`**

**`eth_blockNumber`**

**`eth_call`**

**`eth_estimateGas`**

**`eth_gasPrice`**

Returning `0x0`

**`eth_getBalance`**

**`eth_getBlockByNumber`**

**`eth_getBlockByHash`**

**`eth_chainId`**

**`eth_getCode`**

**`eth_getLogs`**

**`eth_getStorageAt`**

**`eth_getTransactionByHash`**

**`eth_getTransactionCount`**

Returning `0x0`

**`eth_getTransactionReceipt`**

**`eth_isSyncing`**

**`eth_requestAccounts`**

**`eth_sendRawTransaction`**

Requiring passing a `Net` object when constructing an instance of `Provider` or `ProviderWeb3`

**`eth_sendTransaction`**

**`eth_subscribe`, `eth_unsubscribe`**

Supported subscription type: `newHeads`, `logs`

**`evm_mine`**

**`net_version`**

Equivalent to `eth_chainId`

**`web3_clientVersion`**

Returning string `thor`

**`debug_traceTransaction`**

**`debug_traceCall`**

## Implementation Notes

1. Fields `blockHash` and `transactionHash` return the values of `blockId` and `transactionId` defined in the Thor protocol, respectively.
2. APIs `eth_estimateGas`, `eth_call`, `eth_getTransactionReceipt`, `debug_traceTransaction` and `debug_traceCall` only return information associated with the first clause in a transaction.[clauses-multi-task-transaction.md](../../core-concepts/transactions/meta-transaction-features/clauses-multi-task-transaction.md "mention")
3. Unsupported returning fields (all set to zero):

* `cumulativeGasUsed`
* `difficulty`
* `gasPrice`
* `logsBloom`
* `nonce`
* `sha3Uncles`
* `totalDifficulty`

4. For the default block number options \[1], only `latest` and `earliest` are supported



## License

web3-providers-connex is licensed under the GNU Lesser General Public License v3.0 (LGPL-3.0). The full text of the license can be found in the _LICENSE_ file included in the [repository](https://github.com/vechain/web3-providers-connex/blob/main/LICENSE).

The GNU Lesser General Public License v3.0 is an open-source license that grants users the freedom to use, modify, and distribute the software under certain conditions. It ensures that users have access to the source code, can make improvements, and distribute their modifications while also preserving the rights of the original authors.

For more details about the GNU Lesser General Public License v3.0, please visit the [GNU website](https://www.gnu.org/licenses/lgpl-3.0.html).

# Usage

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

A delegator is a web service that co-signs and returns a signature for transactions it accepts. The gas fee would then be deducted from the delegator's account instead of the transaction sender's account. More information on fee delegation is available [fee-delegation](../../../core-concepts/transactions/meta-transaction-features/fee-delegation/ "mention")

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
2. APIs `eth_estimateGas`, `eth_call`, `eth_getTransactionReceipt`, `debug_traceTransaction` and `debug_traceCall` only return information associated with the first clause in a transaction.[clauses-multi-task-transaction.md](../../../core-concepts/transactions/meta-transaction-features/clauses-multi-task-transaction.md "mention")
3. Unsupported returning fields (all set to zero):

* `cumulativeGasUsed`
* `difficulty`
* `gasPrice`
* `logsBloom`
* `nonce`
* `sha3Uncles`
* `totalDifficulty`

4. For the default block number options \[1], only `latest` and `earliest` are supported

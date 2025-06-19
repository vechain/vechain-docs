---
description: An introduction and overview of the VeChainThor blockchain transaction model.
---

# Transaction Model

VeChainThor defines a [transaction ](https://github.com/vechain/thor/blob/master/tx/transaction.go)in Golang as:

```go
// transaction.go

type Transaction struct {
	body body
}

type body struct {
	ChainTag              byte			
	BlockRef              uint64
	Expiration            uint32
	Clauses               []*Clause
	GasPriceCoef          uint8
	Gas                   uint64
	MaxFeePerGas          *big.Int
	MaxPriorityFeePerGas  *big.Int
	DependsOn             *thor.Bytes32 `rlp:"nil"`
	Nonce                 uint64
	Reserved              reserved
	Signature             []byte
}
```

Fields within the transaction `body`, $$\Omega$$ , are defined as:

* `ChainTag` – last byte of the genesis block ID which is used to identify a blockchain to prevent the cross-chain replay attack
* `BlockRef` - reference to a specific block
* `Expiration` – how long, in terms of the number of blocks, the transaction will be allowed to be mined in VeChainThor
* `Clauses` – an array of _Clause_ objects each of which contains fields `To`, `Value` and `Data` to enable a single transaction to carry multiple tasks issued by the transaction sender
* `GasPriceCoef` – coefficient used to calculate the gas price for legacy transactions
* `Gas` – maximum amount of gas allowed to pay for the transaction
* `MaxFeePerGas` - the absolute maximum to pay per unit of gas
* `MaxPriorityFeePerGas` - the absolute maximum tip to pay per unit of gas directly to the proposer
* `DependsOn` – ID of the transaction on which the current transaction depends
* `Nonce` – a random number set by the wallet / user
* `Reserved` - _reserved_ Object contains two fields: `Features` and `Unused`
  * `Feature` as 32-bit unsigned integer and default set as `0`.For Designated Gas Payer (VIP-191) must be set as `1`
  * `Unused` an array of reserved field for backward compatibility, it **MUST** be set as an empty array for now otherwise the transaction will be considered invalid
* `Signature` - transaction signature, $$sig = sign(hash(rlp\lbrace\Omega - sig \rbrace), sk))$$, where $$sk$$ is the transaction sender's private key

{% hint style="info" %}
Refer to the [meta-transaction-features](meta-transaction-features/ "mention") section for more detail on the unique aspects of transactions within the VeChainThor blockchain when compared to other blockchains.
{% endhint %}

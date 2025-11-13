---
description: An introduction and overview of the VeChainThor blockchain block model.
---

# Block Model

VeChainThor defines a [block ](https://github.com/vechain/thor/blob/master/block/block.go)in Golang as:

```go
// block.go

type Block struct {
	header *Header
	txs    tx.Transactions
}

type Header struct {
	body headerBody
}

type headerBody struct {
	ParentID     thor.Bytes32
	Timestamp    uint64
	GasLimit     uint64
	Beneficiary  thor.Address
	GasUsed      uint64
	BaseFee      *big.Int
	TotalScore   uint64
	TxsRoot      thor.Bytes32
	StateRoot    thor.Bytes32
	ReceiptsRoot thor.Bytes32
	Signature    []byte
	Alpha        []byte
	COM          bool
}

type Transactions []*Transaction

```

Fields within the `headerBody`, $$\Gamma$$, are defined as:

* `ParentID` - the ID of the parent block
* `Timestamp` - the block time
* `GasLimit` - the maximum amount of gas that all transactions inside the block are allowed to consume
* `Beneficiary` - the address assigned by the block generator to receive reward (in VTHO)
* `GasUsed` - the actual amount of gas used within the block
* `BaseFee` - the mandatory minimum fee required for including a transaction within the block
* `TotalScore` - the accumulated witness number of the chain branch headed by the block. See [#meta-transaction-features-3](../../introduction-to-vechain/about-the-vechain-blockchain/consensus-deep-dive.md#meta-transaction-features-3 "mention") for more detail.
* `TxsRoot` - root hash of the transaction in the payload
* `StateRoot` - root hash for the global state after applying changes in this block
* `ReceiptsRoot` - hash of the transaction receipts trie
* `Signature` - signature of block builder
* `Alpha` - an input into the Verifiable Random Function (VRF)
* `COM` - a boolean indicating whether the packer votes commit

The block ID (`thor.Bytes32`) can be computed as:

$$BlkID = h \circ (hash(\Gamma - sig )[4:]$$

where $$h$$ is the block number stored as a `uint32` and $$[4:]$$ the operation that discards the first four bytes.

---
description: >-
  A native approach to scale transaction throughput on the VeChainThor
  blockchain.
---

# Clauses (Multi-Task Transaction)

## Introduction <a href="#clauses" id="clauses"></a>

Most blockchain transactions models are limited to one payload and one recipient per transaction. The VeChainThor blockchain transaction model contains a native scaling solution called clauses which allows for the transfer of multiple payloads to different recipients.

## Clauses <a href="#clauses" id="clauses"></a>

Clauses are not transactions, but they do perform a similar function which is to deliver a payload on the VeChainThor blockchain. Clauses can be considered as an on-chain scaling mechanism which allows a user to send multiple payloads to different recipients in a single transaction. The `Clause` structure is defined in Golang as follows:

```go
type Clause struct {
	body clauseBody
}

type clauseBody struct {
	To    *thor.Address `rlp:"nil"`
	Value *big.Int
	Data  []byte
}
```

The three fields of a clause are:

* `To` – recipient’s address;
* `Value` – amount to be transferred to the recipient;
* `Data` – input data.

We then define `Clauses` as a `Clause` array in the transaction model to make it possible for a transaction to contain multiple tasks.

## Clause Attributes

Clauses have two interesting characteristics:

* Since clauses are included in a single transaction, their executions can be considered as atomic, meaning that, either they all succeed, or all fail.
* Clauses are processed one by one in the exact order defined in `Clauses`.

## Conclusion

Clauses are a unique feature to the VeChainThor blockchain and allows for a transaction to deliver multiple payloads to different recipients. Clauses are a form of on-chain scaling which allows for transaction throughput on the VeChainThor blockchain. When measuring the overall activity of the VeChainThor blockchain we must include clauses in the measurement.

{% hint style="info" %}
This [article](https://mirei83.medium.com/howto-vechain-blockchain-part-4-8c1e363da00f) provides additional information and a demonstration of clauses on the VeChainThor blockchain.
{% endhint %}

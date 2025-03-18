---
description: Enforce a transaction order on the VeChainThor blockchain.
---

# Transaction Dependency

## Introduction

Set dependencies on your transactions to ensure the execution order meets your business needs. Transactions that specify a dependency with the`DependOn` field in the transaction model will not be executed until the required transaction is processed.

## DependsOn <a href="#dependson" id="dependson"></a>

`DependsOn` stores the ID of the transaction on which the current transaction depends. In other words, the current transaction cannot be processed without the success of the transaction referred by `DependsOn`. Here by “success”, we mean that the referred transaction has been executed without state reversion.

## Implementation

The validation logic below ensures that the `DependsOn` field of a transaction is enforced when validating transactions within a block (see function verifyBlock in `$THORDIR/consensus/validator.go`).

```go
// check depended tx 
if dep := tx.DependsOn(); dep != nil { 
  found, reverted, err := findTx(*dep) 
  if err != nil { 
    return nil, nil, err 
  } 
  if !found { 
    return nil, nil, consensusError("tx dep broken") 
  } 
  if reverted { 
    return nil, nil, consensusError("tx dep reverted") 
  } 
}
```

Now let us have a close look at the code. According to its definition, `DependsOn` is a pointer pointing to the ID of the transaction it depends on. The first thing the code does is to get the value of the current transaction's `DependsOn` value via `dep := tx.DependsOn()`. If the field is set, it goes to check the status of the referred transaction using its $$TxID$$ through `found, reverted, err := findTx(*dep)`. The rest of the code checks whether the transaction exists and then whether it's been reverted. It rejects the current transaction if either check fails.

{% hint style="info" %}
This [article](https://peter-zhou.medium.com/what-you-might-not-know-about-vechainthor-yet-part-ii-forcible-transaction-dependency-ac3e98c4c955) provides additional information and a demonstration of `DependsOn` on the VeChainThor blockchain.
{% endhint %}

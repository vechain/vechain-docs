---
description: A unique transaction id for each transaction on the VeChainThor blockchain.
---

# Transaction Uniqueness

## Introduction

Every blockchain must have a way to uniquely identify each transaction otherwise it would be vulnerable to a transaction replay attack. For an unspent transaction output (UTXO) based blockchain like Bitcoin, transactions are linked and can be uniquely identified and verified by the associated spending history. However, such uniqueness no longer holds for an account-based blockchain like VeChain. For account-based blockchains we need to inject additional information into transactions to make them uniquely identifiable.

## VeChain's Approach to Transaction Uniqueness

In the VeChainThor blockchain every transaction has a unique transaction ID, $$TxID$$, which is calculated as:

$$TxID = hash(hash(rlp\lbrace\Omega - sig \rbrace)), signer\_address)$$

* $$\Omega$$ - represents a set that contains all fields within the transaction body.
* $$sig$$ - refers to the signature field in the transaction body.
* $$rlp$$ - recursive length prefix (RLP) encoding function.
* $$signer\_address$$ - refers to the sender's address.

The first element that contributes to transaction uniqueness is the presence of the `Nonce` within the transaction body, which is denoted by $$\Omega$$ in the formula above. The transaction `Nonce` is a 64-bit unsigned integer that is determined by the transaction sender.

The second element that contributes to transaction uniqueness is the use of hash functions. A hash function is any function that can be used to convert data of any size to a fixed size. The VeChainThor blockchain uses the blake2b hash function for hashing transaction data. So given a single transaction two hashes are computed. The first hash is of the RLP of the encoded transaction data without the signature, denoted by $$hash(rlp\lbrace\Omega - sig \rbrace)$$. The second hash takes the output of the previous hash concatenated with the sender's account address, $$signer\_address$$. The result of this second hash function is 256-bits long and is used as the $$TxID$$ which uniquely identifies the given transaction on the VeChainThor blockchain. Note that the calculation of the $$TxID$$ does not require a private key to sign the transaction.

When validating a given transaction, VeChainThor computes the $$TxID$$ and checks whether it has been used before. For any two transactions, so long as both transactions have a field in $$\Omega - sig$$ with different values, their transaction IDs would be different. The first element that we introduced which contributes to transaction uniqueness, the `Nonce`, contributes to the transaction body, $$\Omega$$, being different for each transaction.

## Comparison to Ethereum

Ethereum's approach to transaction uniqueness is to add the `AccountNonce` field to each transaction and set a rule that a pending transaction can only be processed when its `AccountNonce` value equals the latest `Nonce` value of the account that sends the transaction. Where the `Nonce` value is the number of transactions the account has sent so far. So in Ethereum a transaction is uniquely identifiable by combining the `AccountNonce` and the sender's account address.

The major downside of this approach is the limitation it places on the sender. Within this design transactions sent from the same account are forced to adhere to a transaction order based on the `Nonce` value of the transaction. An account with multiple transactions will have only one transaction processed at a time, the transaction which has a `Nonce` value the same as the `AccountNonce`. All other transactions sent by this account will be in a pending state waiting until the transaction `Nonce` equals the `AccountNonce`. Additionally, when a user has multiple pending transactions within an account and wants to send a new transaction, the user runs the risk of having the new transaction stuck in the transaction pool if any of the pending transactions fail. Overall, this is a poor user experience with the user occasionally having to resubmit transactions and overwrite the transaction `Nonce` to "unblock" their account.

## Conclusion

The Ethereum approach to transaction uniqueness has introduced a restriction on the Ethereum blockchain in the form of synchronous transaction processing, for transactions sent from a single account. The same restriction does not apply to the VeChainThor blockchain and transaction processing is asynchronous, for transactions sent from a single account.

{% hint style="info" %}
This [article](https://medium.com/vechain-foundation/what-you-might-not-know-about-vechainthor-yet-part-i-transaction-uniqueness-7a90146f2ace) provides additional information and a demonstration of transaction uniqueness on the VeChainThor blockchain.
{% endhint %}

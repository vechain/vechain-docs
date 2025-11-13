---
description: Overview of transaction features.
---

# Meta Transaction Features

Meta-transaction features native to the VeChainThor blockchain network make the development more user-friendly for enterprise adoption.

* **Transaction uniqueness:** Every blockchain must have a way to uniquely identify each transaction otherwise it would be vulnerable to a transaction replay attack. VeChain has implemented a novel approach to transaction uniqueness.
* **Controllable transaction lifecycle:** With the BlockRef and Expiration fields within the transaction model, users can set the time when a transaction is processed or expired if it has not yet been included in a block.
* **Clauses (Multi-Task Transaction):** Clauses are an additional data structure within the VeChainThor transaction model which enables a transaction to carry multiple payloads within a single transaction.
* **Fee delegation:** VeChain supports two methods for implementing fee delegation Multi-party payment (MPP) and VIP-191 Designated gas payer both of which offer flexible transaction fee delegation schemes.
* **Transaction dependency:** Set dependencies on a transaction to ensure the execution order meets the business need, transactions that specify a dependency will not be executed until the required transaction is processed.

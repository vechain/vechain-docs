---
description: >-
  The core infrastructure component that packages UserOperations into
  transactions.
---

# Bundler

## Overview

A Bundler plays a crucial role in the account abstraction architecture. Its primary responsibility is to collect these UserOperations from a public mempool, bundle them together, and pass them to the EntryPoint contract for execution.

The `EntryPoint contract` serves as a "global trusted singleton," meaning it is a single, universally trusted smart contract within the blockchain ecosystem.  In reality it's not like that, in a public blockchain anyone can create and promote its EP, do your own research and trust the EP you can find on trusted websites only.
This contract handles incoming transactions, validates them, and manages the execution of UserOperations. The Bundler acts as the intermediary between users and the EntryPoint contract, ensuring UserOperations are properly packaged and processed.

Unlike `Paymaster` or `Account` contract entities, which require individual smart contracts for each instance, the Bundler does not have its own smart contract. Instead, the Bundler uses an externally owned account (EOA) to execute on-chain transactions. This design simplifies its operation while maintaining its critical role in the system.

## Role

The Bundler’s role in the account abstraction system is analogous to that of a miner or validator in traditional blockchain networks. It performs the following functions:

* Monitoring and Aggregating: Continuously scans the public mempool for UserOperations submitted by users.
* Packaging Transactions: Groups multiple UserOperations into a single transaction to optimize execution.
* Submitting to EntryPoint: Passes the packaged transactions to the EntryPoint contract, ensuring they are executed in a reliable and timely manner.
* Compensation: Receives rewards for successfully executing UserOperations. These rewards are paid by users as fees within the bundled transactions.

To perform these functions, a Bundler must:

* Remain online consistently to monitor the mempool.
* Maintain sufficient funds in its EOA to cover the cost of gas fees required for executing transactions.

## Security and Decentralization

The decentralized nature of Bundlers contributes to the robustness and security of the account abstraction ecosystem. By allowing multiple independent Bundlers to operate, the system ensures:

* Fault Tolerance: No single point of failure.
* Fairness: Competition among Bundlers prevents monopolization.
* Reliability: Ensures continuous availability of services for UserOperation execution.



## Implementation

Several Bundler implementations are available, with the most notable being the [Infinitism Bundler](https://github.com/eth-infinitism/bundler). This implementation was developed by the team behind the EIP-4337 proposal and is widely regarded as the standard for Bundler operations. It provides:

* Open-Source Flexibility: Developers can adapt and customize the implementation for specific use cases.
* Community Support: Backed by a community of contributors improving and maintaining the codebase.

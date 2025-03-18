---
description: Introduction to what a block represents and what block finality is.
---

# Blocks

## What is a block in a blockchain?

A block is a data structure that contains a set of transactions and other relevant information, linked together in a chain with preceding blocks through cryptographic hashes, forming the basis of a secure, transparent, and immutable blockchain network. A simple analogy would be to think of a blockchain as a notebook, where a transaction is a single line on a page of the notebook, think of a block as a page.

## How fast, on average, are blocks produced in the VeChain blockchain?

The VeChainThor blockchain is not only energy efficient to operate, it is also very fast. Blocks are created, on average, every ten seconds. The PoA consensus mechanism ensures that the blockchain is capable of producing blocks in a very efficient manner.

## What is block finality and how does it work?

Blockchains usually achieve probabilistic finality, meaning that the probability of a transaction being reversed decreases as more blocks are added to the network. With the introduction of [VIP-220](https://github.com/vechain/VIPs/blob/master/vips/VIP-220.md), VeChainThor's block finality mechanism grants qualified blocks an absolute safety guarantee. Once a block acquires it's finality, the consensus assures it cannot be modified, replaced or removed from the public ledger, even when the network encounters extremely asynchronous situations, such as being subject to large-scale network partitioning.

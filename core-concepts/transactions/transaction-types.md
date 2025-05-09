---
description: An introduction and overview of the VeChainThor transaction types.
---

# Transaction Types

With the introduction of typed transactions, see [VIP-252](https://github.com/vechain/VIPs/blob/master/vips/VIP-252.md), the VeChainThor blockchain has become more extensible and forward compatible by enabling support for the introduction of new transaction types while ensuring backward compatibility with existing transactions. Each transaction is encapspulated in an envelope consisting of a single byte type identifier which specifics the transaction type and a payload of varying size which contains the serialized transaction data specific to the type.

## Dynamic Fee Transactions

Transactions with a type `0x51` are dynamic fee transactions that are introduced with [VIP-251](https://github.com/vechain/VIPs/blob/master/vips/VIP-251.md). The dynamic fee transaction model introduces a fluctuating base fee that is burned and a user-set priority fee that is paid directly to the proposer. This transaction model enhances network security and user experience by transitioning from a fixed-fee model to a dynamic fee model, adjusting fees based on network congestion.

## Legacy Transactions

Transactions with a starting byte in the range [`0x7f`, `0xfe`] are considered legacy transactions that use the transaction format that existed before typed transactions were introduced with [VIP-252](https://github.com/vechain/VIPs/blob/master/vips/VIP-252.md). This transaction model uses a fixed-fee model.

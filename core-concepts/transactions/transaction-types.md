---
description: An introduction and overview of the VeChainThor transaction types.
---

# Transaction Types

With the introduction of typed transactions, see [VIP-252](https://github.com/vechain/VIPs/blob/master/vips/VIP-252.md), the VeChainThor blockchain has become more extensible and forward compatible by enabling support for the introduction of new transaction types while ensuring backward compatibility with existing transactions.

### Legacy Transactions

Transactions with a type [`0xc0`, `0xfe`] are legacy transactions that use the transaction format that existed before typed transactions were introduced with [VIP-252](https://github.com/vechain/VIPs/blob/master/vips/VIP-252.md).

### Dynamic Fee Transactions

Transactions with a type `0x51` are dynamic fee transactions that are introduced with [VIP-251](https://github.com/vechain/VIPs/blob/master/vips/VIP-251.md). The dynamic fee transaction model introduces a fluctuating base fee that is burned and a user-set priority fee that is paid directly to the proposer. This transaction model enhances network security and user experience by transitioning from a fixed-fee model to a dynamic fee model, adjusting fees based on network congestion.

Dynamic Fee Transactions don't specify `gasPrice` and instead use an in-protocol dynamically changing `baseFee` per gas. At each block, the base fee per gas is adjusted to address network congestion as measured by a gas target, see [VIP-251](https://github.com/vechain/VIPs/blob/master/vips/VIP-251.md) for more details. Dynamic Fee Transactions include a `maxPriorityFeePerGas` which specifices the maximum fee that a user is willing to pay per gas above the base fee in order to get their transaction prioritized; and a `maxFeePerGas` which specifies the absolute maximum a user is willing to pay per unit of gas, this is the sum of the `baseFee` and the `maxPriorityFeePerGas`.

A Dynamic Fee Transaction always pays the base fee of the block it's included in, and it pays a priority fee as priced by `maxPriorityFeePerGas` or if the base fee per gas plus `maxPriorityFeePerGas` exceeds `maxFeePerGas` it pays a priority fee as priced by `maxFeePerGas` minus the base fee per gas. The base fee is burned, and the priority fee is paid to the miner that included the transaction. A transaction's priority fee per gas incentivizes validators to include the transaction over other transactions with lower priority fees per gas.

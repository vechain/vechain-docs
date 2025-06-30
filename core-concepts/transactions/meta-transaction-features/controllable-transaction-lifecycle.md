---
description: Configure your transaction lifecycle on the VeChainThor blockchain.
---

# Controllable Transaction Lifecycle

## Introduction

Configure your transaction, which has not yet been included in a block, to be processed or expire at a set time by using the `BlockRef` and `Expiration` fields on the transaction model.

## BlockRef <a href="#blockref" id="blockref"></a>

`BlockRef` stores the reference to a particular block whose next block is the earliest block the current transaction can be included. In particular, the first four bytes of `BlockRef` contain the block height, while the second four bytes can be used to prove that the referred block is known before the transaction is assembled. If that is the case, the value of `BlockRef` should match the first eight bytes of the ID of the block at the required height.

## Expiration <a href="#expiration" id="expiration"></a>

`Expiration` stores a number that can be used, together with `BlockRef`, to specify when the transaction expires. Specifically, the sum of `Expiration` and the first four bytes of `BlockRef` defines the height of the last block that the transaction can be included.

---
description: The math behind gas fee calculation on the VechainThor blockchain.
---

# Transaction Calculation

## What is gas? <a href="#intrinsic-gas-calculation" id="intrinsic-gas-calculation"></a>

Blockchain networks often refer to transaction fees as gas. Gas refers to the unit that measures the amount of computation effort required to execute operations on the blockchain network. This is a fee that is paid by the transaction sender and received by the blockchain network validator.

## Intrinsic Gas Calculation <a href="#intrinsic-gas-calculation" id="intrinsic-gas-calculation"></a>

The VechainThor blockchain transaction model is capable of containing clauses which allows a single transaction to carry out multiple tasks. Therefore, the total gas cost of the transaction needs to include all the clauses gas costs in the transaction.

The total gas, $$g_{total}$$, required for a transaction can be computed as:

$$g_{total} = g0 + \sum_i(g_{type}^i+g_{data}^i+g_{vm}^i)$$

* where $$g_0 = 5,000$$
* There are two types of $$g_{type}$$
  * Regular transaction : 16,000
  * Contract creation : 48,000
* $$g_{data}^i = 4 \cdot n_z^i + 68 \cdot n_{nz}^i$$
  * $$n_z^i$$ is the number of bytes equal to zero within the data in the $$i^{th}$$ clause and $$n_{nz}^i$$ the number of bytes not equal to zero
* $$g_{vm}^i$$ is the gas cost returned by the virtual machine for executing the $$i^{th}$$ clause.

## Proof of Work <a href="#proof-of-work" id="proof-of-work"></a>

The VechainThor blockchain allows for transaction-level proof of work (PoW) and converts the proved work into extra gas price that will be used by the system to generate more reward to the block generator, the Authority Masternode, that validates the transaction. In other words, users can utilize their local computational power to make their transactions more likely to be included in a new block.

In particular, the computational work can be proved through fields `Nonce` and `BlockRef` in the transaction model. Let $$n$$ and $$g$$ represent the values of the transaction fields `Nonce` and `Gas`, respectively. We use $$b$$ to denote the number of the block indexed by transaction field `BlockRef` and $$h$$ the number of the block that includes the transaction. Let $$\Omega$$ denote the transaction without fields `Nonce` and `Signature`, $$S$$ the transaction sender's account address, $$P$$ the base gas price, $$H$$ the hash function and $$E$$ the recursive length prefix (RLP) encoding function.

The PoW, $$w$$, is defined as:

$$w = min(2^{64}-1, \frac {{2^{256}-1}}{H(H(E(\Omega \parallel S))\parallel n)})$$

The extra gas price, $$\Delta$$, is computed as:

$$\Delta P = P_0(\frac1{g}min[g,\frac w{10^3}(\frac 1{1.04})^\frac {h-1}{3600\cdot24\cdot3}])$$

with the following constraint

$$\mid h - h_0 \mid \leq 30$$

The VTHO reward for packing the transaction into a new block is computed as:

$$r = \frac3{10}g^*(P_0(1+\phi) + \Delta P)$$

where $$\phi \in [0,1]$$ is the gas price coefficient and $$g^*$$ the actual amount of gas used for executing the transaction.

From the above equations, we know that

1. Since $$h_0$$ is a valid block number, `BlockRef` must refer to an existing block, that is, it's value must equal the first four bytes of an existing block ID;
2. The transaction must be packed into a block within the period of 30 blocks after block $$b$$, or otherwise, the PoW would not be recognized by the system;
3. The extra gas price $$\Delta P$$ can not be greater than base gas price P.

## Total Gas Price <a href="#total-gas-price" id="total-gas-price"></a>

The total gas price for the transaction sender is computed as:

$$g^{total} = g^{base} + g^{base} \frac\phi{255}$$

and the total price for block generators as

$$g^{total} = g^{base} + g^{base} \frac\phi{255} + \Delta P$$

Where $$g^{base}$$ is the gas used by the transaction and $$\phi$$ is the value of field `GasPriceCoef`(a value between **0-255**) and $$\Delta P$$ the extra gas price converted from the proven local computational work.

It can be seen that the gas price used to calculate the transaction cost depends solely on the input gas-price coefficient while the reward for packing the transaction into a block varies due to the transaction-level proof-of-work mechanism.

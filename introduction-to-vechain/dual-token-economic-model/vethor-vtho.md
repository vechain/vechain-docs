---
description: Understanding VeChain's transaction/gas token, VTHO
---

# VeThor Token (VTHO)

<table><thead><tr><th width="258.27956989247315">VTHO Characteristics</th><th>Details</th></tr></thead><tbody><tr><td>Type</td><td><a href="https://github.com/vechain/VIPs/blob/master/vips/VIP-180.md">VIP180</a></td></tr><tr><td>Token contract address</td><td>0x0000000000000000000000000000456E65726779</td></tr><tr><td>Precision</td><td>18 decimal places</td></tr><tr><td>Supply</td><td>VTHO (also known as _energy_) is used to pay for a transfer or for executing a smart contract transaction on the VeChainThor blockchain.</td></tr><tr><td>Dynamic behaviour</td><td>VTHO is subject to the rules of a fee market, the _BaseFee_ of each transaction fee paid is burned and the remaining priority fee is rewarded to the Validator which has proposed the block.</td></tr></tbody></table>

## VIP180: VeChain's Fungible Token Standard

VeChain had implemented an improvement proposal defining a new fungible token standard, VIP180. It was a superset of Ethereum's ERC20 standard, now superseded. All VIP180 are compatible with the most used ERC20 fungible token standard across blockchains. VTHO, as a VIP180 token, powers the VeChainThor blockchain by:

* Serving as the fee for transactions and smart contract execution
* Rewarding Validators and Delegators for block production and network maintenance

## VTHO Supply Dynamics

Unlike VET, VTHO doesn't have a fixed maximum supply. Its supply is governed by [VIP-251](https://github.com/vechain/VIPs/blob/master/vips/VIP-251.md) 
a dynamic fee mechanism, inspired by Ethereum's EIP-1559. It introduces a fluctuating base fee set by the protocol, 
which is the minimum you have to pay for your transaction to be considered valid, and a priority fee a tip that you add 
to the base fee to make your transaction attractive to validators:

* Generation rate (pre Hayabusa fork): new VTHO is generated at every block by holding VET
* Generation rate: since the Hayabusa hardfork, new VTHO is generated at every block and it is a function of Total VET being locked
* Block rewards: VTHO is used for transaction fees which, since the Galactica hardfork, is split in two parts
  * Base fee - which gets burned
  * Priority fee - that goes to the Validator who proposed the block

This dynamic supply model allows VeChain to adapt to network demand and maintain economic stability.

## The Purpose of VTHO Burning

VTHO burning serves several crucial functions:

* **Supply Control**: Helps regulate the circulating supply of VTHO
* **Value Stability**: Aims to maintain a stable VTHO value for predictable transaction costs
* **Flexibility**: Allows VeChain to adjust parameters based on network adoption and demand

## Earning VTHO

In a Delegated Proof of Stake (DPoS) consensus, every VET staked does contribute in keeping the network secure and those who do it are eligible to VTHO generation.
Before Hayabusa, every holder was generating VTHO just by holding VET. Incentive was diluted, and it was proven to provide a very weak incentive for the validators (responsible for keeping the network secure).
How to start earning:
To make the first step to start accumulating VTHO reward you can either:
- become a **delegator**: buying a StarGate NFTs and delegating it to a validator in StarGate.
- become a **validator**: running the node infrastructure to propose blocks and staking 25 M VET.
  More about staking can be found in the StarGate docs:

https://docs.stargate.vechain.org/hayabusa

## VTHO generation formula

VTHO is generated for each block produced, the amount of VTHO generated is a function of total VET staked in the network.
Mathematically it can be described with formula:

$$VTHO_{gen} = 1200 \cdot 64 \cdot \sqrt{VET_{staked}}$$

Where $$VTHO_{gen}$$ denotes the amount of VTHO generated per year. The constants: $$1200$$ and $$64$$ are scaling factors 
that determine the base generation rate, and: $$VET_{staked}$$ 

represents the total amount of VET staked across the network, by both validators and delegators at the point of block production. 

The square root function ensures that VTHO generation scales sub-linearly with the amount of staked VET, meaning that as 
more VET is staked, the rate of VTHO generation per additional staked VET decreases. This design helps maintain economic 
balance by preventing excessive VTHO inflation while still rewarding network participation through staking.

An example would be, if the total amount of VET staked in the network is 2.525 billion VET, the network would generate 
approximately 3.86 billion VTHO annually. This dynamic model, introduced with the Hayabusa hardfork, replaces the previous 
linear generation model where VET holders automatically generated VTHO at a fixed rate, and instead ties VTHO generation 
directly to active staking participation.

## VTHO transaction cost formula

On the other hand, for each transaction, a transaction fee must be paid to pay for the computation on the network. Mathematically, we can write it as:

$$E_{con} = p \cdot G$$

Where $$E_{con}$$ is the price in VTHO for performing a transaction. $$G$$ denotes the amount of gas required to process the transaction and $$p$$ the gas price in VTHO, which is a constant equal to $$1 \cdot 10^{-5}$$. An example would be, if an individual were performing a transaction costing 21k gas, they would have to pay 0.21 VTHO.

The gas price $$p$$ can vary in the range $$[p^{base}, 2 \cdot p^{base}]$$ where $$p^{base}$$ is a parameter that can be adjusted according to the market supply and demand of VTHO. Currently, we set $$p^{base} = 1 \cdot 10^{-5}$$.

This dual-token model, with staked VET generating VTHO and VTHO powering transactions, creates a flexible, scalable economic system for the VeChainThor blockchain. It allows for transaction cost stability while maintaining the potential for VET value appreciation, making it attractive for both enterprise use and individual investment.

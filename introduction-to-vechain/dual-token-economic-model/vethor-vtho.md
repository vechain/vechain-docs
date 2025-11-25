---
description: Understanding VeChain's transaction/gas token, VTHO
---

# VeThor Token (VTHO)

<table><thead><tr><th width="258.27956989247315">VTHO Characteristics</th><th>Details</th></tr></thead><tbody><tr><td>Type</td><td><a href="https://github.com/vechain/VIPs/blob/master/vips/VIP-180.md">VIP180</a></td></tr><tr><td>Token contract address</td><td>0x0000000000000000000000000000456E65726779</td></tr><tr><td>Precision</td><td>18 decimal places</td></tr><tr><td>Supply</td><td>VTHO is the energy or the cost of carrying out the payment and smart contract transactions on the VeChainThor blockchain.</td></tr><tr><td>Consumption</td><td>Base fee of the transaction fee paid in VTHO in each block is burned and the remaining priority fee is rewarded to the Validator Masternode which produces the block.</td></tr></tbody></table>

## VIP180: VeChain's Fungible Token Standard

VeChain had implemented an improvement proposal defining a new fungible token standard, VIP180. It was a superset of Ethereum's ERC20 standard, now superseded. All VIP180 are compatible with the most used ERC20 fungible token standard across blockchains. VTHO, as a VIP180 token, powers the VeChainThor blockchain by:

* Serving as the fee for transactions and smart contract execution
* Rewarding Authority Masternodes for block production and network maintenance

## VTHO Supply Dynamics

Unlike VET, VTHO doesn't have a fixed maximum supply. Its supply is governed by:

* Generation rate (pre Hayabusa fork): new VTHO is generated at every block by holding VET
* Generation rate (post Hayabusa fork): new VTHO is generated at every block production and it is a function of Total VET being locked
* Consumption (as of Galactica fork): VTHO is used for transaction fees, which is split in two parts
  * Base fee gets burned
  * Priority fee goes to the Validator Masternode who proposed the block as reward

This dynamic supply model allows VeChain to adapt to network demand and maintain economic stability.

## The Purpose of VTHO Burning

VTHO burning serves several crucial functions:

* **Supply Control**: Helps regulate the circulating supply of VTHO
* **Value Stability**: Aims to maintain a stable VTHO value for predictable transaction costs
* **Flexibility**: Allows VeChain to adjust parameters based on network adoption and demand

## Earning VTHO

VET holders do NOT automatically generate VTHO, as of Hayabusa, anymore. Instead VET holders who are wiling to participate
should buy Stargate NFT of appropriate level and stake via Stargate in order to receive VTHO as a reward for participation.
More about staking can be found in Stargate docs:

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

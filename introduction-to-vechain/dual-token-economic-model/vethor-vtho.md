---
description: Understanding VeChain's transaction/gas token, VTHO
---

# VeThor Token (VTHO)

<table><thead><tr><th width="258.27956989247315">VTHO Characteristics</th><th>Details</th></tr></thead><tbody><tr><td>Type</td><td><a href="https://github.com/vechain/VIPs/blob/master/vips/VIP-180.md">VIP180</a></td></tr><tr><td>Token contract address</td><td>0x0000000000000000000000000000456E65726779</td></tr><tr><td>Precision</td><td>18 decimal places</td></tr><tr><td>Supply</td><td>VTHO is the energy or the cost of carrying out the payment and smart contract transactions on the VeChainThor blockchain.</td></tr><tr><td>Consumption</td><td>70% of the transaction fee paid in VTHO in each block is burned and the remaining 30% is rewarded to the Authority Masternode which produces the block.</td></tr></tbody></table>

## VIP180: VeChain's Fungible Token Standard

VeChain had implemented an improvement proposal defining a new fungible token standard, VIP180. It was a superset of Ethereum's ERC20 standard, now superseeded. All VIP180 are compatible with the most used ERC20 fungible token standard across blockchains. VTHO, as a VIP180 token, powers the VeChainThor blockchain by:

* Serving as the fee for transactions and smart contract execution
* Rewarding Authority Masternodes for block production and network maintenance

## VTHO Supply Dynamics

Unlike VET, VTHO doesn't have a fixed maximum supply. Its supply is governed by:

* Generation rate: new VTHO is generated at every block by holding VET
* Consumption: VTHO is used for transaction fees, which is split in two parts
  * 70% gets burned
  * 30% goes to the Authority Masternode who proposed the block as reward

This dynamic supply model allows VeChain to adapt to network demand and maintain economic stability.

## The Purpose of VTHO Burning

VTHO burning serves several crucial functions:

* **Supply Control**: Helps regulate the circulating supply of VTHO
* **Value Stability**: Aims to maintain a stable VTHO value for predictable transaction costs
* **Flexibility**: Allows VeChain to adjust parameters based on network adoption and demand

## Earning VTHO

VET holders automatically generate VTHO at a constant rate, without the need for active staking or node operation. This passive reward system encourages long-term holding and participation in the VeChain ecosystem.

## VTHO generation formula

VTHO is generated from holding VET at a constant rate of $$5 \cdot 10^{-9}$$ VTHO per VET per second or 0.000432 VTHO per VET every 24 hours. Mathematically, we can write it as:

$$E_{gen} = v \cdot V \cdot t$$

Where $$E_{gen}$$ denotes the amount of VTHO generated from holding $$V$$ amount of VET. $$v$$ is the VTHO generation velocity which is a constant equal to $$5 \cdot 10^{-9}$$, per second. Let $$t$$ be the amount of time in seconds. An example would be, if an individual had 10k VET in an account, they would generate 4.32 VTHO every 24 hours.

## VTHO transaction cost formula

On the other hand, for each transaction, a transaction fee must be paid to pay for the computation on the network. Mathematically, we can write it as:

$$E_{con} = p \cdot G$$

Where $$E_{con}$$ is the price in VTHO for performing a transaction. $$G$$ denoates the amount of gas required to process the transaction and $$p$$ the gas price in VTHO, which is a constant equal to $$1 \cdot 10^{-5}$$. An example would be, if an individual were performing a transaction costing 21k gas, they would have to pay 0.21 VTHO.

The gas price $$p$$ can vary in the range $$[p^{base}, 2 \cdot p^{base}]$$ where $$p^{base}$$ is a parameter that can be adjusted according to the market supply and demand of VTHO. Currently, we set $$p^{base} = 1 \cdot 10^{-5}$$.

This dual-token model, with VET generating VTHO and VTHO powering transactions, creates a flexible, scalable economic system for the VeChainThor blockchain. It allows for transaction cost stability while maintaining the potential for VET value appreciation, making it attractive for both enterprise use and individual investment.

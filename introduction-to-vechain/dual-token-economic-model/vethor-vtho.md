---
description: Vechain's transaction / gas token.
---

# VeThor (VTHO)

<table><thead><tr><th width="258.27956989247315">VTHO</th><th></th></tr></thead><tbody><tr><td>Type</td><td><a href="https://github.com/vechain/VIPs/blob/master/vips/VIP-180.md">VIP180</a></td></tr><tr><td>Token contract address</td><td>0x0000000000000000000000000000456E65726779</td></tr><tr><td>Precision</td><td>18 decimal places</td></tr><tr><td>Supply</td><td>VTHO is the energy or the cost of carrying out the payment and smart contract transactions on the VeChainThor blockchain.</td></tr><tr><td>Consumption</td><td>70% of the transaction fee paid in VTHO in each block is burned and the remaining 30% is rewarded to the Authority Masternode which produces the block.</td></tr></tbody></table>

## What is a VIP180 token?

VIP180 is an implemented improvement proposal which defined a fungible token standard in VeChain. VIP180 is a superset of the ERC20 standard on the Ethereum blockchain and is the most used fungible standard used across all blockchains. VTHO is the energy token used to power VeChainThor. Transactions will be paid in VTHO and Authority Masternodes are paid in VTHO for producing blocks, securing and maintaining the chain.

## Does VTHO have a max supply?

No, unlike VET, VTHO does not have a max supply. VTHO supply is governed by the generation and burning parameters, you can read more about the technical details in the last section of this page. VTHO parameters can only be altered via the transparent governance process and can be configured to increase or decrease the monetary supply. Currently, the supply is regulated by destroying 70% of the VTHO used for transaction costs. The other 30% will go towards the Authority Masternodes as a reward for maintaining the blockchain.

## Why are VTHO burned?

Burning is when a fraction of the tokens are sent to a wallet without a private key, thus rendering the tokens irrecoverable as they cannot be moved from the wallet. Tokens are burned to attempt to control the supply of a token which in turn will control the market value. This mechanism allows VeChain to be reactive to the amount of demand on the network. If the network witnesses greater adoption, the parameters can be reduced to allow for more VTHO to be circulated.

## Do I earn VTHO?

Yes, by holding VET in a wallet, you can earn VTHO. Holding VET generates VTHO automatically, it is built into the protocol. Unlike many other blockchains, VeChain users are not burdened with the task of staking with nodes to earn rewards.

## VTHO generation formula

VTHO is generated from holding VET at a constant rate of $$5 \cdot 10^{-9}$$ VTHO per VET per second or 0.000432 VTHO per VET every 24 hours. Mathematically, we can write it as:

$$E_{gen} = v \cdot V \cdot t$$

Where $$E_{gen}$$ denotes the amount of VTHO generated from holding $$V$$ amount of VET. $$v$$ is the VTHO generation velocity which is a constant equal to $$5 \cdot 10^{-9}$$, per second. Let $$t$$ be the amount of time in seconds. An example would be, if an individual had 10k VET in an account, they would generate 4.32 VTHO every 24 hours.

## VTHO transaction cost formula

On the other hand, for each transaction, a transaction fee must be paid to pay for the computation on the network. Mathematically, we can write it as:

$$E_{con} = p \cdot G$$

Where $$E_{con}$$ is the price in VTHO for performing a transaction. $$G$$ denoates the amount of gas required to process the transaction and $$p$$ the gas price in VTHO, which is a constant equal to $$1 \cdot 10^{-5}$$. An example would be, if an individual were performing a transaction costing 21k gas, they would have to pay 0.21 VTHO.

The gas price $$p$$ can vary in the range $$[p^{base}, 2 \cdot p^{base}]$$ where $$p^{base}$$ is a parameter that can be adjusted according to the market supply and demand of VTHO. Currently, we set $$p^{base} = 1 \cdot 10^{-5}$$.

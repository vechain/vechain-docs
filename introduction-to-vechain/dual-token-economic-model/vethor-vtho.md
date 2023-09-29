---
description: Vechain's transaction / gas token.
---

# VeThor (VTHO)

<table><thead><tr><th width="265">VTHO</th><th></th></tr></thead><tbody><tr><td>Type</td><td><a href="https://github.com/vechain/VIPs/blob/master/vips/VIP-180.md">VIP180</a></td></tr><tr><td>Token contract address</td><td>0x0000000000000000000000000000456E65726779</td></tr><tr><td>Precision</td><td>18 decimal places</td></tr><tr><td>Supply</td><td>VTHO is the energy or the cost of carrying out the payment and smart contract transactions on the VechainThor blockchain. VTHO is generated from VET in each block over time in a linear manner. (0.000432 VTHO is generated per VET per day)</td></tr><tr><td>Consumption</td><td>70% of the transaction fee paid in VTHO in each block is burned and the remaining 30% is rewarded to the Authority Masternode which produces the block.</td></tr></tbody></table>

## What is a VIP180 token?&#x20;

VIP180 is an implemented improvement proposal which defined a fungible token standard in vechain. VIP180 is a superset of the ERC20 standard on the Ethereum blockchain and is the most used fungible standard used across all blockchains. VTHO is the energy token used to power VechainThor. Transactions will be paid in VTHO and Authority Masternodes are paid in VTHO for producing blocks and maintaining the chain.

## Does VTHO have a max supply?&#x20;

No, unlike VET, VTHO does not have a max supply. VTHO supply is governed by the generation and burning parameters, you can read more about the technical details in the last section of this page. VTHO parameters can only be altered via the transparent governance process and can be configured to increase or decrease the monetary supply. Currently, the supply is regulated by destroying 70% of the VTHO used for transaction costs. The other 30% will go towards the Authority Masternodes as a reward for maintaining the blockchain.&#x20;

## Why are VTHO burned?&#x20;

Burning is when a fraction of the tokens are sent to a wallet without a private key, thus rendering the tokens irrecoverable as they cannot be moved from the wallet. Tokens are burned to attempt to control the supply of a token which in turn will control the market value. This mechanism allows vechain to be reactive to the amount of demand on the network. If the network witnesses greater adoption, the parameters can be reduced to allow for more VTHO to be circulated.

## Do I earn VTHO?&#x20;

Yes, by holding VET in a wallet, you can earn VTHO. Holding VET generates VTHO automatically, it is built into the protocol. Unlike many other blockchains, vechain users are not burdened with the task of staking with nodes to earn rewards.

## The maths behind VTHO generation.

According to our design, VTHO is generated from holding VET at a constant speed. In this way, we are able to detach the direct cost of using the VechainThor blockchain from the VET price. Let $$V$$ be the amount of VET, $$t$$ the amount of time, in terms of the number of blocks, and $$v$$ the VTHO generation speed. Mathematically, we can write

$$E_{gen} = v \cdot V \cdot t$$

where $$E_{gen}$$ denotes the amount of VTHO generated from holding $$V$$ VET. On the other hand, for each transaction, let $$G$$ be the amount of Gas required to process the transaction by the system and $$p$$ the transaction fee / gas price in VTHO given by the transaction sender, we can calculate the amount of VTHO consumed for the transaction as:

$$E_{con} = p \cdot G$$

Velocity $$v$$ is a constant equal to $$5 \cdot 10^{-8}$$ VTHO per VET per block. In other words, if you had 10K VET, you would be given at most 4.32 VTHO every 24 hours. The gas price $$p$$ can vary in the range $$[p^{base}, 2 \cdot p^{base}]$$ where $$p^{base}$$ is a parameter that can be adjusted according to the market supply and demand of VTHO. Currently, we set $$p^{base} = 1 VTHO / Kgas$$.

{% hint style="info" %}
The current VTHO generation rate is 0.000432 VTHO per 1 VET.
{% endhint %}

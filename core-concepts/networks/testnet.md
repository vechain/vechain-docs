---
description: Defining a blockchain testnet and it's purposes.
---

# Testnet

## What is a blockchain testnet?

A blockchain testnet is a testing environment where developers and users can experiment prior to deploying code to the blockchain production network, refered to as mainnet. Testnets are essentially separate blockchain networks that mirror the functionality of the mainnet but are isolated from it. Testnets in blockchain networks should have identical consensus mechanisms, network infrastructure, blockchain protocol and economic model.

## How can I access the testnet?

In order to interact with the testnet you either have to run a node yourself and send requests to the node to access the blockchain, or alternatively, you would need to identify a public node, who's job it is to add transactions to the network and return with data from the network, and direct requests there. There are several community run nodes as well as third party services who operate nodes.

{% hint style="info" %}
See a full list of the publicly available VeChainThor nodes in the Developer Resource article [nodes.md](../../how-to-run-a-node/nodes.md "mention")
{% endhint %}

## What are some key characteristics of testnets?

**Tests Tokens:** As previously stated, the economic model should mirror mainnet. That means on the VeChain testnet, VET and VTHO will have identical max supply and generation/burn parameters. The major difference is that testnet tokens are never supposed to have real world value.

**Faucets:** A testnet faucet is essentially a wallet which holds vast amounts of testnet tokens. A developer/user can enter their wallet address and receive a specific amount of testnet funds to carry out tests. It is good practice and ethics to return testnet funds to the faucet once you have finished testing, so other developers can use the service.

{% hint style="info" %}
Need some testnet funds, use our faucet, [https://faucet.vecha.in](https://faucet.vecha.in)
{% endhint %}

{% hint style="info" %}
If you have testnet VET and need to convert some to testnet VTHO use [https://energy.outofgas.io/#/](https://energy.outofgas.io/#/)
{% endhint %}

**Community support:** A key to a blockchain network functioning lies in incentivisation. Stakeholders, miners or nodes, support consensus and get rewarded for their time. Although the rewards paid to these stakeholders in the testnet should mirror mainnet, the rewards are worthless in a financial sense. Therefore, often the community support the maintenance of the testnet without directly receiving a reward. In the long run, the usability of a blockchain depends on having a well maintained testnet for builders.

## What can't I validate on testnet?

Deploying on testnet will validate much of your dApp, however there are some conditions testnet may not validate. An example of this may be network congestion, how does the dApp perform if transactions are not received at an expected time. The reality of mainnet is there will often be some congestion and transactions may take longer to propagate through the network.

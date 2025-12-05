---
description: Defining the different types of nodes who support the VeChain ecosystem.
---

# Nodes

## What are nodes in blockchain networks?&#x20;

In blockchain networks, nodes are individual computers or devices that participate in maintaining the blockchain's network alive and secure by either 

* validating
* storing
* relaying 

transactions and blocks of data

As with any peer-to-peer network, nodes play a crucial role in the overall functioning and security of the network. The more nodes who contribute to the network, generally the more robust and secure the network will be. 
&#x20;

## What are the different types of nodes that support the VeChainThor blockchain?&#x20;

The VeChainThor network is supported by various different types of nodes, who all contribute to the ecosystem in a particular way.

### Validators (VeChainThor Validators)

Are responsible for maintaining consensus and producing blocks on the VeChain network (see [Consensus](../consensus/consensus.md "mention")). There are 101 active validators who are authorised to validate and propose new blocks. As a reward, they receive the priority fees of the transactions in the block, with the baseFee being burned (see [Transaction Fees](../transactions/transaction-fees.md "mention")).&#x20;

There's a big responsibility for validators, and so it's required that they:&#x20;

* Stake 25M VETs as collateral
* Run and manage a server with the best possible level of performance and availability.

As the network will require 2/3+1 of the validators to reach consensus and finality. 

### Economic & X-Nodes

Node programs have been shifted to StarGate (see [StarGate](https://docs.stargate.vechain.org "mention")).
Both VeChain Economic and X-Node are encouraged to migrate to StarGate, where they will receive a new node of equivalent level, and become eligible of the additional rewards if they stake it.

{% hint style="info" %}
Please note only new nodes can participate in the network governance.&#x20;
{% endhint %}


### Full Nodes

Full nodes can be deployed by anybody by running an instance of the VeChainThor node software, and they support the network in a few fundamental ways. Full nodes are configured to be interacted with and are constantly injecting new transactions into the network for AMs to build into blocks. Full nodes also enable people to query the VeChainThor blockchain and get the blockchain data from the chain to other systems to be processed. They also increase resiliency as they have a complete copy of the blockchain history stored.

{% hint style="info" %}
See a full list of the publicly available VeChainThor nodes in the Developer Resource article [nodes.md](../how-to-run-a-node/nodes.md "mention")
{% endhint %}

{% hint style="info" %}
Interested in operating a public Thor node, here's a link to the public repo [https://github.com/vechain/thor](https://github.com/vechain/thor), and a link to a tutorial on how to run a local Thor node [how-to-run-a-thor-solo-node](../how-to-run-a-node/how-to-run-a-thor-solo-node.md "mention").
{% endhint %}

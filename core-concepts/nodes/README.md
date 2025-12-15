---
description: Defining the different types of nodes who support the VeChain ecosystem.
---

# Nodes

## What are nodes in blockchain networks?

In blockchain networks, nodes are individual computers or devices that participate in maintaining the blockchain's network by&#x20;

* validating
* storing
* relaying

transactions and blocks.&#x20;

As with any peer-to-peer network, nodes play a crucial role in the overall functioning and security of the network. The more nodes who contribute to the network, generally the more robust and secure the network will be.

## What are the different types of nodes that support the VeChainThor blockchain?

The VeChainThor network is supported by various different types of nodes, who all contribute to the ecosystem in a particular way.

### Validators

Validators are responsible for keeping operational both consensus and block production on the VeChain network. There are 101 who are active, via a FIFO queue. They are responsible to validate and propose blocks on the VeChainThor blockchain. As a reward, receives 30% of all VTHO which was delegated to him, and the priority fees of the blocks he proposes.

There's a rigorous process implemented in order for a person/entity to run a validator:

* Hold 25M VETs as collateral; and,
* Run and manage the node with a certain guaranteed level of performance and availability

### StarGate Nodes

With only 101 nodes being responsible for the network, staking program aim to increase stability in the VeChain ecosystem and act as a distribution of power and privilege within the blockchain’s economy.&#x20;

StarGate nodes are also governance tokens and are tied to a minimum requirement of VET, and the  node tiers have slightly different requirements.

  More about staking can be found in the [StarGate docs](https://docs.stargate.vechain.org).

### Full Nodes

Full nodes can be deployed by anybody by running an instance of the VeChainThor node software, and they support the network in a few fundamental ways. Full nodes, once fully synced, can relay new transactions into the network for AMs to build into blocks. Full nodes also enable people to query the VeChainThor blockchain and get the blockchain data from the chain to other systems to be processed. They also increase resiliency as they have a complete copy of the blockchain history stored.

{% hint style="info" %}
See a full list of the publicly available VeChainThor nodes in the Developer Resource article [nodes.md](../../how-to-run-a-node/nodes.md "mention")
{% endhint %}

{% hint style="info" %}
Interested in operating a public Thor node, here's a link to the public repo [https://github.com/vechain/thor](https://github.com/vechain/thor), and a link to a tutorial on how to run a local Thor node [how-to-run-a-thor-solo-node](../../how-to-run-a-node/how-to-run-a-thor-solo-node.md "mention").
{% endhint %}

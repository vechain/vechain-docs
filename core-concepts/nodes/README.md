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

### Authority Masternode (AM)

AMs are responsible for keeping operational both consensus and block production on the VeChain network. There are 101 AMs who are authorised, via an on-chain whitelist, to validate and propose blocks on the VeChainThor blockchain. As a reward, the AM who has proposed a block receives 30% of all VTHO used for the transactions (gas fees) in a block, with the other 70% being burned.

There's a rigorous process implemented in order for a person/entity to run an AM:

* Be vetted to ensure they have a legitimate identity;
* Hold 25M VETs as collateral; and,
* Run and manage the node with a certain guaranteed level of performance and availability.

### Economic & X-Nodes

With only 101 nodes being responsible for the network, both VeChain Economic and X-Node programs aims to increase stability in the VeChain ecosystem and act as a distribution of power and privilege within the blockchain’s economy.&#x20;

Both nodes are governance tokens and are tight to a minimum requirement of VET soft-locked in the wallet, and the two node types but have slightly different requirements.

<table><thead><tr><th width="156.33333333333331"></th><th>Economic Nodes</th><th>X-Nodes</th></tr></thead><tbody><tr><td>Rewards</td><td>--</td><td>VTHO generated from 5bln VET X-Node pool.</td></tr><tr><td>Application</td><td>Applied for based on minimum VET required or purchased on secondary market.</td><td>X-Node non-fungible tokens (NFTs) were distributed upon mainnet launch but can be purchased on secondary market.</td></tr><tr><td>Upgrade</td><td>Upgradeable, minimum threshold of next tier applies.</td><td>Upgradeable, minimum threshold of next tier applies.</td></tr><tr><td>Revoke</td><td><p>VET drops below current level minimum threshold then node level gets downgraded.</p><p>Unclaimed VTHO can be claimed.</p></td><td>VET drops below current level minimum threshold then Node token loses X status and becomes an Economic Node. VeThorX node in this case gets destroyed as lowest X level node<br><br>Unclaimed VTHO can be claimed.</td></tr></tbody></table>

<table><thead><tr><th width="157">Node</th><th width="157">Requirement</th><th width="142">Staking Bonus</th><th width="151">Maturity Period</th><th width="129">Voting Tier</th></tr></thead><tbody><tr><td><img src="https://manager.vechainstats.com/assets/images/tokens/Node-VNT-S.png" alt="Strength Economic node" data-size="line"> Strength</td><td>1,000,000 VET</td><td></td><td>10 days</td><td>1 EN Votes</td></tr><tr><td><img src="https://manager.vechainstats.com/assets/images/tokens/Node-VNT-T.png" alt="Thunder Economic node" data-size="line"> Thunder</td><td>5,000,000 VET</td><td></td><td>20 days</td><td>5 EN Votes</td></tr><tr><td><img src="https://manager.vechainstats.com/assets/images/tokens/Node-VNT-M.png" alt="Mjolnir Economic node" data-size="line"> Mjolnir</td><td>15,000,000 VET</td><td></td><td>30 days</td><td>15 EN Votes</td></tr><tr><td><img src="https://manager.vechainstats.com/assets/images/tokens/Node-VNT-XV.png" alt="VeThor X-node" data-size="line"> VeThor X</td><td>600,000 VET</td><td>25%</td><td>-</td><td>1 XN Votes</td></tr><tr><td><img src="https://manager.vechainstats.com/assets/images/tokens/Node-VNT-XS.png" alt="Strength X-node" data-size="line"> Strength X</td><td>1,600,000 VET</td><td>100%</td><td>30 days</td><td>3 XN Votes</td></tr><tr><td><img src="https://manager.vechainstats.com/assets/images/tokens/Node-VNT-XT.png" alt="Thunder X-node" data-size="line"> Thunder X</td><td>5,600,000 VET</td><td>150%</td><td>60 days</td><td>10 XN Votes</td></tr><tr><td><img src="https://manager.vechainstats.com/assets/images/tokens/Node-VNT-XT.png" alt="Mjolnir X-node" data-size="line"> Mjolnir X</td><td>15,600,000 VET</td><td>200%</td><td>90 days</td><td>26 XN Votes</td></tr></tbody></table>

### Full Nodes

Full nodes can be deployed by anybody by running an instance of the VeChainThor node software, and they support the network in a few fundamental ways. Full nodes, once fully synced, can relay new transactions into the network for AMs to build into blocks. Full nodes also enable people to query the VeChainThor blockchain and get the blockchain data from the chain to other systems to be processed. They also increase resiliency as they have a complete copy of the blockchain history stored.

{% hint style="info" %}
See a full list of the publicly available VeChainThor nodes in the Developer Resource article [nodes.md](../../how-to-run-a-node/nodes.md "mention")
{% endhint %}

{% hint style="info" %}
Interested in operating a public Thor node, here's a link to the public repo [https://github.com/vechain/thor](https://github.com/vechain/thor), and a link to a tutorial on how to run a local Thor node [how-to-run-a-thor-solo-node.md](../../how-to-run-a-node/how-to-run-a-thor-solo-node.md "mention").
{% endhint %}

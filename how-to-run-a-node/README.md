---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
---

# How to run a node

To interact with the blockchain, a node is required.&#x20;

The node is the blockchain client, that runs locally and connects to the distributed network of all the other clients. Every node holds a local copy of the blockchain and can potentially participate in the consensus.&#x20;

Dapps do require to push and pull information to and from the blockchain, to do so, they will require to be connected to a node. In many cases, a remote connection to a public node is sufficient.&#x20;

Public nodes are hosted by organizations like VeChain, and are particularly helpful for "light-clients" like wallets to avoid having the weight of a local copy of the blockchain, and of the time required to being operative, since a new node requires to download all the history before being ready. Of course, the machine performance of a public node is shared across the users, even when allocating multiple machines and systems to balance demand, they have an upper limit that might not match what the dapp requires. In such cases, but also for additional trust and to avoid the eventuality of censorship, running a node is recommended.

Mastering VeChainThor nodes opens up a world of possibilities in blockchain development. Whether you're running a local Thor Solo Node for development or connecting to public nodes for production, understanding these concepts is crucial for building robust, blockchain-powered applications.

By leveraging the power of nodes, the flexibility of the Thorest API, and the development-friendly environment of Thor Solo, you're well-equipped to innovate on the VeChainThor blockchain. Happy building!

<table data-view="cards"><thead><tr><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center">Nodes</td><td><a href="nodes.md">nodes.md</a></td></tr><tr><td align="center">How to run a Thor Solo Node</td><td><a href="how-to-run-a-thor-solo-node.md">how-to-run-a-thor-solo-node.md</a></td></tr><tr><td align="center">Custom Network</td><td><a href="custom-network.md">custom-network.md</a></td></tr><tr><td align="center">Connect Sync2 to a Thor Solo Node</td><td><a href="connect-sync2-to-thor.md">connect-sync2-to-thor.md</a></td></tr></tbody></table>

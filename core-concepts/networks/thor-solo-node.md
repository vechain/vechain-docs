---
description: An introduction to the Thor solo node and its purpose.
---

# Thor Solo Node

## What is Thor solo node?

Running a solo node in blockchains refers to operating a single node that independently maintains and validates the entire blockchain network. In other words, a solo node does not rely on other nodes for validation and verification of transactions and blocks. Instead, it performs all the necessary tasks on its own. Therefore, running a Thor solo node is essentially running the VehcainThor node software but not connecting it to other network participants in mainnet or testnet.

### When should I run a Thor solo node?

Developers are encouraged to run a Thor solo node when they are developing. Thor nodes are useful in the sense you can initially validate the behaviour of smart contracts which will support decentralized applications (dApps) in a closed off environment. Initial tests on Thor solo nodes often don't need the entire history of the blockchain and it makes setting up a test environment simpler and less time consuming for the developer.

## What are the limitations to testing and validating on a Thor solo node?

As good as Thor solo nodes are for initial testing, we would always recommend that developers validate dApps on VechainThor's testnet before going into production on mainnet. Thor solo nodes are great for validating the core functionality of smart contracts but they do not simulate a real world peer-to-peer network. Here are some potential vulnerabilities that won't be discovered while using a Thor solo node:

* **Real world conditions:** Running a dApp on a Thor solo node means it is not exposed to real-world network conditions. In a decentralised network, various factors like latency, packet loss, and network congestion can affect the performance and reliability of the dApp.
* **Security vulnerabilities:** A Thor solo node setup does not adequately replicate the security measures and potential attack vectors that exist in a real-world network. Testnets provide an environment where you can identify and address security vulnerabilities.
* **Scalability & Performance:** Testing on a Thor solo node limits your ability to assess the scalability and performance of your dApp. In a decentralised network, the load is distributed among multiple nodes, and the performance of your dApp may vary depending on network size and activity.

{% hint style="info" %}
If you'd like to understand more about practically working with a Thor solo node, see [how-to-run-a-thor-solo-node](../../developer-resources/tutorials/how-to-run-a-thor-solo-node/ "mention")
{% endhint %}

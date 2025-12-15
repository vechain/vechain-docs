---
description: Introduction to blockchain governance and VeChain's implementation.
---

# Governance

## On-Chain Governance Overview

On-chain governance in blockchain refers to the process of making decisions and implementing changes in a permissionless and auditable way. This approach ensures transparency, allowing all stakeholders and community members to view proposals, cast votes, and audit outcomes. Major stakeholders in blockchain networks should aim to make as many decisions as possible directly on-chain.

## VeChain's On-Chain Governance Implementation

VeChain leverages on-chain governance to enable stakeholders to make decentralize decision with on-chain voting.
Execution though was kept off-chain. This means that the outcome will require a human action to propagate the change.
These actions can, for instance, be activating or not a new network upgrade, changing token emission parameters, gas rules or block rewards, or any technical or economic mechanics that can be implemented on the VeChainThor blockchain.

VeChain's on-chain governance process consists of three phases:

* **Decision making:** creation of a Discourse discussion, and possibly also a VIP with all the details of the subject of a new voting.
* **Authorization:** actual creation of the proposal by whitelisted accounts to safeguard on-chain governance against malicious activities.
* **Execution:** off-chain mechanics to execute a proposal that has passed, ending in an on-chain transaction to track and notify that the change was executed.

## Voters

Voting power is available through staking. The number of votes, the voting power, is determined by the node tiers owned or managed.

For more details, refer to the [VeVote documentation](https://docs.vevote.vechain.org). 

  More about staking can be found in the [StarGate docs](https://docs.stargate.vechain.org).

## Some History

The governing body of VeChain, was originally a steering committee, which represented the balanced interests of all VeChainThor blockchain stakeholders. The steering committee has now been deprecated, and decisions are in the hands of Node holders and Validators casting their votes on VeVote.

{% hint style="info" %}
Explore VeChain's on-chain governance and view past or future proposals, visit [VeVote](https://vevote.vechain.org/home), VeChain's voting platform. VeVote enhances ecosystem transparency and decentralization.
Specific documentation can be found here: [docs.vevote.vechain.org](docs.vevote.vechain.org) together with details about the new goverance.
{% endhint %}

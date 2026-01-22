---
description: A deeper dive into our PoA consensus mechanism.
---

# Consensus Deep Dive

## Transitioning from Proof of Authority (PoA) to Delegated Proof of Stake (DPoS) <a href="#transition" id="transition"></a>

Designing a consensus algorithm for a public blockchain network is a critical decision that influences how participants agree on the blockchain's growth and embodies the governance model of the network. VeChainThor originally implemented a PoA consensus algorithm. As VeChain evolves towards greater decentralization and stakeholder participation, there is a growing need for a staking-based consensus mechanism that enables broader stakeholder involvement. This led to the governance-approved DPoS.

Upgrading to a DPoS consensus mechanism has introduced a new way to participating in consensus, via delegation (becoming Delegators). Individual VET token holders can participate in securing the VeChainThor network in a user-friendly, secure and compliant way. 
Delegations contribute this way to higher levels of cryptoeconomic security of the VeChainThor blockchain.

To become a Validator instead, there are minimum requirements to meet.
## What's new <a href="#what-s-new" id="what-s-new"></a>

* **Increased Decentralization:** The validator set is no longer rigidly defined by central authority. Instead, it becomes dynamically determined by market-based staking, expanding the pool of potential validators and reducing reliance on trusted parties.
* **Enhanced Cryptoeconomic Security:** By allowing a wider base of VET holders to contribute their stake toward securing the network, DPoS increases the economic weight behind consensus, raising the cost of potential attacks and improving the overall resilience of the blockchain.
* **Validator Competition and Accountability:** With stake-weighted block production and the possibility of entry and exit from the validator set, performance and reputation become key to retaining delegations and rewards. This fosters greater validator accountability and operational excellence.

## Validation <a href="#validation" id="validation"></a>

The validator is limited to 101 active validators. Any participant meeting the minimum staking requirement of 25m VET will be eligible to become a validator.

Validator admission will follow a first-in, first-out (FIFO) queueing mechanism. Validators who meet the staking requirement and submit a valid staking transaction enter the prospective validator queue. When a position becomes available in the active validator set, due to an exit, the next eligible validator in the queue is promoted to an active validator at the start of the next epoch.

Validators that are inactive for more than 7 days will be evicted from the Leader group (the set of validators currently elected to participate in the network’s consensus) and placed on the exit queue.

## Delegation <a href="#delegation" id="delegation"></a>

Delegations will be restricted to a single entity the delegator contract. This delegator contract will serve as a single, trusted delegation layer that interfaces between individual delegators and the VeChainThor validator set.

## Finality <a href="#finality" id="finality"></a>

Under the current PoA consensus, finality for an epoch is achieved after two rounds of Byzantine Fault Tolerance (BFT), where each round requires at least two-thirds of the leader group to propose a block within the epoch. Proposing a block is effectively a vote for finalizing the epoch.

With the transition to DPoS consensus, this mechanism requires modification. Unlike PoA, validator nodes in DPoS are no longer uniform in stake size. Relying on two-thirds of the validator count to propose a block within an epoch is less likely as validators may differ significantly in their quantity of staked VET.

To ensure a high likelihood of the network being able to achieve finality, the mechanism will be altered slightly. Finality will require more than two-thirds of the total weighted staked VET to have proposed a block within an epoch. This update aligns the finality mechanism with the stake-based nature of DPoS, maintaining both security and liveness in the consensus protocol.

## Block Production Likelihood <a href="#block-production-likelihood" id="block-production-likelihood"></a>

In the VeChainThor blockchain, under PoA consensus, validators do not compete to create blocks. Instead, they are selected through a random mechanism, ensuring equal, predictable and deterministic block production. Provided the validator set remains stable and no slots are missed. The sequence of block producers is known for the next 8,640 slots.

Under DPoS consensus, a modification to block production will be introduced, making the likelihood of a validator producing a block proportional to the quantity of VET staked. Validators with higher total staked VET will have an increased likelihood of being selected to produce the next block. Delegations from different network participants will influence this likelihood, with different weights applied to different network participants.

#### Formula
$$P_{v} = \frac{W_{v} * S_{vs} + W_{x} * \sum S_{xd} + W_{e} * \sum S_{ed}}{\sum_{i=1}^{101}(W_{v} * S_{vs,i} + W_{x} * \sum S_{xd,i} + W_{e} \sum S_{ed,i})}$$

#### Variables
- **$P_{v}$:** Probability that validator $v$ is selected to produce a block.
- **$W_{v}$:** Valdiator weight.
- **$S_{vs}$:** VET Staked by validator $v$.
- **$W_{x}$:** X-Node weight.
- **$S_{xd}$:** Staked VET from X-Node delegations to validator $v$.
- **$W_{e}$:** Eco-Node weight.
- **$S_{ed}$:** Staked VET from Eco-Node delegations to validator $v$.
- **$\sum S_{xd}$:** Total staked VET from X-Node delegations to validator $v$.
- **$\sum S_{ed}$:** Total staked VET from Eco-Node delegations to validator $v$.

### Delegator Contract Trusted Intermediary

All delegation operations will be restricted to a single, trusted delegator contract intermediary.

### Validator Staking Identification

Unique validator identification is an important requirement to ensure that delegations are assigned to the correct validator. To generate a unique validator identification a validator’s endorser account will sign and issue a transaction requesting to create a stake in the network.

The create stake transaction must contain the following information:
   - **Stake:** The quantity of VET being committed to securing the network.
   - **Stake Lock Period:** The duration of time that the validator is committing to secure the network.
   - **Auto Renewal:** A binary option signalling the validators intent to automatically recommit to securing the network for the same stake lock period after the completion of the current stake lock period.
   - **NodeID:** The public address of the validator node that proposes blocks..

A validator's unique ValidationID is the outcome of a signed transaction `ValidationID = Sign(Endorsor Account, AddValidationTx(Stake, Staking Lock Period, Auto Renewal, NodeID))`. The create validator stake transaction must have a NodeID that is not in Queued, Active, or On Cooldown state.

### Delegation Position Identification 

Given the protocol does not have a direct connection to the VET holder that is delegating stake to the protocol it is important to have a unique identifier for delegation positions.

To generate a unique delegation position identification a delegation position stake transaction must contain the following information
   - **Stake:** The quantity of VET being committed to securing the network.
   - **Validation ID:** The validation id that the delegator intends to stake with.
   - **Auto Renewal:** A binary option signalling the validators intent to automatically recommit to securing the network for the same stake lock period after the completion of the current stake lock period.
   - **Multiplier:** A multiplier that will be applied to the stake to contribute to the block production likelihood.

A delegation position identification is calculated as an incremental counter. The create delegator position stake transaction must have a ValidationID that is not On Cooldown state.

### Validator Operations

#### Stake Lock Period

When joining the network, a validator specifies a stake lock period, the duration of time they commit to securing the network. This period aligns with the start and end of an epoch.

During the stake lock period, a validator may submit transactions to increase or decrease their stake, or to disable their auto-renewal setting.

#### Alter Stake

To increase their staked VET, the validator sends a transaction along with additional VET. The increased quantity of VET will take effect at the start of the next staking period. To decrease their stake, the validator submits a transaction signalling the desired reduction, also effective at the start of the next staking period. The reduced quantity of VET  becomes withdrawable once the current stake lock period ends.

#### Alter Auto-Renewal

When joining the VeChainThor network validators have their auto-renewal set to TRUE, meaning that the validator will automatically enter a new stake lock period of the same duration once the current stake lock period concludes. A validator can stop their auto-renewal by sending a transaction which will set auto-renewal to FALSE. If the auto-renewal is set to FALSE, the validator begins the exit process at the end of the current stake lock period. Once the auto-renewal is set to FALSE it is non reversible, the validator will exit at the end of the stake lock period.

### Validator Entry

<img width="865" alt="Image" src="https://github.com/vechain/VIPs/blob/master/assets/vip-253/entry.png?raw=true" />

Prospective validators join the leader group on a First-In, First-Out (FIFO) basis, provided there is available capacity. Once a validator enters the leader group, their stake lock period begins and they are eligible to earn rewards. Validator joining is aligned to an epoch block.

### Validator Exit

<img width="749" alt="Image" src="https://github.com/vechain/VIPs/blob/master/assets/vip-253/exit.png?raw=true" />

When an active validator submits an exit transaction and completes their staking period, they enter a cooldown period, which aligns with an epoch block. Only one validator can enter cooldown per epoch, this will be managed by a FIFO queue. When a validator enters the cooldown state, the validator is removed from the leader group and can no longer accept delegations, increase or decrease their staked VET or alter their auto-renewal setting. Delegators associated with a validator in the cooldown state can access their funds. Delegators in a fully exited validator are inactive and ineligible for rewards, and can withdraw their funds. The validator’s staked VET becomes withdrawable at the end of the cooldown period, the exit_epoch.

### Delegator Operations

All delegation operations modifying individual delegation positions are performed via the delegator contract.

#### Alter Auto-Renewal

When joining the VeChainThor network delegation positions have their auto-renewal set to TRUE, meaning that the delegation position will automatically enter a new stake lock period of the same duration once the current stake lock period concludes. A delegation position can stop their auto-renewal by sending a transaction which will set auto-renewal to FALSE. If the auto-renewal is set to FALSE, the delegation position begins the exit process at the end of the current stake lock period. Once the auto-renewal is set to false it is non reversible, the delegation position will exit at the end of the stake lock period.

An edge case exists where a delegation position auto-renewal setting of TRUE is superseded by the delegated to validator exiting. Given that the delegation position depends on the existence and participation of the delegated to validator if the validator exits all delegation positions associated with the validator become inactive, ineligible for rewards and associated delegation positions can withdraw their funds.
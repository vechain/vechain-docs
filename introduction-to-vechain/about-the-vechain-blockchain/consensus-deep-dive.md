---
description: A deeper dive into our PoA consensus mechanism.
---

# Consensus Deep Dive

## Proof of Authority (PoA)

Designing a consensus algorithm for a public blockchain network is a critical decision that influences how participants agree on the blockchain's growth and embodies the governance model of the network. VeChainThor implements the PoA consensus algorithm, aligning with our governance philosophy:

> _"neither a total centralization nor a total decentralization would be the correct answer, but a compromise from and balance of both would_."

VeChainThor implements the PoA consensus algorithm which suits our governance model which states that there would not be anonymous block producer, but a fixed number of known validators (Authority Masternodes) authorized by the steering committee of the VeChain Foundation.

> “It takes twenty years to build a reputation and five minutes to ruin it. If you think about that, you’ll do things differently.” – Warren Buffett

To be an Authority Masternode (AM), the individual or entity voluntarily discloses who they are, identity and reputation by extension, to the VeChain Foundation in exchange for the right to validate and produce blocks. Their identity, reputation and financial investment is placed at stake and this acts as an incentive for the AMs to behave correctly and keep the network secure. In VeChainThor, each AM has to go through a strict know-your-customer (KYC) procedure and satisfy the minimum requirements set by the VeChain Foundation.

When discussing a consensus algorithm, we must answer the following questions:

* When is a new block produced?
* Who generates the block?
* How to choose the "trunk" from two legitimate blockchain branches?

## When <a href="#meta-transaction-features" id="meta-transaction-features"></a>

The VeChainThor blockchain schedules a new block to be generated once every $$\Delta$$ seconds. We set $$\Delta = 10$$, which is based on our estimation of the usage of VeChainThor. Let $$t_{0}$$ be the timestamp of the genesis block. The timestamp of the block with height $$h > 0$$ and $$t_{h}$$,must satisfy $$_h = t_{0} + m\Delta$$ where $$m \in \mathbb{N}^{+}$$ and $$\geqslant h$$.

## Who <a href="#meta-transaction-features" id="meta-transaction-features"></a>

PoA allows every available AM to have an equal opportunity to be selected to produce blocks. To do that, we introduce a Deterministic Pseudo-Random Process (DPRP) and the “active/inactive” AM status to decide whether a particular AM $$\alpha$$ is legitimate for producing a block $$(h,t)$$ with height $$h$$(uint32) and timestamp $$t$$(uint64). Here $$t$$ must satisfy $$(t - t_{0})mod\Delta = 0$$. We first define the DPRP to generate a pseudo-random number $$\gamma(h,t)$$ as:

$$\gamma(h,t) = DPRP(h,t) =hash(h \circ t)$$

where $$\circ$$ denotes the operation that concatenates two byte arrays.

Let $$A_{B}$$ denote the sorted set of AMs with the “active” status in the state associated with block $$B$$. Note that on the VeChainThor blockchain each AM is given a fixed index number and the numbers are used to sort elements in $$A_{B}$$. To verify whether $$a$$ is the legitimate AM for producing $$B(h,t)$$, we first define

$$A^{a}_{B(h,t)} = sort(A_{PA(Bh,t))} ) \cup a$$

where $$PA(\cdot)$$ returns the parent block. We then compute index $$i^{a}(h,t)$$as:

$$i^{a}(h,t) = \gamma(h,t) mod \parallel A^{a}_{B(h,t)} \parallel$$

AM $$a$$ is the legitimate producer of $$B(h,t)$$ if and only if $$A^{a}_{B(h,t)} [i^{a}(h,t)] = a$$. Note that we put double quotes around the word “active” to emphasize that the status does not directly reflect the physical condition of a certain AM, but merely a status derived from the incoming information from the network.

## AM Status Updating <a href="#meta-transaction-features" id="meta-transaction-features"></a>

Given the latest block $$B(h,t_{1})$$ and its parent $$B(h - 1,t_{0})$$, for any $$t_{0} < t < t_{1}$$ and $$(t - t_{0}) mod \Delta = 0$$, the system computes AM $$a_{t}$$ such that

$$A^{a_{t}}_{B(h,t_{1})}[i^{a_{t}}(h,t)] = a_{t}$$

and mark $$a_{t}$$ as "inactive" in the state associated with $$B(h,t_{1})$$. In addition, the system always sets the status of the AM that generates $$B(h,t_1)$$ as "active". Note that we set all the AMs as "active" from the beginning.

## Trunk <a href="#meta-transaction-features" id="meta-transaction-features"></a>

The final question we need to answer is how to choose the “trunk” from two legitimate blockchain branches. Since there is no computational competition in PoA, the “longest chain” rule does not apply. Instead, we consider the better branch as the one witnessed by more AMs.

To do that, we compute the accumulated witness number (AWN), $$\pi$$, for block $$B(h, t)$$ as:

$$\pi_{B(h,t)} = \pi_{PA(B(h,t))} + \parallel A_{B(h,t)} \parallel$$

with $$\pi_{B_{genesis}} = 0$$. Since $$\parallel A_{B(h,t)} \parallel$$ computes the number of AMs with “active” status associated with $$B(h,t)$$, it can be viewed as the number of AMs that witness the generation of $$B(h,t)$$. Therefore, we select the branch with the larger AWN as the trunk. If the AWNs are the same, we choose the branch with less length. Note that the AWN is stored in the block header as `TotalScore`.

Formally, given two branches $$<\mathcal{B}_{1}$$ and $$\mathcal{B}_{2}$$ with their latest blocks $${B}_{1}(h_{1},t_{1})$$ and $${B}_{2}(h_{2},t_{2})$$, respectively, we first calculate their AWNs $$\pi_{B_{1}}$$ and $$\pi_{B_{2}}$$. The system then makes the following decision: choose $${B_{1}}$$ as the trunk if $$\pi_{B_{1}} > \pi_{B_{2}}$$, or $$B_{2}$$ if $$\pi_{B_{1}} < \pi_{B_{2}}$$. In case $$\pi_{B_{1}} = \pi_{B_{2}}$$, choose $$B_{1}$$if $$h_{1} < h_{2}$$ or $$B_{2}$$ if $$h_{1} > h_{2}$$. If $$h_{1} = h_{2}$$, keep the current trunk.

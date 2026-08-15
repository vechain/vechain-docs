# How to Integrate VIP-191 (I)

This document provides an introduction to VIP-191 Fee Delegation on VeChain, explaining its purpose, significance, and potential applications. Subsequent sections will include practical examples of integrating VIP-191 into a dApp workflow.

### What is VIP-191? <a href="#what-is-vip-191" id="what-is-vip-191"></a>

VIP-191 is a fee delegation proposal introduced by VeChain. It enables users to interact with the blockchain without needing to pay transaction fees in native tokens. Instead, these fees are covered by a designated sponsor.

To illustrate, consider a real-world analogy: a parent provides their child with a supplementary credit card. The child can make purchases, but the parent ultimately pays the bill.

<figure><img src="https://cdn-images-1.medium.com/max/2152/1*-vWHlvBFcxlm3D_XeF6AlA.png" alt=""><figcaption><p><em>The sponsor pays for the user’s blockchain fees.</em></p></figcaption></figure>

### Why is VIP-191 Important? <a href="#why-is-vip-191-important" id="why-is-vip-191-important"></a>

Adopting blockchain technology can pose significant challenges for new users, such as:

* Setting up and managing wallets.
* Safeguarding private keys.
* Purchasing cryptocurrency.
* Understanding and paying transaction fees.

These complexities can hinder user adoption, particularly among individuals unfamiliar with blockchain concepts. For developers, this limits the potential user base, as onboarding non-technical users becomes increasingly difficult.

The result is a lack of growth in user numbers, with blockchain ecosystems primarily catering to technically proficient individuals. This issue is contrary to the ease-of-use principles widely embraced in Web 2.0 and the mobile app era.

VIP-191 addresses these challenges by enabling a frictionless user experience, where users can interact with dApps without requiring a detailed understanding of blockchain fees. This enhances accessibility and encourages broader adoption.

### Key Use Cases for VIP-191 <a href="#key-use-cases-for-vip-191" id="key-use-cases-for-vip-191"></a>

The following are examples of scenarios where VIP-191 fee delegation can be effectively utilized:

**1) Web Applications and Games**

A game that leverages VeChain as a database for tracking points or progress would typically require users to pay VTHO for transactions.

With VIP-191, developers can sponsor the transaction fees for new users as part of a promotion (e.g., a 3-day trial period). This allows users to try the application without needing prior knowledge of blockchain systems, improving accessibility and potentially increasing user engagement. Developers can later monetize the service through subscription models or other mechanisms.

<figure><img src="https://cdn-images-1.medium.com/max/2832/1*0r9a_RmPNJqKYrWSiA6ZTA.png" alt=""><figcaption><p><em>Example: Web-based games using VIP-191 for user onboarding.</em></p></figcaption></figure>

**2) Logistics and Supply Chain Management**

In industries such as shipping and logistics, blockchain is often used to track cargo movement. Employees at various checkpoints (e.g., customs clearance, shipping, and inspection) may need to interact with smart contracts, incurring transaction fees.

With VIP-191, a centralized management team can sponsor these fees using a corporate wallet. This eliminates the need for employees to manage wallet balances or tokens, improving security and operational efficiency.

<figure><img src="https://cdn-images-1.medium.com/max/3252/1*yMF-aQQtSHU1PfIlKOd2mA.png" alt=""><figcaption><p><em>Example: Logistics companies using VIP-191 for streamlined operations.</em></p></figcaption></figure>

### How VIP-191 Works <a href="#how-vip-191-works" id="how-vip-191-works"></a>

VIP-191 introduces a modified transaction signature mechanism. Normally, a valid transaction contains a signature from the sender. Under VIP-191, the transaction includes a composite signature, formed by combining the user’s signature and the sponsor’s signature.

The process is as follows:

1. The user creates a transaction and signs it.
2. The sponsor signs the transaction hash, including metadata specifying for whom the fees are being covered.
3. The two signatures are concatenated and sent to the VeChain network along with the transaction data.

<figure><img src="https://cdn-images-1.medium.com/max/3412/1*EqQX-xtv6RLNb0t1nUQCdQ.png" alt=""><figcaption><p><em>How VIP-191 signatures are constructed.</em></p></figcaption></figure>

### Next Steps <a href="#next-steps" id="next-steps"></a>

This document outlined the purpose and applications of VIP-191 Fee Delegation. The next section will provide a step-by-step guide for implementing VIP-191 in your dApp workflow.

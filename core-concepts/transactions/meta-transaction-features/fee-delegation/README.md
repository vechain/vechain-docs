---
description: >-
  Vechain provides two approaches for fee delegation on the VechainThor
  blockchain.
---

# Fee Delegation

## Introduction <a href="#multi-party-payment-prototype" id="multi-party-payment-prototype"></a>

Fee delegation is a feature on the VechainThor blockchain which enables the transaction sender to request another entity, a sponsor, to pay for the transaction fee on the sender's behalf. Fee delegation greatly improves the user experience, especially in the case of onboarding new users by removing the necessity of the user having to first acquire cryptocurrency assets before being able to interact on-chain.

The purpose of this document is to provide a high-level introduction to both fee delegation protocols and to compare and contrast them. Further detail is provided on both fee delegation protocols in subsequent documents.

{% hint style="info" %}
Additional detail and documentation is provided in the supplementary sections:

* [multi-party-payment-mpp.md](multi-party-payment-mpp.md "mention")
* [designated-gas-payer-vip-191.md](designated-gas-payer-vip-191.md "mention")
{% endhint %}

## Fee Delegation Protocols <a href="#multi-party-payment-prototype" id="multi-party-payment-prototype"></a>

The VechainThor blockchain offers two protocols for implementing fee delegation, multi-party payment (MPP) and designated gas payer (VIP-191). Both fee delegation protocols achieve the same goal of delegating the transaction fee from the transaction sender to a designated sponsor. The difference between both protocols is the implementation and the use cases.

## Multi-Party Payment (MPP) <a href="#multi-party-payment-prototype" id="multi-party-payment-prototype"></a>

MPP is a native protocol on the VechainThor blockchain. MPP enables the sender of a transaction to request that a sponsor or the receiver of the transaction pays the transaction fee on the senders behalf. MPP is a fee delegation approach which is implemented on the smart contract level. This means that data must be written on-chain, which comes at a cost. It is more cost effective to use the MPP protocol for frequent interactions between users and a decentralized application (dApp). An example of MPP implementation could be a marketplace or game which has opted to pay for all users transaction fees.

## Designated Gas Payer (VIP-191) <a href="#designated-gas-payer-vip191" id="designated-gas-payer-vip191"></a>

The designated gas payer is a standard which has been implemented on the VechainThor blockchain, through VIP-191, which extends the MPP functionality in a more flexible way. VIP-191, allows a transaction sender to seek for an arbitrary party to pay the transaction fee on the sender's behalf. An example of VIP-191 implementation could be to implement a transaction fee sponsor for users that are performing a particular action such as minting an NFT at an event or awarding the highest points scorer on a game with sponsored transactions.&#x20;

## Conclusion

Both fee delegation protocols achieve a common goal of allowing a transaction sender to delegate the transaction fee to a sponsor. However, both protocols are implemented in different ways.

The MPP implementation is at a smart contract level and thus comes with a cost. Including MPP within a smart contract will increase the size of the smart contract which will requires more space and thus will have a larger cost when it comes to deploying the smart contracts on the VechainThor blockchain. The MPP approach to fee delegation is worthwhile if you intend to sponsor all user transactions for a set of smart contracts which form a decentralized application (dApp).

VIP-191 is a more flexible fee delegation approach which moves the fee delegation feature from the smart contract to the transaction itself. A user when sending a transaction can provide a sponsor who will sponsor the transaction fee on the sender's behalf. However, VIP-191 requires that both the transaction sender and sponsor are both online for the transaction to be completed. This is not the case for MPP as it is implemented at a smart contract level.

Both fee delegation protocols have their specific use cases and it is up to the developer to determine which fee delegation protocol best suits their needs. Please read the following articles and subsequent documents for deeper information on both fee delegation protocols.

{% hint style="info" %}
Some useful articles to read on this subject include:

* [This MPP article](https://peter-zhou.medium.com/what-you-might-not-know-about-vechainthor-yet-part-iii-transaction-fee-delegation-vip-191-4ee71d690f1b)
* [This VIP-191 article](https://blog.vechain.energy/how-to-setup-fee-delegation-for-vechain-9ac9fef31455)
{% endhint %}

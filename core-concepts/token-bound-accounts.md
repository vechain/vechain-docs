---
description: >-
  An interface and registry that allows ERC-721 and ERC-1155 tokens to have
  their own smart contract accounts.
---

# Token Bound Accounts

{% hint style="warning" %}
The implementation of token bound accounts is work in progress. Hence, this material is subject to change.
{% endhint %}

## TL;DR

Token Bound Accounts (TBAs) enhance the functionality of new and existing NFTs by equipping them with smart contract accounts. TBAs can be used to interact with decentralized applications (dApps), receive, store or transfer digital assets, either fungible or non-fungible. TBAs are backwards compatible with the ERC-721 and ERC-1155 standards, meaning existing non-fungible tokens (NFTs) can implement ERC-6551 without undergoing any fundamental changes.

## Introduction

Token Bound Accounts (TBAs) allow ERC-721 and ERC-1155 tokens to have their own smart contract accounts. This means that non-fungible tokens (NFTs) can own and interact with digital assets, either fungible or non-fungible, and interact with decentralized applications (dApps). There are several implementations of the TBA standard. When we refer to TBAs were are referring to the ERC-6551 standard implementation.

## Token Bound Account Use Cases

TBAs allow ERC-721 and ERC-1155 tokens to have their own smart contract account which opens a range of potential use cases:

* **Identity**: Individuals can utilise a TBA enabled NFT as their on-chain identity.
* **Metaverse**: By utilising a TBA enabled NFT as their on-chain identity the user can enter and interact in the metaverse as their NFT avatar.
* **Membership / DAO Management**: Soul bound tokens, rewards or proof of participation (PoP) tokens are sent to the decentalized autonomous organization (DAO) TBA NFT instead of a user account.
* **Composability**: A TBA can be an inventory system holding different types of digital assets. For example, you could equip an NFT with different clothing or accessories which could provide your NFT with different abilities.
* **Gaming**: Your TBA enabled NFT holds your in game assets. You can customise your NFT with different gear or equipment giving it different capabilities or abilities.

## How Token Bound Accounts Work

Token Bound Accounts are formalized through ERC-6551 If you wish to read more on how it works the following resources are a good starting point:

* [Official ERC-6551 Ethereum Site](https://eips.ethereum.org/EIPS/eip-6551)

### ERC-6551: Registry

The registry is permissionless and immutable, and it deploys a smart contract account for an NFT.

### ERC-6551: Account Interface

The account interface sets the standard process, rules, and limits for account creation.

### ERC-6551: Proxy

ERC-1167 minimal proxy contracts are used in deploying accounts, making account implementations much easier and cheaper.

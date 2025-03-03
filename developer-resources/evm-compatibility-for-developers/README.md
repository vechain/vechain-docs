---
description: >-
  This document provides an overview of VeChainThor's compatibility with the
  Ethereum Virtual Machine (EVM), highlighting differences, benefits, supported
  RPC methods, and considerations for developers
---

# EVM Compatibility for Developers

#### 1. Introduction: EVM Compatibility and VeChain's Enterprise Focus

VeChainThor development started from a fork of the go-ethereum client, and from its inception, was designed to be EVM compatible. The commitment to EVM compatibility means VeChainThor is built to readily execute Ethereum-based smart contracts, aiming to bridge the gap for developers familiar the Ethereum ecosystem. VeChain is dedicated to incorporating new upgrades, continually striving to minimize any divergence and maintain a high degree of alignment with the evolving Ethereum standard. This strategic approach allows developers to easily transition to VeChainThor, leveraging their existing knowledge of:

* **Solidity:** The primary smart contract language for Ethereum.
* **Development Tools:** Tools like Hardhat, and Remix.
* **Development Patterns:** Established best practices for Ethereum dApp development.

This compatibility also streamlines the porting of existing Ethereum-based dApps and smart contracts to VeChainThor with zero to minimal adjustments.  However, it's crucial to understand that while VeChainThor offers strong EVM compatibility, it is not designed for strict EVM equivalence, which would aim for an identical replication of the Ethereum environment. Instead, VeChainThor strategically incorporates significant architectural optimizations and features tailored for enterprise adoption and real-world use cases.

---
description: >-
  An optional actor within the account abstraction flow that can be used to pay
  gas fees on behalf of the user or accept a different token as payment for gas
  fees.
---

# Paymaster Contract

## Overview

A Paymaster, another optional entity in the account abstraction flow, is a contract designed to sponsor user transactions based on specific criteria. Typically, users pay their own transactions fees. However, by filling the `paymasterAndData` field in their UserOperation, users can opt for a Paymaster to sponsor their transactions.

Sponsorship of transactions comes in two forms. The Paymaster can opt to pay the gas fee for a user transaction or the Paymaster can accept a different token, perhaps a stablecoin, and pay the fee on the users behalf in the blockchains required gas fee token. Both of these approaches will contribute towards an enhanced user experience by either abstracting gas fees entirely or removing the requirement of a user having to hold or fund a smart contract wallet with the blockchain native currency.

## Role

During the EntryPoint contracts verification loop, the UserOperation is passed to the selected Paymaster contract, who then decides to either approve or reject the request. If approved, the Paymaster contract refunds the required gas to the EntryPoint contract, a task typically done by the Account contract.

## Implementation

Each Paymaster contract is an individually deployed and configured contract.

To safeguard against potential system disruption by malicious Paymaster contracts, a staking mechanism is implemented in the EntryPoint to measure their reputation. To deter sybil attacks, Paymaster contracts must first deposit a stake to become part of the system.

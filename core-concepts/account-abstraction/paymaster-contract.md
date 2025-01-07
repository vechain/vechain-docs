---
description: >-
  An optional actor within the account abstraction flow that can be used to pay
  gas fees on behalf of the user or accept a different token as payment for gas
  fees.
---

# Paymaster Contract

## Overview

The Paymaster is an optional but significant component in the account abstraction flow. It acts as a sponsor for user transactions under specific conditions. Traditionally, users are required to pay transaction fees using the blockchain’s native token. However, by leveraging the `paymasterAndData` field in a UserOperation, users can designate a Paymaster to cover these fees on their behalf.

## Sponsorship Models

A Paymaster can support transactions in two primary ways:

1. **Gas Fee Sponsorship**: The Paymaster directly pays the gas fees for a user transaction, abstracting the fee payment process entirely.

2. **Alternative Token Payment**: The Paymaster accepts payment in an alternate token (e.g., stablecoins) and then converts it to the native gas token to pay the transaction fee.

These mechanisms enhance the user experience by removing the requirement for users to hold native tokens or by simplifying the fee payment process.

## Role

During the EntryPoint contracts verification loop, the UserOperation is passed to the selected Paymaster contract, who then decides to either approve or reject the request. If approved, the Paymaster contract refunds the required gas to the EntryPoint contract, a task typically done by the Account contract.

## Implementation

Each Paymaster contract is an individually deployed and configured contract.

To safeguard against potential system disruption by malicious Paymaster contracts, a staking mechanism is implemented in the EntryPoint to measure their reputation. To deter sybil attacks, Paymaster contracts must first deposit a stake to become part of the system.

---
description: Bespoke contracts for scaffolding and creating smart contract wallets.
---

# Account Factory Contract

## Overview

The AccountFactory contract is primarily used to create Account contracts that represent a user's account in a blockchain network, differing from traditional externally owned accounts (EOAs). It has two main functions: aiding client code in pre-generating the Account contract address to facilitate pre-funding, and assisting the EntryPoint contract in deploying the Account contract when the first UserOperation associated with a given account is transmitted.

Account Factory contracts are not uniform. They differ based on the type of Account contract and the specific logic they implement. For instance, a common type is the `SimpleAccountFactory`, which creates Account contracts that behave similar to EOAs. However, these accounts offer additional functionalities, like conducting batch transfers and handling ERC-20 token transfers, adding to their flexibility and versatility.

## Role

The Account Factory contract plays a crucial role in the lifecycle of a UserOperation:

* **Initialization with initCode**: When a UserOperation includes the initCode field, the EntryPoint contract invokes the Account Factory contract to deploy the corresponding Account contract.
* **Seamless Integration**: Ensures the created Account contract adheres to the required interface for subsequent operations.

## Implementation

Each Account Factory contract is independently deployed and configured, tailored to the specific requirements of the associated Account contract. Smart contract wallet providers may implement distinct features to offer competitive advantages.

### Example: SimpleAccountFactory Interface

In the code snippet below there are two main functions of the `SimpleAccountFactory` helper contract. The `createAccount()` method is used by the EntryPoint contract to deploy the Account contract and the `getAddress()` method is used by the client side code to generate the Account contract address.

```solidity
/**
 * create an account, and return its address.
 * returns the address even if the account is already deployed.
 * Note that during UserOperation execution, this method is called only if the account is not deployed.
 * This method returns an existing account address so that entryPoint.getSenderAddress() would work even after account creation
 */
function createAccount(address owner,uint256 salt) public returns (SimpleAccount ret);

/**
 * calculate the counterfactual address of this account as it would be returned by createAccount()
 */
function getAddress(address owner,uint256 salt) public view returns (address);
```

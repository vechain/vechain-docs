---
description: >-
  A singleton entry point contract to verify and execute bundles of
  UserOperations.
---

# EntryPoint Contract

## Overview

The EntryPoint contract is a singleton contract that acts as a "guard" or "entry point" to account abstraction. Bundlers that receive signed UserOperations pass them to the EntryPoint contract in the `handleOps` public method. The EntryPoint contract then uses the Account contract to verify the `signature` of the UserOperation, which could include any additional arbitrary logic, and if valid proceeds to execute it on chain. A more detailed step-by-step process of the EntryPoint role can be found below.

## Role

The role of the EntryPoint contract is to handle the verification and execution logic of transactions.

Below is an example flow of a transaction focusing on the EntryPoint contract.

1. The Bundler listens for UserOperations and calls the `EntryPoint.simulateVerification()` function for the UserOperation. If the verification simulation is successful the process continues to the next step.
2. The Bundler calls the `EntryPoint.handleOps()` function which triggers the verification and execution loop performed by the EntryPoint contract.
3. If this is the first time the account has made a transaction, the EntryPoint contract will use the `userOperation.initCode` field to deploy the Account contract via the Account Factory contract.
4. Now that the Account contract is deployed the EntryPoint contract will call `Account.validateUserOp()` passing in the UserOperation as a parameter. The account is responsible for verifying the `signature` which could potentially have arbitrary verification logic such as social recovery, muti-signature, etc.
5. The EntryPoint contract passes the fee in the `Account.validateUserOp()` and if it is a valid UserOperation the Account contract pays the fee back to the EntryPoint contract. If there is a Paymaster involved then the Paymaster will be asked to pay the fee by the EntryPoint contract by running `Paymaster.validatePaymasterUserOp()` to verify that the Paymaster is willing to pay the fee.
6. If that verification step passes, finally, the EntryPoint contract calls the account contract with `UserOperation.callData`. Which executes the user’s intent as a transaction.

## Implementation

As the EntryPoint contract is a singleton contract there only exists a single implementation and deployment of the contract on the VechainThor blockchain mainnet and testnet.

<table><thead><tr><th width="132">Network</th><th>Address</th></tr></thead><tbody><tr><td>Mainnet</td><td>0xeE8A9E01A08bbdf3586dFa97d15aCA174DFc4d29</td></tr><tr><td>Testnet</td><td>0xf9188E94783Ca505886488F04249DD7f6a36770B</td></tr></tbody></table>

### Vechain EntryPoint Contract Modifications

The EntryPoint contract was developed for the Ethereum blockchain. Given vechain has some modifications that are not present in Ethereum it is expected that the EntryPoint contract requires some modifications to be interoperable with vechain.

The most significant modification to implementing account abstraction on vechain is to adjust the smart contracts to accommodate for the vechain [two-token design](https://github.com/vechain/vechain-docs/blob/main/core-concepts/account-abstraction/broken-reference/README.md) which is in contrast to the single asset ETH on Ethereum. On Ethereum, all account abstraction participants spend and are compensated in ETH, the native token of Ethereum. Whereas, on vechain the account abstraction participants are modified to accept VTHO, the vechain gas token, instead of VET, the vechain utility token, by adding additional VTHO-equivalent methods.

The EntryPoint contract was modified to accept VTHO instead of VET by adding additional VTHO-equivalent methods to its public interface and subsequently the BaseAccount and Paymaster were modified to reimburse VTHO instead of VET back to the EntryPoint contract using these new methods.

### StakeManager Modifications

Modifications were made to the StakeManager contract which the EntryPoint contract inherits from. The purpose of the modifications to the StakeManager contract was to use the VTHO asset instead of the VET asset. Modifications were made to all methods that were payable to not payable since we do not require the Account contract or the Paymaster contract to deposit VET. We also added `depositAmount()` and `addStakeAmount()` alongside `deposit()` and `addStake()` such that the Account contract or Paymaster contract can deposit a specific amount and not all of their VTHO allowance.

The changes to the StakeManager interface can be found below:

```diff
-    /**
-     * add to the deposit of the given account
-     */
-    function depositTo(address account) external payable;
+    /// Deposit the full amount of VTHO approved by the sender, to the specified account
+    function depositTo(address account) external;
 
-    /**
-     * add to the account's stake - amount and delay
-     * any pending unstake is first cancelled.
-     * @param _unstakeDelaySec the new lock duration before the deposit can be withdrawn.
-     */
-    function addStake(uint32 _unstakeDelaySec) external payable;
+    /// Deposit a fixed amount of VTHO approved by the sender, to the specified account
+    function depositAmountTo(address account, uint256 amount) external;
+
+    /// Stake the full amount of VTHO approved by the sender
+    function addStake(uint32 _unstakeDelaySec) external;
+
+    /// Stake a fixed amount of VTHO approved by the sender
+    function addStakeAmount(uint32 _unstakeDelaySec, uint256 amount) external;
```

The new StakeManager interface can be found below:

```solidity
// Modified StakeManager.sol Interface

/// @return info - full deposit information of given account
function getDepositInfo(address account) external view returns (DepositInfo memory info);

/// @return the deposit (for gas payment) of the account
function balanceOf(address account) external view returns (uint256);

/// Deposit the full amount of VTHO approved by the sender, to the specified account
function depositTo(address account) external;

/// Deposit a fixed amount of VTHO approved by the sender, to the specified account
function depositAmountTo(address account, uint256 amount) external;

/// Stake the full amount of VTHO approved by the sender
function addStake(uint32 _unstakeDelaySec) external;

/// Stake a fixed amount of VTHO approved by the sender
function addStakeAmount(uint32 _unstakeDelaySec, uint256 amount) external;
```

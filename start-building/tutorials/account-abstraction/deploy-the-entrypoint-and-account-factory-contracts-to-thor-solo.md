---
description: >-
  This guide describes how to deploy the Entrypoint and AccountFactory smart
  contracts.
---

# Deploy the EntryPoint and Account Factory Contracts to Thor Solo

## Prerequisites

Run a thor solo node. Follow the guide [how-to-run-a-thor-solo-node](../how-to-run-a-thor-solo-node/ "mention")

## Clone the repo

```bash
git clone -b vechain https://github.com/vechain/account-abstraction.git
```

## Deploy the contracts

```bash
yarn hardhat test --network vechain test/deploy-contracts.test.ts
```

Update [./test/config.ts](https://github.com/vechain/account-abstraction/blob/vechain/test/config.ts) with the addresses of the deployed contracts and

## Run the tests

### EntryPoint Tests
```bash
yarn hardhat test test/entrypoint.test.ts --network vechain
```

### Paymaster Tests
```bash
yarn hardhat test test/paymaster.test.ts --network vechain
```

### Simple Wallet Tests
```bash
yarn hardhat test test/simple-wallet.test.ts --network vechain
```

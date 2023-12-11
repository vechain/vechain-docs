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
git clone https://github.com/eth-infinitism/account-abstraction/tree/v0.6.0
```

## Initialise and add vechain specific dependencies&#x20;

Initialize the cloned directory and add vechain Ethers plugins for Hardhat

```bash
yarn && yarn add -D @vechain/hardhat-vechain @vechain/hardhat-ethers
```

## Configure `hardhat.config.ts`

```typescript
import { VECHAIN_URL_SOLO } from "@vechain/hardhat-vechain";
import "@vechain/hardhat-ethers";

module.exports = {
    ...
    networks: {
        ...
        vechain: { url: VECHAIN_URL_SOLO }
    }
}
```

## Create `test/DeployContracts.test.ts` :

```typescript
const EntryPoint = artifacts.require('EntryPoint');
const SimpleAccountFactory = artifacts.require('SimpleAccountFactory');
const MyPaymaster = artifacts.require('MyPaymaster');
const { expect } = require('chai');
​
contract('Deployments', function (accounts) {
    it('Adresses', async function () {
        this.EntryPoint = await EntryPoint.new({ from: accounts[0] });
        this.SimpleAccountFactory = await SimpleAccountFactory.new(this.EntryPoint.address, { from: accounts[0] });
        this.MyPaymaster = await MyPaymaster.new(this.EntryPoint.address, { from: accounts[0], value: 10000 });
        
        await this.MyPaymaster.deposit({ from: accounts[0], value: 10000 });
        
        console.log("    EntryPoint address:           ", this.EntryPoint.address)
        console.log("    SimpleAccountFactory address: ", this.SimpleAccountFactory.address)
        console.log("    MyPaymaster address:          ", this.MyPaymaster.address)
    });
​
});
```

## Run the deployment test

```bash
yarn test test/DeployContractsVTHO.test.ts --network vechain
```

After running the deployment tests you should see an output similar to the below. Your addresses for these contracts will differ from the contract address shown below. These are important addresses you will be referring back to these in the following tutorials.

```
  Contract: Deployments
    EntryPoint address:            0xDbA21aab0Fa0A58895D19a9C13f9400D98D4f418
    SimpleAccountFactory address:  0x0b15A724EFd206ae08452Ec99C3BAc2548e58FA3
    ✔ Adresses (10119ms)
  1 passing (10s)ba
```

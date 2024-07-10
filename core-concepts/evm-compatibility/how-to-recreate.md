---
description: >-
  A tutorial on how to recreate the OpenZeppelin tests locally using a Thor Solo
  node.
---

# How to Recreate

## Run a Thor Solo Node

Use the tutorial [how-to-run-a-thor-solo-node](../../start-building/how-to-run-a-thor-solo-node/ "mention") to start up a thor solo node.

## Configure a Development Environment (OZ4)

### Clone openzeppelin-contracts

```bash
git clone git@github.com:OpenZeppelin/openzeppelin-contracts.git
cd openzeppelin-contracts
```

### Install the required VeChain libraries

```bash
npm install @vechain/hardhat-vechain@0.0.1 --save-exact
npm install @vechain/hardhat-web3@0.0.1 --save-exact
npm install @vechain/web3-providers-connex@1.0.0 --save-exact
```

### Modify your hardhat.config.js

Add the following to your hardhat config

```javascript
require("@vechain/hardhat-vechain");
require("@vechain/hardhat-web3");
```

Add the VeChain network settings

```javascript
   vechain: {
      url: "http://127.0.0.1:8669",
      accounts: {
        mnemonic: "denial kitchen pet squirrel other broom bar gas better priority spoil cross",
        count: 10,
      },
      restful: true,
      gas: 10000000,
      delegate: {
        url: "hello",
        signer : "world"
      },
    },
```

## Configure a Development Environment (OZ5)

### Clone openzeppelin-contracts

```bash
git clone -b thor-compatibility git@github.com:vechain/openzeppelin-contracts.git
cd openzeppelin-contracts
```

## Run the OpenZeppelin Tests

Assuming you have cloned OpenZeppelin and are running thor locally in solo mode we can now move on to running the OpenZeppelin tests. First navigate to the appropriate directory.

```bash
cd openzeppelin-contracts
```

### Run a single test

```bash
npx hardhat test --network vechain test/access/AccessControlEnumerable.test.js
```

### Run all tests

```bash
npx hardhat test --network vechain
```
or in case of OZ5
```bash
npm run test:solo
```

### Run all tests in a specific directory (OZ5)
```bash
npm run test:solo:dir <dir_relative_path>
```

### Expectation
- [OZ4] After running a given number of tests a `*.csv` file with the results of the tests will appear under openzeppelin-contracts folder;
- [OZ5] All tests are expected to pass as is.

### OpenZeppelin v5
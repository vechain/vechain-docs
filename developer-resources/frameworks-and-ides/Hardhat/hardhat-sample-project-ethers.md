# Hardhat Sample Project (Ethers)

## Prerequisites

```bash
git
npm
typescript
```

## Setup

First, clone the sample project from our repository

```bash
git clone git@github.com:vechain/hardhat-plugin-sample-ethers.git
cd hardhat-plugin-sample-ethers
```

Then install the required node modules by running

```bash
npm install
```

### Install VeChain's Web3 library

```bash
npm i @vechain/web3-providers-connex
```

### Install VeChain's Hardhat plugin

```bash
npm i @vechain/hardhat-vechain
npm i @vechain/hardhat-ethers
```

## Start Thor

To be able to run the tests on VeChain you need Thor installed, which is VeChain's node implementation. We have a detailed guide on how to do that [here](https://app.gitbook.com/).

## Running the tests

```bash
npx hardhat test --network vechain
```

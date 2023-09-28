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
git clone git@github.com:vechainfoundation/hardhat-plugin-sample-ethers.git
cd hardhat-plugin-sample-ethers
```

Then install the required node modules by running

```bash
npm install
```

### Install Vechain's Web3 library

```bash
npm i @vechain/web3-providers-connex
```

### Install Vechain's Hardhat plugin

```bash
npm i @vechain/hardhat-vechain
npm i @vechain/hardhat-ethers
```

## Start Thor

To be able to run the tests on Vechain you need Thor installed, which is Vechain's node implementation. We have a detailed guide on how to do that [here](https://app.gitbook.com/).

## Running the tests

```bash
npx hardhat test --network vechain
```

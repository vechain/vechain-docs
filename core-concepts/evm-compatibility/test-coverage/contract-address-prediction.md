# Contract address prediction

## Description

Some contracts require another contract's address in their constructor. For various reasons the required contract instance might not be deployed at the time when our contract is being deployed. Thus, we need a way to predict or pre-generate the required contract's address before its deployed. Since Openzeppelin was written for Ethereum, the contract prediction code takes into account how Ethereum addresses are generated. But since VeChain differs in that regard some tests fail since the predicted address is wrong and there is no deployed contract in that address. Specifically, the address of a contract is predicted by incrementing the nonce of an address which can be obtained by the web3 plugin:

```javascript
const nonce = await web3.eth.getTransactionCount(deployer);
const predictGovernor = makeContractAddress(deployer, nonce + 1);
```

Unfortunately, VeChain's `web3-providers-connex` library does not yet support getting the transaction count for an address. Thus, we have to manually set the address after the contract is deployed. See below which contracts are affected.

## Contracts Affected

| Contract Name              |
| -------------------------- |
| GovernorTimelockCompound   |
| GovernorCompatibilityBravo |

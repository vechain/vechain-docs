# evm\_increaseTime

## Description

`evm_increaseTime` is a feature supported by both Ganache and Hardhat. The basic idea is that we can artificially increase time to some future point manually. This is useful when we are testing contracts that use time-locks, and it is not practical to wait for months on end for a test to finish. Unfortunately, since our plugin is connected to `thor`, which is a real blockchain implementation and not a testing framework like Ganache or Hardhat, this feature is not supported. This is inherent to all blockchains not just VeChain.

## Contracts Affected

| Contract Name           |
| ----------------------- |
| GovernorTimelockControl |
| TimelockController      |
| TokenTimelock           |
| TimersTimestamp         |

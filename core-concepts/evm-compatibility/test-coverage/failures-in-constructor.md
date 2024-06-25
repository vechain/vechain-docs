# Failures in constructor

## Description

This type of error happens due to the fact that something in the contract's constructor prevents it from being deployed as it fails while running the constructor. This is different from other types of errors where the problem occurs on a test after a contract has been deployed. In this case the error is more severe as the contract fails to be deployed.

## Contracts Affected

| Contract Name               |
|-----------------------------|
| BeaconProxy                 |
| ERC1967Proxy                |
| TransparentUpgradeableProxy |

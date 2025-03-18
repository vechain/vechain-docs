# Gas model

## Description

These errors are justifiable as they occur due to VeChain and Ethereum having different gas models and the tests being designed with Ethereum's gas model in mind. When these transactions are performed on VeChain the maximum amount of gas set by the test is exceeded, hence the failure. The tests are passable when the tests are modified to account for a higher maximum amount of gas.

## Contracts Affected

| Contract Name                  |
| ------------------------------ |
| ERC165                         |
| ERC165Storage                  |
| AccessControl                  |
| ERC1155Holder                  |
| ERC721Enumerable               |
| TimelockController             |
| ERC721                         |
| ERC1155PresetMinterPauser      |
| ERC1155                        |
| Governor                       |
| ERC721PresetMinterPauserAutoId |
| ERC721Royalty                  |
| ERC721Enumerable               |
| GovernorTimelockCompound       |
| GovernorTimelockControl        |

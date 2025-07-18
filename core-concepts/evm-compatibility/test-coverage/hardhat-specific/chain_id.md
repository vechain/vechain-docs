# Chain ID

## Description

In VeChain, the ChainTag is equivalent to ChainID in Ethereum. Both of them will return a shorter string.
However in VeChain EVM,the opconde `block.chainid` will return the genesis block id with a length of 32 bytes.

This difference will cause the `eip712Domain` hex values of the contract and the local computation in the EIP712 test cases to be different.

Therefore, we modified the test code. When calculating the `eip712Domain` locally, instead of directly using the value returned by the `eth_chainId` PRC interface, we used `eth_getBlockByNumber` to obtain the ID of the genesis block to ensure that the hex value of eip712Domain is the same.

## Contracts Affected

| Contract Name                  |
|--------------------------------|
| EIP712                         |
# Chain ID

## Description

In the VeChain EVM, the `block.chainid` opcode returns the 32-byte genesis block ID, which represents a significantly larger value than the typical `chainId` used in other EVM-compatible networks.

This difference will cause the `eip712Domain` hex values of the contract and the local computation in the EIP712 test cases to be different.

Therefore, we modified the test code. When calculating the `eip712Domain` locally, instead of directly using the value returned by the `eth_chainId` RPC interface, we used `eth_getBlockByNumber` to obtain the ID of the genesis block to ensure that the hex value of `eip712Domain` is the same.

## Contracts Affected

| Contract Name                  |
|--------------------------------|
| ERC712                         |
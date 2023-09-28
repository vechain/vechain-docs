# Web3-Providers-Connex

The web3-providers-connex library implements the JSON-RPC provider defined in [EIP-1193](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1193.md) for the VechainThor blockchain. The provider is compatible with [web3.js](https://github.com/ChainSafe/web3.js) and [ethers.js](https://github.com/ethers-io/ethers.js), allowing developers to use both libraries to interact with the VechainThor blockchain, via Connex.

{% hint style="info" %}
Available on GitHub [here](https://github.com/vechain/web3-providers-connex).
{% endhint %}

## Key Features

The web3-providers-connex library offers a wide range of functionalities related to the VechainThor blockchain and dApp development. Some of the key features include:

1. **web3.js support**: web3-providers-connex enables developers to interact with the VechainThor blockchain with the familiar web3.js library.
2. **ethers.js support**: web3-providers-connex enables developers to interact with the VechainThor blockchain with the familiar ethers.js library.
3. **Supports all of the key features of Connex**:
   1. **Blocks and node status**: The library enables developers to interact with and retrieve information about blocks on the VeChainThor blockchain. This includes accessing block data and querying the status of connected VeChain nodes.
   2. **Accounts**: Facilitates interactions with Externally Owned Accounts (EOAs), allowing developers to manage and transact with individual user accounts on the VeChainThor blockchain. This includes sending VET tokens and interacting with VTHO (VeThor) tokens.
   3. **Smart Contracts**: Developers can interact with and manage smart contracts deployed on the VeChainThor blockchain. This includes deploying smart contracts, invoking their functions, and retrieving contract data.
   4. **Transactions**: Create and broadcast transactions on the VeChainThor blockchain. Developers can initiate various transactions, such as token transfers, contract interactions, and asset management.
   5. **Certificates**: Manage certificates and certificate-related operations on the blockchain. Certificates are often used for identity verification and access control in dApps.
   6. **Queries**: Efficiently query the VechainThor blockchain. This includes querying transaction details, contract state, and other relevant blockchain information for dApp development.

## Online Functionality

web3-providers-connex serves as an "online" library, primarily used for dApp development and blockchain-related operations that can be performed online. For example, users can use web3-providers-connex to create, sign and broadcast transactions to the VechainThor blockchain network.

## License

web3-providers-connex is licensed under the GNU Lesser General Public License v3.0 (LGPL-3.0). The full text of the license can be found in the _LICENSE_ file included in the [repository](https://github.com/vechain/web3-providers-connex/blob/main/LICENSE).

The GNU Lesser General Public License v3.0 is an open-source license that grants users the freedom to use, modify, and distribute the software under certain conditions. It ensures that users have access to the source code, can make improvements, and distribute their modifications while also preserving the rights of the original authors.

For more details about the GNU Lesser General Public License v3.0, please visit the [GNU website](https://www.gnu.org/licenses/lgpl-3.0.html).

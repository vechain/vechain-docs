# Connex

Connex is the standard interface to connect decentralized applications (dApps) and users with the VeChainThor blockchain. This documentation provides a comprehensive guide to using the Connex library, including installation, usage instructions, and details about its key features and methods.

Connex can be utilized through two distinct methodologies: as a Browser application or as a conventional Command Line Interface (CLI) application.

{% hint style="info" %}
Available on GitHub [here](https://github.com/vechainfoundation/connex).
{% endhint %}

## Source Code <a href="#source-code" id="source-code"></a>

Connex is available through several interfaces:

* [connex](https://github.com/vechain/connex/blob/master/packages/connex): Standard Connex implementation for the browser.
* [framework](https://github.com/vechain/connex/blob/master/packages/framework): Implements Connex interface.
* [driver](https://github.com/vechain/connex/blob/master/packages/driver): Implements Connex.Driver interface.
* [repl](https://github.com/vechain/connex/blob/master/packages/repl): The REPL style command-line playground.
* [types](https://github.com/vechain/connex/blob/master/packages/types): Connex interface declarations presented in Typescript.

## Key Features

The Connex library offers a wide range of functionalities related to the VeChainThor blockchain and dApp development. Some of the key features include:

1. **Blocks and node status**: The library enables developers to interact with and retrieve information about blocks on the VeChainThor blockchain. This includes accessing block data and querying the status of connected VeChain nodes.
2. **Accounts**: Connex facilitates interactions with Externally Owned Accounts (EOAs), allowing developers to manage and transact with individual user accounts on the VeChainThor blockchain. This includes sending VET tokens and interacting with VTHO (VeThor) tokens.
3. **Smart Contracts**: With Connex, developers can interact with and manage smart contracts deployed on the VeChainThor blockchain. This includes deploying smart contracts, invoking their functions, and retrieving contract data.
4. **Transactions**: Connex provides the capability to create and broadcast transactions on the VeChainThor blockchain. Developers can initiate various transactions, such as token transfers, contract interactions, and asset management.
5. **Certificates**: Connex supports the management of certificates and certificate-related operations on the blockchain. Certificates are often used for identity verification and access control in dApps.
6. **Queries**: The library offers a querying system that allows developers to retrieve specific data from the blockchain efficiently. This includes querying transaction details, contract state, and other relevant blockchain information for dApp development.

## Online Functionality

Connex serves as an "online" library, primarily used for dApp development and blockchain-related operations that can be performed online. For example, users can use Connex to create, sign and broadcast transactions to the VeChainThor blockchain network.

## License

Connex is licensed under the GNU Lesser General Public License v3.0 (LGPL-3.0). The full text of the license can be found in the _LICENSE_ file included in the [repository](https://github.com/vechain/connex/blob/master/LICENSE).

The GNU Lesser General Public License v3.0 is an open-source license that grants users the freedom to use, modify, and distribute the software under certain conditions. It ensures that users have access to the source code, can make improvements, and distribute their modifications while also preserving the rights of the original authors.

For more details about the GNU Lesser General Public License v3.0, please visit the [GNU website](https://www.gnu.org/licenses/lgpl-3.0.html).

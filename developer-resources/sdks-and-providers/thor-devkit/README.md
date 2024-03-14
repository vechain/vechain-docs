# Thor DevKit

[Thor DevKit](https://github.com/vechain/thor-devkit.js) is a library specifically designed to aid in decentralized application (dApp) development on the VechainThor blockchain. This documentation provides a comprehensive guide to using the Thor DevKit library, including installation, usage instructions, and details about its key features and methods.

{% hint style="info" %}
An alternative [SDK](../sdk/README.md) is currently available as a beta release. The vechain SDK offers enhanced features, improved performance, and better compatibility with the latest developments on the VechainThor blockchain.
{% endhint %}

## Languages

The Thor DevKit library is available in the following languages:

* TypeScript
* Java
* C#
* Python

## Key Features

The Thor DevKit library offers a wide range of functionalities related to the VechainThor blockchain and dApp development. Some of the key features include:

1. **Hash Functions** and **Public Key Cryptography**: Thor DevKit provides essential hash functions and public key cryptography methods that are essential for secure blockchain operations. (blake2b256, keccak256, and secp256k)
2. **Accounts Handling**: The library offers tools to manage accounts and perform operations related to account management, including private key generation, mnemonic handling, and keystore encryption / decryption. (mnemonics and keystore)
3. **Transactions**: Thor DevKit enables users to build, sign, and manipulate transactions to interact with the VechainThor blockchain. Users can construct transactions with various clauses and gas settings. (transactions and ABI)
4. **Recursive Length Prefix (RLP)**: The library includes RLP encoding and decoding capabilities, which are essential for efficient data serialisation and deserialisation on the VechainThor blockchain.
5. **Certificates**: Thor DevKit supports the creation and verification of client-side self-signed certificates, enabling secure identification and validation processes.
6. **Bloom filter**: The Bloom filter is a highly efficient and space-efficient probabilistic data structure employed to enhance the speed and efficiency of element lookup within a given set. It operates by providing a mechanism to test whether an element is a member of the set, thus offering a valuable tool in numerous applications, including database management, network routing, and caching systems.

## Offline Functionality

Thor DevKit serves as an "offline" library, primarily used for dApp development and blockchain-related operations that can be performed offline. For example, users can use Thor DevKit to create and sign transactions offline. However, to broadcast transactions and interact with the blockchain, users will require Connex, which facilitates online blockchain interaction.

## License

Thor DevKit is licensed under the GNU Lesser General Public License v3.0 (LGPL-3.0). The full text of the license can be found in the _LICENSE_ file included in the [repository](https://github.com/vechain/thor-devkit.js).

The GNU Lesser General Public License v3.0 is an open-source license that grants users the freedom to use, modify, and distribute the software under certain conditions. It ensures that users have access to the source code, can make improvements, and distribute their modifications while also preserving the rights of the original authors.

For more details about the GNU Lesser General Public License v3.0, please visit the [GNU website](https://www.gnu.org/licenses/lgpl-3.0.html).

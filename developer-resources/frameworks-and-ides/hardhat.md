# Hardhat

[Hardhat](https://hardhat.org/) is a powerful, flexible development environment for Ethereum-based blockchain projects. It offers a comprehensive suite of tools for editing, compiling, debugging, and deploying smart contracts and decentralized applications (dApps). These components seamlessly integrate to create a robust ecosystem that supports the entire development lifecycle.

Our custom VeChain plugin extends Hardhat's capabilities to the VeChain blockchain, enabling our community to leverage this advanced toolset for VeChain-specific development. This integration allows developers to harness Hardhat's efficient workflows and powerful features while building on VeChain's innovative blockchain platform.

## Introduction

The VeChain SDK Hardhat Plugin seamlessly integrates Hardhat with the VeChain SDK, providing developers with a powerful toolset for smart contract development on the VeChainThor blockchain. This essential package streamlines the process of creating, testing, deploying, and interacting with smart contracts in the VeChain ecosystem.

## Installation and Setup

### Prerequisites

Ensure Hardhat is installed in your project:

```bash
yarn add --dev hardhat
npx hardhat
```

### Adding VeChain Support

*   Install the VeChain Hardhat plugin:

    ```bash
    yarn add @vechain/sdk-hardhat-plugin
    ```
*   Configure your `hardhat.config.ts`:

    ```javascript
    import '@vechain/sdk-hardhat-plugin';

    import { VET_DERIVATION_PATH } from '@vechain/sdk-core';
    import { type HttpNetworkConfig } from 'hardhat/types';

    const config: HardhatUserConfig = {
    solidity: {
        compilers: [
        {
            version: '0.8.20', // Specify the first Solidity version
            settings: {
                // Additional compiler settings for this version
                optimizer: {
                    enabled: true,
                    runs: 200
                },
                evmVersion: 'paris' // EVM version (e.g., "byzantium", "constantinople", "petersburg", "istanbul", "berlin", "london")
            }
        },
        ]
    },
    networks: {
        vechain_testnet: {
        // Testnet
        url: 'https://testnet.vechain.org',
        accounts: {
            mnemonic:
                'vivid any call mammal mosquito budget midnight expose spirit approve reject system',
            path: VET_DERIVATION_PATH,
            count: 3,
            initialIndex: 0,
            passphrase: 'vechainthor'
        },
        debug: true,
        delegator: undefined,
        gas: 'auto',
        gasPrice: 'auto',
        gasMultiplier: 1,
        timeout: 20000,
        httpHeaders: {}
    } satisfies HttpNetworkConfig,
    }
    };
    ```

> **Notice**: At the date of writing, VeChainThor EVM is aligned with Ethereum's at the `paris` hard fork. Set the [evmVersion](https://docs.soliditylang.org/en/latest/using-the-compiler.html#setting-the-evm-version-to-target) to `paris` if you are using solidity compiler version `0.8.20` or above.

### Networks

*   VeChain mainnet:

    ```
    vechain_mainnet: {
        // Mainnet
        url: 'https://mainnet.vechain.org',
        accounts: [
            '7f9290cc44c5fd2b95fe21d6ad6fe5fa9c177e1cd6f3b4c96a97b13e09eaa158'
        ],
        debug: false,
        delegator: undefined,
        gas: 'auto',
        gasPrice: 'auto',
        gasMultiplier: 1,
        timeout: 20000,
        httpHeaders: {}
    } satisfies HttpNetworkConfig
    ```
*   VeChain solo network:

    ```
    vechain_solo: {
        // Thor solo network
        url: 'http://localhost:8669',
        accounts: [
            '7f9290cc44c5fd2b95fe21d6ad6fe5fa9c177e1cd6f3b4c96a97b13e09eaa158'
        ],
        debug: false,
        enableDelegation: false,
        delegator: undefined,
        gas: 'auto',
        gasPrice: 'auto',
        gasMultiplier: 1,
        timeout: 20000,
        httpHeaders: {}
    } satisfies HttpNetworkConfig
    ```

### Example Usage

For a detailed example of integrating the VeChain SDK with Hardhat, visit our [apps/sdk-hardhat-integration directory](https://github.com/vechain/vechain-sdk-js/tree/main/apps/sdk-hardhat-integration). This repository contains a fully configured project demonstrating best practices and common use cases, serving as an excellent starting point for your VeChain development journey.

By leveraging this plugin, developers can harness the full potential of VeChainThor blockchain while benefiting from Hardhat's robust development environment. Happy coding!

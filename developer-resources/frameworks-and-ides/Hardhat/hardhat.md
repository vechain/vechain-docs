# Hardhat

## Introduction

The VeChain SDK Hardhat Plugin seamlessly integrates Hardhat with the VeChain SDK, providing developers with a powerful toolset for smart contract development on the VeChainThor blockchain. This essential package streamlines the process of creating, testing, deploying, and interacting with smart contracts in the VeChain ecosystem.

## Installation and Setup

### Prerequisites

Ensure Hardhat is installed in your project:

``` bash
yarn add --dev hardhat
npx hardhat
```

### Adding VeChain Support

 - Install the VeChain Hardhat plugin:

    ``` bash
    yarn add @vechain/sdk-hardhat-plugin
    ```

 - Configure your `hardhat.config.ts`:

    ``` typescript
    import '@vechain/sdk-hardhat-plugin';

    import { VET_DERIVATION_PATH } from '@vechain/sdk-core';
    import { type HttpNetworkConfig } from 'hardhat/types';

    const config: HardhatUserConfig = {
    solidity: {
        compilers: [
        {
            version: '0.8.17', // Specify the first Solidity version
            settings: {
                // Additional compiler settings for this version
                optimizer: {
                    enabled: true,
                    runs: 200
                },
                evmVersion: 'london' // EVM version (e.g., "byzantium", "constantinople", "petersburg", "istanbul", "berlin", "london")
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

## Example Usage

For a detailed example of integrating the VeChain SDK with Hardhat, visit our [apps/sdk-hardhat-integration directory](https://github.com/vechain/vechain-sdk-js/tree/main/apps/sdk-hardhat-integration). This repository contains a fully configured project demonstrating best practices and common use cases, serving as an excellent starting point for your VeChain development journey.

By leveraging this plugin, developers can harness the full potential of VeChainThor blockchain while benefiting from Hardhat's robust development environment. Happy coding!
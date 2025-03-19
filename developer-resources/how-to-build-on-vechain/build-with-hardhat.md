# Build with Hardhat

Hardhat is a development environment to compile, deploy, test, and debug your EVM-compatible applications. It helps developers manage and automate the recurring tasks inherent to the process of building smart contracts, as well as easily integrating with various plugins to extend its functionality. With Hardhat, you can write and run tests, script deployments, and interact with your contracts.

VeChain's SDK provides a plugin to instantly enable connectivity.

_The example project is relying on hardhat version 2.22.15 and the project initiated with `npx hardhat init`._

## Setup Hardhat

### Setup

To bootstrap a hardhat project:

```shell
npm install --save-dev hardhat
npx hardhat init
```

### Install Hardhat Plugin

To add VeChain support, install the hardhat plugin:

```bash
npm install --save-dev @vechain/sdk-hardhat-plugin
```

### Configure

Import or require the plugin in your `hardhat.config.ts` file:

```ts
import '@vechain/sdk-hardhat-plugin'
```

Add a network for TestNet or MainNet:

1. The Hardhat plugin requires `vechain` in the network's name.
2. Remote accounts are unsupported; therefore, provide account information.

Configure the solidity compile to `Paris` (or version that VeChain is compatible with)

A fully functional example configuration with:
- defined accounts to use
- fee delegation using vechain energy
- networks for mainnet, testnet, solo and hardhard

```ts
import { type HardhatUserConfig } from 'hardhat/config';
import '@nomicfoundation/hardhat-toolbox';
import '@vechain/sdk-hardhat-plugin';
import { HDKey } from '@vechain/sdk-core';
import { type HttpNetworkConfig } from 'hardhat/types';

// account to use
const accounts = ['0x2422eb37a0046d42e3c8d05c7d972de7fe1bb805e90b3a0dbc7d12b4d444c634']


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
				evmVersion: 'paris'
				}
			}
		]
	},
	networks: {

		/**
		* Example Mainnet configuration
		* No fee delegation
		*/
		vechain_mainnet: {
			// Mainnet
			url: 'https://mainnet.vechain.org',
			accounts,
			debug: false,
			gasPayer: undefined,
			gas: 'auto',
			gasPrice: 'auto',
			gasMultiplier: 1,
			timeout: 20000,
			httpHeaders: {}
		} satisfies HttpNetworkConfig,

		/**
		* Example Testnet configuration
		* With gasPayer url for fee delegation
		* Here a mnemonic is used to specify accounts
		*/
		vechain_testnet_gas_payer_url: {
			// Testnet
			url: 'https://testnet.vechain.org',
			accounts: {
				mnemonic:
					'vivid any call mammal mosquito budget midnight expose spirit approve reject system',
				path: HDKey.VET_DERIVATION_PATH,
				count: 3,
				initialIndex: 0,
				passphrase: 'vechainthor'
			},
			debug: true,
			gasPayer: {
				gasPayerServiceUrl:
					'https://sponsor-testnet.vechain.energy/by/269'
			},
			enableDelegation: true,
			gas: 'auto',
			gasPrice: 'auto',
			gasMultiplier: 1,
			timeout: 20000,
			httpHeaders: {}
		} satisfies HttpNetworkConfig,

		/**
		* Thor solo network configuration
		* Thor solo can be used for local deployment and testing
		*/
		vechain_solo: {
			// Thor solo network
			url: 'http://localhost:8669',
			accounts: [
			'7f9290cc44c5fd2b95fe21d6ad6fe5fa9c177e1cd6f3b4c96a97b13e09eaa158'
			],
			debug: false,
			enableDelegation: false,
			gasPayer: undefined,
			gas: 'auto',
			gasPrice: 'auto',
			gasMultiplier: 1,
			timeout: 20000,
			httpHeaders: {}
		} satisfies HttpNetworkConfig,

		/**
		* Default hardhat network configuration
		*/
		hardhat: {
			accounts: {
				mnemonic:
					'vivid any call mammal mosquito budget midnight expose spirit approve reject system',
				path: HDKey.VET_DERIVATION_PATH,
				count: 3,
				initialIndex: 0

			},
			debug: true,
			gasPayer: undefined,
			gas: 'auto',
			gasPrice: 'auto',
			gasMultiplier: 1,
			timeout: 20000,
			httpHeaders: {}

		}

	}

};

export default config;
```

## OpenZeppelin Contracts

Bootstrap your smart contract creation with [OpenZeppelin](https://www.openzeppelin.com/contracts) contracts. A compilation of widely used standards and patterns can significantly speed up the development process.

### Install

Install contract libraries and Hardhat helpers:

```shell
npm install --save @openzeppelin/contracts @openzeppelin/contracts-upgradeable @openzeppelin/hardhat-upgrades
```


### Create a ERC20 Token

Create `contracts/GLDToken.sol` and save this example:

```sol
// contracts/GLDToken.sol
// SPDX-License-Identifier: MIT
pragma solidity 0.8.20;


// Importing the ERC20 contract from OpenZeppelin
import "@openzeppelin/contracts/token/ERC20/ERC20.sol";

// Defining the GLDToken contract which inherits from ERC20
contract GLDToken is ERC20 {

	// Constructor to initialize the token with an initial supply
	// `initialSupply` is the amount of tokens that will be created at deployment

	constructor(uint256 initialSupply) ERC20("Gold", "GLD") {

		// Mint the initial supply of tokens and assign them to the contract deployer
		_mint(msg.sender, initialSupply);

	}
}
```

Run the following command to compile your contract:

```shell
npx hardhat compile
```

[https://wizard.openzeppelin.com](https://wizard.openzeppelin.com) provides an easy-to-use web interface for generating basic smart contracts.

## Deployment Contract

With [`hardhat-deploy`](https://github.com/wighawag/hardhat-deploy), deployments can be managed automatically without tracking the addresses of deployed contracts or manually upgrading contracts.

Create a deployment script in `deploy/MyToken.ts`:

```ts
import { ethers } from 'hardhat';

  
async function main(): Promise<void> {
	const erc20Contract = await ethers.deployContract('GLDToken', [100000]);
	await erc20Contract.waitForDeployment();
	const address = await erc20Contract.getAddress();
	console.log(`Gold contract deployed with address: ${address}`);
}

  
// We recommend this pattern to be able to use async/await everywhere
// and properly handle errors.
main().catch((error) => {
	console.error(error);
	process.exitCode = 1;
});
```

To execute the deploy script, specifying the network to deploy to:

```bash
npx hardhat deploy --network vechain_testnet_gas_payer_url
```

If a contract changes, deployment will automatically take place.

The status of deployments is stored in `deployments/<network name>`. Check out [`hardhat-deploy`](https://github.com/wighawag/hardhat-deploy) to learn more about its features and best practices.

### Example

The above steps are available in an example project with the SDK repository: [Example App](https://github.com/vechain/vechain-sdk-js/tree/main/apps/sdk-hardhat-integration)

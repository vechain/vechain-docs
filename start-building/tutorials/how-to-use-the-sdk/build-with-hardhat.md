# Build with Hardhat

Hardhat is a development environment to compile, deploy, test, and debug your EVM-compatible applications. It helps developers manage and automate the recurring tasks inherent to the process of building smart contracts, as well as easily integrating with various plugins to extend its functionality. With Hardhat, you can write and run tests, script deployments, and interact with your contracts.

Vechain's SDK provides a plugin to instantly enable connectivity.

_The example project is relying on hardhat version 2.22.5 and the project initiated with `npx hardhat init`._

## Setup Hardhat

### Install

To add Vechain support, install the plugin:

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

```ts
vechain_testnet: {
    url: "https://testnet.vechain.org",
    accounts,

    // optionally use fee delegation to let someone else pay the gas fees
    // visit vechain.energy for a public fee delegation service
    delegator: {
        delegatorUrl: "https://sponsor-testnet.vechain.energy/by/90"
    },
    enableDelegation: true,
},

vechain_mainnet: {
    url: "https://mainnet.vechain.org",
    accounts
},
```

### Example

A fully functional example configuration:

```ts
import "@nomicfoundation/hardhat-toolbox"
import "@vechain/sdk-hardhat-plugin"


const accounts = ['0x2422eb37a0046d42e3c8d05c7d972de7fe1bb805e90b3a0dbc7d12b4d444c634']

/** @type import('hardhat/config').HardhatUserConfig */
module.exports = {
  solidity: "0.8.24",
  networks: {
    vechain_testnet: {
      url: "https://testnet.vechain.org",
      accounts,

      // optionally use fee delegation to let someone else pay the gas fees
      // visit vechain.energy for a public fee delegation service
      delegator: {
        delegatorUrl: "https://sponsor-testnet.vechain.energy/by/90"
      },
      enableDelegation: true,
    },
    vechain_mainnet: {
      url: "https://mainnet.vechain.org",
      accounts
    },
  }
};
```

## OpenZeppelin Contracts

Bootstrap your smart contract creation with [OpenZeppelin](https://www.openzeppelin.com/contracts) contracts. A compilation of widely used standards and patterns can significantly speed up the development process.

### Install

Install contract libraries and Hardhat helpers:

```shell
npm install --save @openzeppelin/contracts @openzeppelin/contracts-upgradeable @openzeppelin/hardhat-upgrades
```

### Configure

Import or require the hardhat plugin in your `hardhat.config.ts` file:

```ts
import "@openzeppelin/hardhat-upgrades";
```

### Test

Create `contracts/MyToken.sol` and save this example:

```sol
// SPDX-License-Identifier: MIT
// Compatible with OpenZeppelin Contracts ^5.0.0
pragma solidity ^0.8.20;

import "@openzeppelin/contracts-upgradeable/token/ERC20/ERC20Upgradeable.sol";
import "@openzeppelin/contracts-upgradeable/access/AccessControlUpgradeable.sol";
import "@openzeppelin/contracts-upgradeable/proxy/utils/Initializable.sol";

contract MyToken is Initializable, ERC20Upgradeable, AccessControlUpgradeable {
    /// @custom:oz-upgrades-unsafe-allow constructor
    constructor() {
        _disableInitializers();
    }

    function initialize(address defaultAdmin) initializer public {
        __ERC20_init("MyToken", "MTK");
        __AccessControl_init();

        _grantRole(DEFAULT_ADMIN_ROLE, defaultAdmin);
    }
}
```

Run the following command to compile your contract:

```shell
npx hardhat compile
```

[https://wizard.openzeppelin.com](https://wizard.openzeppelin.com) provides an easy-to-use web interface for generating basic smart contracts.

## Deployment Manager

With [`hardhat-deploy`](https://github.com/wighawag/hardhat-deploy), deployments can be managed automatically without tracking the addresses of deployed contracts or manually upgrading contracts.

### Install

The installation requires installing the following packages:

```bash
npm install --save-dev @nomicfoundation/hardhat-ethers ethers hardhat-deploy hardhat-deploy-ethers
```

### Configure

Import or require the plugins in your `hardhat.config.ts` file:

```ts
import "hardhat-deploy";
import "hardhat-deploy-ethers";
```

### Deploy

Create a deployment script in `deploy/MyToken.ts`:

```ts
import { HardhatRuntimeEnvironment } from "hardhat/types";
import type { DeployFunction } from "hardhat-deploy/types";
import type { MyToken } from "../typechain-types";

const func: DeployFunction = async function (hre: HardhatRuntimeEnvironment) {
    const [deployer] = await hre.getUnnamedAccounts()
    await hre.deployments.deploy("MyToken", {
        contract: "MyToken",
        log: true,
        from: deployer,
        proxy: {
            proxyContract: "UUPS",
            execute: {
                init: {
                    methodName: "initialize",
                    args: [deployer],
                },
            },
        },
        libraries: {},
    });

    // read data from contract
    const contract = (await hre.ethers.getContract(
        "MyToken",
        deployer
    )) as MyToken;

    // get role identifier
    const ugpraderRole = await contract.DEFAULT_ADMIN_ROLE();

    // check role
    if (!(await contract.hasRole(ugpraderRole, deployer))) {
        console.log("Granting DEFAULT_ADMIN_ROLE");

        // execute a function of the deployed contract
        // .wait() waits for the receipts and throws if it reverts
        await (await contract.grantRole(ugpraderRole, deployer)).wait();
    } else {
        console.log("Already has DEFAULT_ADMIN_ROLE");
    }

    // access deployed address
    const MyToken = await hre.deployments.get("MyToken");
    console.log("MyToken is available at", MyToken.address);
};

func.id = "mytoken-upgradeable"; // name your deployment
func.tags = ["mytoken"]; // tag your deployment, to run certain tags only
func.dependencies = []; // build a dependency tree based on tags, to run deployments in a certain order

export default func;
```

All scripts in `deploy` will be run with:

```bash
npx hardhat deploy --network vechain_testnet
```

If a contract changes, deployment will automatically take place.

The status of deployments is stored in `deployments/<network name>`. Check out [`hardhat-deploy`](https://github.com/wighawag/hardhat-deploy) to learn more about its features and best practices.

### Example

The above steps are available in an example project on GitHub at [https://github.com/vechain-energy/example-hardhat-project](https://github.com/vechain-energy/example-hardhat-project).


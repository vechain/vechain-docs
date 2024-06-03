# Build with Hardhat

Hardhat is a development environment to compile, deploy, test, and debug your EVM-compatible applications. It helps developers manage and automate the recurring tasks inherent to the process of building smart contracts, as well as easily integrating with various plugins to extend its functionality. With Hardhat, you can write and run tests, script deployments, and interact with your contracts.

Vechain's SDK provides a plugin to instantly enable connectivity.

_The example project is relying on hardhat version 2.22.4 and the project initiated with `npx hardhat init`._

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
3. Set `requiredConfirmations` for ignition to 1 to workaround an RPC incompatibility

```typescript
  ignition: {
    requiredConfirmations: 1
  },
```

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
  ignition: {
    requiredConfirmations: 1
  },
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

# Run an Infinitism Bundler

## Clone the repo

```bash
git clone https://github.com/eth-infinitism/bundler.git
```

## Configuration

The following configuration changes then need to be made:

### Dependencies

Add vechain's Hardhat plugins in the Bundler's dependencies

```bash
cd packages/bundler && \
yarn add -D @vechain/hardhat-vechain @vechain/hardhat-ethers
```

### Hardhat Config

Modify `packages/bundler/hardhat.config.ts` to include:

```typescript
import { VECHAIN_URL_SOLO } from "@vechain/hardhat-vechain";
import "@vechain/hardhat-ethers";

module.exports = {
    ...
    defaultNetwork: "vechain"
    networks: {
        ...
        vechain: { url: VECHAIN_URL_SOLO }
    }
}
```

### Local Config

Modify `packages/bundler/localconfig/bundler.config.json`to include:

```json
{
  ...
  "network": "hardhat",
  "entryPoint": <Your EntryPoint Address>,
  ...
  "autoBundleMempoolSize": 1
}
```

* `"network": "hardhat"` directs the Bundler to use the Hardhat Provider
* `"entryPoint"`'s address is needed by the Bundler
* `"autoBundleMempoolSize": 1` Bundler processes every UserOp instead of polling them

## Run the bundler

```bash
cd ../../ # In the repository's root
```

```bash
yarn && yarn preprocess && yarn run bundler --unsafe
```

### Sample Output

```
command-line arguments:  {
  config: './localconfig/bundler.config.json',
  auto: false,
  unsafe: true
}
Merged configuration: {"port":"4337","entryPoint":"0xDbA21aab0Fa0A58895D19a9C13f9400D98D4f418","unsafe":true,"conditionalRpc":false,"gasFactor":"1","network":"hardhat","beneficiary":"0xd21934eD8eAf27a67f0A70042Af50A1D6d195E81","minBalance":"1","mnemonic":"./localconfig/mnemonic.txt","maxBundleGas":5000000,"minStake":"1","minUnstakeDelay":0,"autoBundleInterval":3,"autoBundleMempoolSize":1}
signer 0xf077b491b355E64048cE21E3A6Fc4751eEeA77fa balance 999999999.99999999999999
Bundle interval (seconds) 3
connected to network { name: 'unknown', chainId: 246 }
running on http://localhost:4337/rpc
```

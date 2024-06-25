# Remix

## RPC Proxy

The RPC Proxy is designed to bridge the gap between Thor's RESTful API and Ethereum's JSON-RPC, enabling seamless interaction with the VeChainThor blockchain through RPC calls. It is particularly useful for integrating with tools such as the Remix IDE, allowing developers to leverage familiar Ethereum development environments while working on VeChain projects.

## Installation

To install the RPC proxy, use the following command:

```bash
yarn add @vechain/sdk-rpc-proxy
```

## Configuration

Create a `config.json` with your desired settings. The configuration file includes the following fields:

- `url`: The URL of the VeChain Thor node.
- `port`: The port of the proxy server.
- `accounts`: The accounts that the proxy server will use to sign transactions (can be a mnemonic or an array of private keys).
- `verbose`: Wheter to enable verbose logging.
- `debug`: Whether to enable debug mode.
- `enableDelegation`: Whether to enable delegation.

### Example Configuration

``` json
{
    "url": "http://127.0.0.1:8669",
    "port": 8545,
    "accounts": {
        "mnemonic": "denial kitchen pet squirrel other broom bar gas better priority spoil cross",
        "count": 10
    },
    "verbose": true,
    "enableDelegation": false
}
```

If you are launching the RPC Proxy with the provided example configuration, make sure to have Thor running locally in solo mode. Find out more about Thors different options and how to build it [here](https://github.com/vechain/thor).

If you want to use VeChain `testnet` or `mainnet` use the following urls: `https://testnet.vechain.org/` or `https://mainnet.vechain.org/`. and remember also to change the `accounts` field by passing the correct account you want to use.

## Running the Proxy

After creating your configuration file, run the proxy using one of the following commands:

```bash
rpc-proxy -c <json config file>
```
Or:
``` bash
rpc-proxy --config <json config file>
```

## Connecting with Remix IDE

#### 1. Go to `DEPLOY & RUN TRANSACTIONS` section

<figure><img src="../../../.gitbook/assets/deploy_run_trxs (1).png" alt=""><figcaption></figcaption></figure>

#### 2. Choose Custom - External HTTP provider

<figure><img src="../../../.gitbook/assets/external_http_provider.png" alt=""><figcaption></figcaption></figure>

#### 3. Choose the URL to your proxy (default is http://127.0.0.1:8545) and click Ok

<figure><img src="../../../.gitbook/assets/set_proxy.png" alt=""><figcaption></figcaption></figure>

#### 4. Compile and deploy contracts

<figure><img src="../../../.gitbook/assets/compile_deploy.png" alt=""><figcaption></figcaption></figure>

#### 5. Interact with contracts via provided interface

<figure><img src="../../../.gitbook/assets/interact.png" alt=""><figcaption></figcaption></figure>

## Known Issues and Workaround

Currently there are some limitations when using this proxy. One of them is the fact that when deploying contracts you could get an error of the following type `creation of ContractName errored: [TIMEOUT] Timeout for call deployMetadataOf from udapp`. This usually happens after 3 or more deployments one after another.

Fortunately there is a workaround for this, if all contracts are required in the same workspace. When deploying contracts note their address as well as the contract name. When you get the aforementioned error refresh Remix and recompile the contracts. When navigating to the `DEPLOY & RUN TRANSACTIONS` section instead of re-deploying the contract paste the address in the `AtAddress` section and it will load from your previous deployment. You can now succesfully interact with a previously deployed contract.

<figure><img src="../../../.gitbook/assets/workaround.png" alt=""><figcaption></figcaption></figure>

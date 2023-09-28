# Custom Network

To start your own custom network, you need to manually configure the genesis file. Once you finished the setup, it allows you to connect to your own network rather than connect to official network (mainnet / testnet)

## Prerequisites <a href="#requirement" id="requirement"></a>

1. Make sure the network has at least **two** nodes running as a authority master node
2. Thor version ≥ [v1.0.7](https://github.com/vechain/thor/releases/tag/v1.0.7)

{% hint style="info" %}
Running a custom network requires prior knowledge of the [built-in-contracts.md](../../../developer-resources/built-in-contracts.md "mention")and [#proof-of-authorithy-poa](../../../introduction-to-vechain/about-the-vechain-blockchain/consensus-deep-dive.md#proof-of-authorithy-poa "mention")
{% endhint %}

## Configure Your Genesis File <a href="#configure-your-genesis-file" id="configure-your-genesis-file"></a>

You can find an example genesis file [here](https://github.com/vechain/thor/blob/master/genesis/example.json)

### Genesis Description Object <a href="#genesis-description-object" id="genesis-description-object"></a>

* `launchTime`: Launch time (unix timestamp) of your network (i.e. the time of genesis block). If you set the time in the future, master node would not propose block before that.
* `gasLimit`: Initial block gas limit.
* `extraData`: Additional data set to genesis block, limited to 28 characters.
* `accounts`: Preallocated accounts in genesis block, including `balance`, `energy`, `storage` and `code`.
* `authority`: Authority master nodes.
* `params`: Governance parameters.
* `executor`: Executor params for on-chain governance, setting approvers means using VeChain builtin executor, omit means an external address.

### Authority <a href="#authority" id="authority"></a>

For setting the authority node, you need to get your authority node's master address first, simply running the following command

```
thor master-key
```

The master address will be shown. `Endorsor Address` is the endorser's address for authority node, you need to ensure the `Endorsor Address` reach the minimum amount of `proposerEndorsement`. You can adjust the minimum endorsement amount of VET by changing `proposerEndorsement`. `Identity` is an identifier of the authority node.

### Params <a href="#params" id="params"></a>

* `rewardRatio`: Reward ratio for block proposer.
* `baseGasPrice`: Base gas price in `wei`.
* `proposerEndorsement`: Authority node endorsement in `wei`.
* `executorAddress`: Executor address, if there is approver in `executor`, the address will be set code of `Builtin Executor Contract` and set up the approves, otherwise the executor will be an external address.

## Launch Custom Network <a href="#launch-custom-network" id="launch-custom-network"></a>

Start all your nodes by running `thor --network genesis.json` and wait for the nodes to connect to each other and then the master nodes will start packing the blocks.

### Custom Bootnode <a href="#custom-bootnode" id="custom-bootnode"></a>

Starting a custom network will use the foundation's bootnode to discover nodes by default. This means you need at least 1 node with public IP attached. Thor provides the ability to specify bootnode.

1. Start thor by `thor --network genesis.json` then get `Node ID` in the startup info, it looks like `enode://0b9f...6932@[extip]:11235`.
2. Replace `[extip]` with the real ip address of your machine.
3. Launch nodes by running `thor --network genesis.json --bootnode "NodeID-1,NodeID-2..."`.

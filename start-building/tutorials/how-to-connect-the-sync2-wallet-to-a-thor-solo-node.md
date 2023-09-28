# How to connect the Sync2 wallet to a Thor Solo Node

This tutorial will provide a step by step guide for running a Thor solo node and connecting it to the Sync2 wallet. The Thor solo node is a sandbox development mode for the VechainThor blockchain, that can be started (and is only available) on a single server. It is not publicly accessible and the generated blocks will be lost if the solo node is stopped.

## Step 1 : Launch the solo node <a href="#step-1-launch-the-solo-node" id="step-1-launch-the-solo-node"></a>

Run Thor solo with the following docker command or follow the [how-to-run-a-thor-solo-node](how-to-run-a-thor-solo-node/ "mention") tutorial.

```bash
docker run -p 127.0.0.1:8669:8669 vechain/thor:latest solo --api-cors '*' --api-addr 0.0.0.0:8669
```

This will launch a solo node with the following configuration:

* On a localhost using port 8669
* Using the latest release of thor solo
* Accepting all cross origin requests
* Allowing all remote connections

## Step 2 : Connect Sync2 node to solo node <a href="#step-2-connect-sync2-node-to-solo-node" id="step-2-connect-sync2-node-to-solo-node"></a>

Sync2 is designed to work with all mainstream web browsers (e.g., Chrome, Safari, MS Edge, Firefox, etc), desktop, and mobile devices.

The main advantage and purpose of Sync2 is the massive simplification of dApps and dApp usage. All editions of Sync2, no matter whether the native app is built for desktop or mobile or the automatically invoked SPA version, are designed to appear and function pretty much in the same way, therefore providing a consistent and comfortable user experience for users across different OS and devices.

### Get Sync2 <a href="#get-sync2" id="get-sync2"></a>

Follow the instructions here [sync2](../../core-concepts/wallets/sync2/ "mention") to download and install the Sync2 wallet.

### Connect Sync2 to solo node <a href="#connect-sync2-to-solo-node" id="connect-sync2-to-solo-node"></a>

#### **Step1: Add node**

1. Click the ![](../../.gitbook/assets/menu.svg)icon, in the top left hand corner.
2. Click **Settings**.
3. Click **Nodes**.
4. Click the ![](../../.gitbook/assets/add\_circle\_outline.svg) icon, in the upper right hand corner.
5. Enter the node's url `http:localhost:8669.`
6. Click **Add** to add node.

#### **Step2: Import the solo built-in wallet**

1. Click upper left ![](../../.gitbook/assets/menu.svg) icon, in the top left hand corner, to open the wallet list.
2. Click the ![](../../.gitbook/assets/add\_circle\_outline.svg)icon to create a new wallet.
3. Click upper right ![](../../.gitbook/assets/more\_horiz.svg) icon.
4. Select **Private.**
5. Click **Import.**
6. Enter the mnemonic words for the Thor solo node built-in wallet.

{% hint style="info" %}
Mnemonic phrase of the Thor solo node built-in wallet:

denial kitchen pet squirrel other broom bar gas better priority spoil cross
{% endhint %}

{% hint style="danger" %}
Do not use the above mnemonic phrase to secure mainnet assets. The funds will not be secure as the mnemonic is exposed.
{% endhint %}

7. Enter your password to authorize the import

Congrats! You have successfully connected to a Thor solo node with the Sync2 wallet, and you can now deploy/integrate by using [inspector ](https://inspector.vecha.in/)or you can check out the [useful-tips-for-building-a-dapp-by-using-connex.md](useful-tips-for-building-a-dapp-by-using-connex.md "mention").

### Step 3: Launch Devpal <a href="#step-3-launch-devpal" id="step-3-launch-devpal"></a>

Devpal is a set of tools to help your develop and test on a Thor solo mode and start your blockchain journey smoothly. Devpal contains two tools:

* **Insight**: a serverless VeChain explorer. It allows you to explore and search for blocks, transactions, and accounts. [Mainnet](https://insight.vecha.in/#/main/) and [Testnet](https://insight.vecha.in/#/test/) links.
* **Inspector**: a tool that allows you to deploy and interact with the contract. Available [here](https://inspector.vecha.in/).

You can simply run devpal by running the following command:

```bash
npx @vechain/devpal
```

{% hint style="info" %}
_**http://locahost:8669**_ is set as the default node url.

If you want to change it, please use `npx @vechain/devpal [Thor REST URL]`
{% endhint %}

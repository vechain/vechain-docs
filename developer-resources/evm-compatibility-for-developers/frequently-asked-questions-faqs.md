# Frequently Asked Questions (FAQs)

**Q: Does VeChain have RPC URLs?**

VeChain has a list of public nodes that can found [here](https://docs.vechain.org/how-to-run-a-node/nodes#mainnet-nodes), but they all expose RESTful API endpoints instead of RPC. This interface should be preferred. &#x20;

For faster integration and migration from Ethereum, you can run a [docker](https://hub.docker.com/r/vechain/sdk-rpc-proxy) or the command\
&#x20;_`npx @vechain/sdk-rpc-proxy`_

A local [JSON-RPC proxy](https://www.npmjs.com/package/@vechain/sdk-rpc-proxy?activeTab=readme) of a Testnet node will be available at `http://127.0.0.1:8545`.

The service is also hosted by a third-party here: [https://rpc-mainnet.vechain.energy](https://rpc-mainnet.vechain.energy).

**Q: Is authentication required to access the node?**

* No authentication is required for public node access.

**Q: Is HTTPS supported?**

* Yes, HTTPS is Supported and recommended.

**Q: What is the request rate limit?**

* Up to 1000 requests per minute (RPM) is supported. IP whitelisting may be required to prevent rate limiting when accessing public nodes.

#### Q: What is VeChain's consensus mechanism?

* Proof of Authority (PoA) 2.0.

**Q: How are transaction fees handled?**

* VTHO is used for gas fees. 30% of transaction fees are burned.

**Q: What is VeChain Network and Chain ID of the RPC proxy?**

* Network ID:
  * Mainnet: 100009
  * Testnet: 100010
* Chain ID:
  * Mainnet: 100009
  * Testnet: 100010

Note that VeChainThor considers the id of the _genesis block_ (block number 0) as chainId.

**Q: What is the time to finality?**

* Typically 30-60 minutes, with deterministic finality requiring two BFT rounds every 30 minutes. Blocks and transactions are justified after the first round.

**Q: What is the native token?**

* Name: VeChain Token (VET) Symbol: VET Decimals: 18

**Q: Does it uses the same address format than Ethereum?**

* Yes, VeChain uses the 0x address format.

**Q: If I import my Ethereum mnemonic into VeWorld, will I get the same address?**

* Yes, but you have to select the Ethereum derivation path.&#x20;

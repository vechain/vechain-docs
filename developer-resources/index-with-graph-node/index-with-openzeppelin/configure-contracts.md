# Configure Contracts

The VeBetterDAO contract addresses are available on [docs.vebetterdao.org/smart-contracts](https://docs.vebetterdao.org/smart-contracts):

* B3TR: `0x5ef79995FE8a89e0812330E4378eB2660ceDe699`
* VOT3: `0x76Ca782B59C74d088C7D2Cce2f211BC00836c602`

To prevent the indexer from scanning every block before the deployment, VeChainStats can be used to determine the contract creation, which will speed up indexing significantly:

* [B3TR on VeChainStats](https://vechainstats.com/account/0x5ef79995fe8a89e0812330e4378eb2660cede699/) was deployed in Block #18,868,849
* [VOT3 on VeChainStats](https://vechainstats.com/account/0x76Ca782B59C74d088C7D2Cce2f211BC00836c602/) was deployed in Block #18,868,851

Create a configuration file `vbd-tokens.json` with this information:

```json
{
  "output": "vebetterdao/tokens.",
  "chain": "mainnet",
  "datasources": [
    {
      "address": "0x5ef79995FE8a89e0812330E4378eB2660ceDe699",
      "startBlock": 18868849,
      "module": ["erc20"]
    },
    {
      "address": "0x76Ca782B59C74d088C7D2Cce2f211BC00836c602",
      "startBlock": 18868851,
      "module": ["erc20"]
    }
  ]
}
```

```shell
npx graph-compiler \
  --config vbd-tokens.json \
  --include node_modules/@openzeppelin/subgraphs/src/datasources \
  --export-schema \
  --export-subgraph
```

The subgraph schema and configuration will be generated in the `vebetterdao/` directory.

* `vebetterdao/tokens.subgraph.yaml` contains the subgraph instructions on what and how to index data.
* `vebetterdao/tokens.schema.graphql` contains the database schema on how to store and connect the data.

Inspect both files to learn more about the basics of writing your own subgraphs.

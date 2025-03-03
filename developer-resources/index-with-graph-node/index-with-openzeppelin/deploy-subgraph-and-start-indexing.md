# Deploy Subgraph and start Indexing

The [@graphprotocol/graph-cli](https://www.npmjs.com/package/@graphprotocol/graph-cli) are required to prepare subgraphs and interact with the graph node.

Install them with npm:

```shell
npm install --save @graphprotocol/graph-cli
```

Deploying the subgraph is a multi-step process:

1. `codegen` generates AssemblyScript types from the subgraph's GraphQL schema and the contract ABIs included in the data sources. It must be run when either the schema or ABIs change.
2. `build` generates the AssemblyScript from the subgraph's indexing scripts.
3. `graph create` generates the namespace on the node where all the subgraph data will be stored. It must only be run once.
4. `graph deploy` uploads the subgraph package to IPFS and instructs the graph node to use it.

## _**`codegen`****\*\*\*\* \*\*\*\*with example output**_

```shell
npx graph codegen vebetterdao/tokens.subgraph.yaml
```

```shell
  Skip migration: Bump mapping apiVersion from 0.0.1 to 0.0.2
  Skip migration: Bump mapping apiVersion from 0.0.2 to 0.0.3
  Skip migration: Bump mapping apiVersion from 0.0.3 to 0.0.4
  Skip migration: Bump mapping apiVersion from 0.0.4 to 0.0.5
  Apply migration: Bump mapping apiVersion from 0.0.5 to 0.0.6
  Skip migration: Bump manifest specVersion from 0.0.1 to 0.0.2
  Apply migration: Bump manifest specVersion from 0.0.2 to 0.0.4
✔ Apply migrations
✔ Load subgraph from vebetterdao/tokens.subgraph.yaml
  Load contract ABI from node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
  Load contract ABI from node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
✔ Load contract ABIs
  Generate types for contract ABI: IERC20 (node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json)
  Generate types for contract ABI: IERC20 (node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json)
  Write types to generated/erc20/IERC20.ts
  Write types to generated/erc20-1/IERC20.ts
✔ Generate types for contract ABIs
✔ Generate types for data source templates
✔ Load data source template ABIs
✔ Generate types for data source template ABIs
✔ Load GraphQL schema from vebetterdao/tokens.schema.graphql
  Write types to generated/schema.ts
✔ Generate types for GraphQL schema

Types generated successfully
```

## **`build` with example output**

```shell
npx graph build vebetterdao/tokens.subgraph.yaml
```

```shell
  Skip migration: Bump mapping apiVersion from 0.0.1 to 0.0.2
  Skip migration: Bump mapping apiVersion from 0.0.2 to 0.0.3
  Skip migration: Bump mapping apiVersion from 0.0.3 to 0.0.4
  Skip migration: Bump mapping apiVersion from 0.0.4 to 0.0.5
  Skip migration: Bump mapping apiVersion from 0.0.5 to 0.0.6
  Skip migration: Bump manifest specVersion from 0.0.1 to 0.0.2
  Skip migration: Bump manifest specVersion from 0.0.2 to 0.0.4
✔ Apply migrations
✔ Load subgraph from vebetterdao/tokens.subgraph.yaml
  Compile data source: erc20 => build/erc20/erc20.wasm
  Compile data source: erc20-1 => build/erc20/erc20.wasm (already compiled)
✔ Compile subgraph
  Copy schema file build/tokens.schema.graphql
  Write subgraph file build/node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
  Write subgraph file build/node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
  Write subgraph manifest build/subgraph.yaml
✔ Write compiled subgraph to build/

Build completed: build/subgraph.yaml
```

## **`graph create` with example output**

The create command needs to know the service URL of your Graph Node, which is `http://127.0.0.1:8020` in the default setup:

```shell
npx graph create vebetterdao/tokens --node http://127.0.0.1:8020
```

```shell
 ›   Warning: In next major version, this command will be merged as a subcommand for `graph local`.
Created subgraph: vebetterdao/tokens
```

## **`graph deploy` with example output**

The deploy command needs to know the service URL, the IPFS node to upload the subgraph package and the subgraph definition to upload. In the default setup, the service URL is `http://127.0.0.1:8020` and the IPFS node is available on `http://127.0.0.1:5001`.

The previously generated `vebetterdao/tokens.subgraph.yaml` is the subgraph definition to upload. A version is required and is used to identify different deployments. In the local environment, versions can be ignored and re-used.

```shell
npx graph deploy vebetterdao/tokens --node http://127.0.0.1:8020 --ipfs http://127.0.0.1:5001 --version-label 1 vebetterdao/tokens.subgraph.yaml 
```

```shell
  Skip migration: Bump mapping apiVersion from 0.0.1 to 0.0.2
  Skip migration: Bump mapping apiVersion from 0.0.2 to 0.0.3
  Skip migration: Bump mapping apiVersion from 0.0.3 to 0.0.4
  Skip migration: Bump mapping apiVersion from 0.0.4 to 0.0.5
  Skip migration: Bump mapping apiVersion from 0.0.5 to 0.0.6
  Skip migration: Bump manifest specVersion from 0.0.1 to 0.0.2
  Skip migration: Bump manifest specVersion from 0.0.2 to 0.0.4
✔ Apply migrations
✔ Load subgraph from vebetterdao/tokens.subgraph.yaml
  Compile data source: erc20 => build/erc20/erc20.wasm
  Compile data source: erc20-1 => build/erc20/erc20.wasm (already compiled)
✔ Compile subgraph
  Copy schema file build/tokens.schema.graphql
  Write subgraph file build/node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
  Write subgraph file build/node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
  Write subgraph manifest build/subgraph.yaml
✔ Write compiled subgraph to build/
  Add file to IPFS build/tokens.schema.graphql
                .. QmTJC228tSzgV6ano5uSgVkk4yq3tdpUAZ11xBBnqtKbmm
  Add file to IPFS build/node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
                .. QmVkgbSMT9SrNoFcfxSdSmhghS2zz7Y6g3QxQ1xZ8HccrB
  Add file to IPFS build/node_modules/@openzeppelin/contracts/build/contracts/IERC20Metadata.json
                .. QmVkgbSMT9SrNoFcfxSdSmhghS2zz7Y6g3QxQ1xZ8HccrB (already uploaded)
  Add file to IPFS build/erc20/erc20.wasm
                .. QmWbi5wkYU15ksR7H4iMkQ7yZYXihPwb8qYfun7Ne1xcLn
  Add file to IPFS build/erc20/erc20.wasm
                .. QmWbi5wkYU15ksR7H4iMkQ7yZYXihPwb8qYfun7Ne1xcLn (already uploaded)
✔ Upload subgraph to IPFS

Build completed: QmezwJ1bGUGAUXehjg1qsTrycRVxsw29vFqVuN5fdzsE98

Deployed to http://127.0.0.1:8000/subgraphs/name/vebetterdao/tokens/graphql

Subgraph endpoints:
Queries (HTTP):     http://127.0.0.1:8000/subgraphs/name/vebetterdao/tokens
```

##

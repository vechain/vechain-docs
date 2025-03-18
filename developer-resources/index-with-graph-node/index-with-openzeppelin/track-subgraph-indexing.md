# Track Subgraph Indexing

The subgraph starts indexing immediately. You can track its indexing status in the service logs using `docker compose logs -n 10 -f`.

Open the Admin GraphQL Playground to track details about the subgraph at [http://localhost:8030/graphql](http://localhost:8030/graphql).

Use the auto-completion in the UI to learn more about the query possibilities. The following query provides you with status information for the deployed `vebetterdao/tokens` subgraph:

```graphql
{
  indexingStatusForCurrentVersion(subgraphName: "vebetterdao/tokens") {
    synced
    health
    entityCount
    subgraph
    chains {
      chainHeadBlock {
        number
      }
      latestBlock {
        number
      }
    }
    fatalError {
      message
      block {
        number
      }
    }
  }
}
```

The output will be similar to this

```json
{
  "data": {
    "indexingStatusForCurrentVersion": {
      "synced": false,
      "health": "healthy",
      "entityCount": "914",
      "subgraph": "QmezwJ1bGUGAUXehjg1qsTrycRVxsw29vFqVuN5fdzsE98",
      "chains": [
        {
          "chainHeadBlock": {
            "number": "19076170"
          },
          "latestBlock": {
            "number": "18869150"
          }
        }
      ],
      "fatalError": null
    }
  }
}
```

The status shows if the subgraph is fully synchronized with all blockchain data, if it's healthy, and any possible errors. During indexing, it's interesting to learn how many entities have been created (transfer events, balances, etc.), and to track the status, the latest block provides an indication of how far the indexing has progressed.

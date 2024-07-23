# Access Subgraph

During deployment, the subgraph URL has been shown. It is the subgraph's name attached to the service URL: [http://127.0.0.1:8000/subgraphs/name/vebetterdao/tokens/graphql](http://127.0.0.1:8000/subgraphs/name/vebetterdao/tokens/graphql)

When opened in the browser, it will display a GraphiQL interface that allows you to build queries by clicking and entering the data. Use it to explore possibilities and test queries.

An example query to test the subgraph is:

```graphql
{
  erc20Contracts {
    name
    symbol
    totalSupply {
      value
    }
    balances(
      orderBy: valueExact
      orderDirection: desc
      where: {account_not: null}
      first: 1
    ) {
      account {
        id
      }
      value
    }
  }
}
```

This query will retrieve all indexed contracts (B3TR + VOT3) and list some details about them, including the largest account holder for each.

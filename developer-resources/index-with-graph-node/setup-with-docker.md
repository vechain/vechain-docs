# Setup with Docker

The most straightforward process of setting up all required elements is using [docker compose](https://docs.docker.com/compose/).

The required services are:

1. A Graph-Node that orchestrates all other services to achieve indexing and data retrieval
2. An IPFS node to store uploaded subgraphs and provide files, if necessary
3. Postgres DB to store the indexed data
4. VeChainThorNode to provide access to Blockchain data
5. RPC-Proxy that adds RPC compatibility on top of the VeChainThorNode

The `docker-compose.yml` combining all services is:

```yaml
services:
  rpc-proxy:
    image: ifavo/vet-rpc:latest
    platform: linux/amd64
    container_name: rpc-proxy
    ports:
      - "8545:8545"
    environment:
      - NODE_URL=https://mainnet.vechain.org
  graph-node:
    platform: linux/amd64
    image: graphprotocol/graph-node:v0.35.1
    ports:
      - '8000:8000'
      - '8001:8001'
      - '8020:8020'
      - '8030:8030'
      - '8040:8040'
    depends_on:
      - ipfs
      - postgres
      - rpc-proxy
    environment:
      postgres_host: postgres
      postgres_user: graph-node
      postgres_pass: let-me-in
      postgres_db: graph-node
      ipfs: 'ipfs:5001'
      ethereum: 'mainnet:http://rpc-proxy:8545'
      GRAPH_LOG: info
      ETHEREUM_POLLING_INTERVAL: 1000
      GRAPH_ETHEREUM_MAX_BLOCK_RANGE_SIZE: 100
  ipfs:
    platform: linux/amd64
    image: ipfs/kubo:v0.29.0
    ports:
      - '5001:5001'
    volumes:
      - ./data/ipfs:/data/ipfs
  postgres:
    image: postgres:14
    ports:
      - '5432:5432'
    command:
      [
        "postgres",
        "-cshared_preload_libraries=pg_stat_statements",
        "-cmax_connections=200"
      ]
    environment:
      POSTGRES_USER: graph-node
      POSTGRES_PASSWORD: let-me-in
      POSTGRES_DB: graph-node
      PGDATA: "/var/lib/postgresql/data"
      POSTGRES_INITDB_ARGS: "-E UTF8 --locale=C"
    volumes:
      - ./data/postgres:/var/lib/postgresql/data
```

If save and run it, you will instantly start indexing VeChain and track its latest status:

```bash
$ docker compose up -d
[+] Running 5/5
 ✔ Network example_default         Created                                                                                                                                                                                                                                                                                                                                0.0s
 ✔ Container example-postgres-1    Started                                                                                                                                                                                                                                                                                                                                3.8s
 ✔ Container example-ipfs-1        Started                                                                                                                                                                                                                                                                                                                                3.8s
 ✔ Container rpc-proxy          Started                                                                                                                                                                                                                                                                                                                                3.8s
 ✔ Container example-graph-node-1  Started

```

The following services will be available:

<table><thead><tr><th width="271">URL</th><th>Service</th><th>Description</th></tr></thead><tbody><tr><td>http://localhost:8000</td><td>GraphQL Service</td><td>Web application to build queries with an interface</td></tr><tr><td>http://localhost:8001</td><td>GraphQL WebSocket Service</td><td>WebSocket connectivity</td></tr><tr><td>http://localhost:8020</td><td>Admin API</td><td>Provides access to manage Subgraphs, should never be made public</td></tr><tr><td>http://localhost:8030/graphql</td><td>Admin GraphQL Service</td><td>Web application to query subgraph details</td></tr><tr><td>http://localhost:5001</td><td>IPFS</td><td>Access to the IPFS Node</td></tr><tr><td><code>postgresql://graph-node:let-me-in@localhost:5432/graph-node</code></td><td>Postgres</td><td>Database access</td></tr><tr><td>http://localhost:8545</td><td>RPC</td><td>RPC Interface to VeChain</td></tr></tbody></table>

Data is stored in `data/` directory and persists between restarts.

---
description: >-
  A thor solo node is a VechainThor blockchain node running in a sandbox
  development mode.
---

# How to run a Thor Solo Node

The official Thor repo is available [here](https://github.com/vechain/thor) and provides more detail and information than this tutorial provides.

Thor Solo always spins up the same ten accounts. Both VET and VTHO are generated on these addresses in the genesis block. A list of all ten accounts is shown when Thor Solo is started.

## Prerequisites

Thor requires `Go` 1.17+ and `C` compiler to build. To install `Go`, follow this [link](https://golang.org/doc/install).

## Installation

The first step is to clone the repository

```bash
git clone https://github.com/vechain/thor
```

Assuming you have Golang and a C compiler installed navigate to the directory and build Thor:

```bash
cd thor
make
```

Assuming there were no errors, a `thor` binary will appear under the `bin` directory.

## Command-line options

Thor supports multiple command-line options which you can see by running:

```bash
./bin/thor -h
```

The most important ones for us are the following:

* `--api-cors '*'`  comma separated list of domains to accept cross origin requests to API
* `--api-addr value` API service listening address (default: "localhost:8669")
* `--api-call-gas-limit value` limit contract call gas (default: 50000000)
* `--api-backtrace-limit value` limit the distance between 'position' and best block for subscriptions APIs (default: 1000)
* `--verbosity value` log verbosity (0-9) (default: 3)

### Sub-Commands

Thor offers several sub-commands to manage the way that the node operates and stores the blockchain data.

```bash
./bin/thor solo --on-demand            # create new block when there is pending transaction
./bin/thor solo --persist              # save blockchain data to disk (default to memory)
./bin/thor solo --persist --on-demand  # two options can work together
```

### Enable Remote Connections

If you are not running Thor on the same host as the development environment then you need to provide an API listening address using the `--api-addr` command-line option. For example to make Thor accept any remote connection:

```bash
./bin/thor solo --on-demand --api-addr 0.0.0.0:8669
```

### Higher Verbosity

The default verbosity option in Thor (3) might not be providing enough information for debugging. Using the `--verbosity` command-line option, we can increase the amount of information Thor prints in stdout. For example:

<pre class="language-bash"><code class="lang-bash"><strong>./bin/thor solo --on-demand --verbosity 4
</strong></code></pre>

### Master Key Management

Thor offers several sub-commands to manage the master key of the node. Using the `master-key` command-line option, allows the user to interact with the master key on the node.

```bash
# print the master address
./bin/thor master-key

# export master key to keystore
./bin/thor master-key --export > keystore.json

# import master key from keystore
cat keystore.json | ./bin/thor master-key --import
```

## Restful API

One notable feature of Thor is that it provides a RESTful API as well as the typical RPC interface. The API can be accessed via the browser using:

```bash
http://127.0.0.1:8669/doc/swagger-ui/
```

If Thor is running on a different host, make sure you use the IP of said host as well as the `--api-addr` command-line option when running Thor.

## Running

To run the node in solo mode which is what we need for development purposes use the following:

```bash
./bin/thor solo --on-demand
```

{% hint style="info" %}
Thor can also be run with a test or main network by passing the command

`--network test | main`&#x20;



A custom network can also be created by passing the command

`--network <custom-net-genesis.json>`



An example genesis config file can be found at [genesis/example.json](https://raw.githubusercontent.com/vechain/thor/master/genesis/example.json).
{% endhint %}

For development purposes the following flags are recommended

{% hint style="warning" %}
The below command runs thor solo allowing all remote connections. Remove the argument `--api-addr 0.0.0.0:8669` to prevent all remote connections.
{% endhint %}

<pre class="language-bash"><code class="lang-bash"><strong>./bin/thor solo --on-demand --api-addr 0.0.0.0:8669 --gas-limit 10000000000000 --api-call-gas-li
</strong></code></pre>

## Docker

You can also run a solo node as a docker container with the following command.

```bash
docker run -p 127.0.0.1:8669:8669 vechain/thor:latest solo --api-cors '*' --api-addr 0.0.0.0:8669
```

This will launch a solo node with the following configuration:

* On a localhost using port 8669
* Using the latest release of thor solo
* Accepting all cross origin requests
* Allowing all remote connections

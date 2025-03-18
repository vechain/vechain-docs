---
description: >-
  A thor solo node is a VeChainThor blockchain node running in a sandbox,
  particularly useful for developers who might need to wait for a specific
  condition to be met, that in a living environment would
---

# How to run a Thor Solo Node

A \[Thor] (https://github.com/vechain/thor) Solo Node is a powerful tool for developers, offering a sandbox environment to interact with the VeChainThor blockchain. This guide will walk you through the setup and operation of your own Thor Solo Node, enabling you to test and develop applications in a controlled setting.

## Prerequisites

Before we begin, ensure you have:

* `Go` 1.17+ installed
* A `C` compiler
* Git

## Installation Process

Clone the Thor repository:

```bash
git clone https://github.com/vechain/thor
```

Navigate to the Thor directory and build:

```bash
cd thor
make
```

Upon successful compilation, you'll find the `thor` binary in the `bin` directory.

## Key Command-line Options

Explore Thor's capabilities with `./bin/thor -h`. Essential options include:

* `--api-cors '*'`: Accept cross-origin requests from any domain.
* `--api-addr value`: Set API service listening address (default: "localhost:8669").
* `--api-call-gas-limit value`: Limit contract call gas (default: 50000000).
* `--verbosity value` log verbosity (0-9) (default: 3).

## Advanced Configuration

### Sub-Commands for Enhanced Control

Thor offers versatile sub-commands:

```bash
./bin/thor solo --on-demand            # Create new blocks for pending transactions
./bin/thor solo --persist              # Save blockchain data to disk
./bin/thor solo --persist --on-demand  # The two options can work together
```

### Enabling Remote Access

If Thor node is not running on the same machine of the development environment, then you need to provide an API listening address using the `--api-addr` command-line option. For example, to make Thor accept any remote connection:

```bash
./bin/thor solo --on-demand --api-addr 0.0.0.0:8669
```

### Debugging with Increased Verbosity

The default verbosity option in Thor (3) might not be providing enough debug information. Using the `--verbosity` command-line option, you can increase the amount of information Thor prints out in stdout. For example:

<pre class="language-bash"><code class="lang-bash"><strong>./bin/thor solo --on-demand --verbosity 4
</strong></code></pre>

### Master Key Management

Secure your node with master key commands:

```bash
# View master address
./bin/thor master-key

# Export master key to keystore
./bin/thor master-key --export > keystore.json

# Import master key from keystore
cat keystore.json | ./bin/thor master-key --import
```

## RESTful API: A Developer's Playground

Thor's RESTful API offers a user-friendly interface for blockchain interaction. Access the Stoplight UI at:

```bash
http://127.0.0.1:8669/doc/stoplight-ui/
```

Or the Swagger UI at:

```bash
http://127.0.0.1:8669/doc/swagger-ui/
```

If Thor is running on a different host, make sure to run it using the IP of said host instead of the localhost, as well as the `--api-addr` command-line option.

## Launching Your Solo Node

To run the node in solo mode which is what we need for development purposes use the following:

```bash
./bin/thor solo --on-demand
```

{% hint style="info" %}
Thor can also be run with a test or main network by passing the command

`--network test | main`

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

## Docker: Containerized Convenience

The most convenient way can be to use a Docker container. You can run your solo node as follows:

```bash
docker run -p 127.0.0.1:8669:8669 vechain/thor:latest solo --api-cors '*' --api-addr 0.0.0.0:8669
```

This sets up a containerized node with:

* Localhost access on port 8669
* Latest Thor Solo release
* Unrestricted cross-origin requests
* Remote connection capability

## Conclusion

With your Thor Solo Node up and running, you're ready to dive into VeChainThor development. This powerful tool provides a flexible, controlled environment for building and testing blockchain applications. Happy coding!

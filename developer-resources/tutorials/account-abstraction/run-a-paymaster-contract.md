# Run a Paymaster Contract

The following instructions demonstrate how to use a Proof of Concept Paymaster that accepts to sponsor any `userOperation`. This is for development purposes only and shall not be deployed in any main-net.

## Prerequisites:

In order to use the paymaster that we will deploy you will need some prerequisites.&#x20;

1. A locally running Thor solo node
2. EntryPoint contract deployed on Thor solo node
3. A bundler with a adequately funded EOA
4. A 4337 client that supports paymasters (e.g. stackup client)

## Instructions:

1. Clone the example repo

```bash
git clone https://github.com/vechainfoundation/dummyPaymaster
```

2. Install dependencies

```bash
npm i --force
```

3. Add the EntryPoint address to `MyPaymasterDeploy.test.ts` script
4. Deploy Paymaster

```bash
 npx hardhat test test/MyPaymasterDeploy.test.ts --network vechain
```

5\. Add the paymaster address to your `config.json` file

6\. Start the paymaster service (by default port 8546)

```bash
npx hardhat run scripts/startPaymaster.ts
```

Now we have:

* A deployed paymaster contract on a Thor solo node
* A Paymaster service running on port 8546

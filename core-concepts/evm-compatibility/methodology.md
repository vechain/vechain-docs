# Methodology

OpenZeppelin smart contracts play a crucial role in the world of decentralized applications and blockchain development.

## OpenZeppelin v4

To prove the OpenZeppelin smart contract compatibility with the VeChainThor blockchain the OpenZeppelin tests were performed using the Hardhat development environment and a custom plugin specifically designed to connect to the VeChainThor Node.

{% hint style="info" %}
The provider's functionality currently being used can be found in

[https://github.com/vechain/web3-providers-connex](https://github.com/vechain/web3-providers-connex)
{% endhint %}

A selection of failing tests were examined and bug fixes were suggested in pull requests. Since test cases include Hardhat specific tests, we opted to compare results against a non Hardhat network, specifically using the [Ganache plugin for Hardhat](https://hardhat.org/hardhat-runner/plugins/nomiclabs-hardhat-ganache).

## OpenZeppelin v5

Upgrading VeChainThor to the Shanghai EVM version, we want to ensure the OpenZeppelin contracts v5 are still compatible. In order to do so we prepared a custom OpenZeppelin contracts [fork](https://github.com/vechain/openzeppelin-contracts/tree/thor-compatibility) where all tests were adapted to run on VeChainThor. Since those tests are meant to be run against Hardhat network, multiple changes were made. Some test cases were removed (the end goal is not to test OpenZeppelin contracts themselves) because they cannot be run against a real blockchain and others were changed to reflect the VeChainThor responses.

To improve testing efficiency, we optimized the testing process and used the matrix feature in GitHub Actions for testing.

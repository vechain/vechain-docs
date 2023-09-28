# Methodology

OpenZeppelin smart contracts play a crucial role in the world of decentralized applications and blockchain development. To prove the OpenZeppelin smart contract compatibility with the VechainThor blockchain the OpenZeppelin tests were performed using the Hardhat development environment and a custom plugin specifically designed to connect to the VechainThor Node.&#x20;

{% hint style="info" %}
The provider's functionality currently being used can be found in&#x20;

[https://github.com/vechain/web3-providers-connex](https://github.com/vechain/web3-providers-connex)
{% endhint %}

A selection of failing tests were examined and bug fixes were suggested in pull requests. Since test cases include Hardhat specific tests, we opted to compare results against a non Hardhat network, specifically using the [Ganache plugin for Hardhat](https://hardhat.org/hardhat-runner/plugins/nomiclabs-hardhat-ganache).

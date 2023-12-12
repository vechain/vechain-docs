---
description: An intro and taxonomy of the different types of wallets.
---

# Wallets

### What are blockchain wallets?

A blockchain wallet, also known as a cryptocurrency wallet, is a software application or a physical hardware device used to store and manage cryptocurrency assets. It provides a way for individuals to interact with a blockchain network, enabling them to send, receive, and store digital assets such as vechain, bitcoin, ethereum and many more.

### How does a blockchain wallet work?

A blockchain wallet consists of two primary components: a public address and a private key. The public address serves as the wallet's identifier and is used to receive funds. It is similar to a bank account number, and you can freely share it with others to receive payments or transactions.

On the other hand, the private key is a secret cryptographic code that grants ownership and access to the funds stored in the wallet. A private key is like the pin to your credit card, it should be kept secure and never shared with anyone, as it enables control over the associated cryptocurrency assets.

{% hint style="danger" %}
Vechain nor any of it's affliates will ever request you to share your private key.\
\
Never share your private key, this will most likely result in a loss of assets.
{% endhint %}

### What are the different types of wallets and what are their use cases?

Wallets come in an wide variety of different implementations so it's important to research and choose a reputable wallet provider that aligns with your security preferences and cryptocurrency needs. Generally, a user makes a tradeoff between security and convenience when choosing a wallet.

In fact, its good practice to have multiple wallets for different use cases. We do this in the real world when dealing with fiat money, we have a wallet with some cash, a credit account in a bank to easily withdraw from and a savings account, which requires more effort and time to access funds. The below table defines some of the configurations a wallet can come in.

<table><thead><tr><th>Type</th><th width="326">Description</th><th width="139">Secure</th><th>Convienient</th></tr></thead><tbody><tr><td>Self-custody</td><td>Wallet provider doesn't manage PK.</td><td>High</td><td>Medium</td></tr><tr><td>Custodian</td><td>Manages PK for a user.</td><td>Low</td><td>High</td></tr><tr><td>Cold wallet</td><td>Wallet is not connected to the internet.</td><td>High</td><td>Low</td></tr><tr><td>Hot wallet</td><td>Wallet is connected to the internet.</td><td>Low</td><td>High</td></tr><tr><td>Web wallet</td><td>A wallet in a web browser.</td><td>Low</td><td>High</td></tr><tr><td>Software wallet</td><td>A downloadable application to use on laptop, phone or tablet.</td><td>Medium</td><td>Medium</td></tr><tr><td>Hardware wallet</td><td>A physical device designed to securely store PKs.</td><td>High</td><td>Low</td></tr><tr><td>Paper wallet</td><td>Printing a public address and PK on a physical piece of paper.</td><td>High</td><td>Low</td></tr></tbody></table>

**\*PK:** Private Key

The above entries are not mutually exclusive, for example, vechain's new VeWorld wallet is a self-custody, hot, web wallet.

### What's a seed phrase and why should I never give it to anyone?

A seed phrase is private key encoded in a human-readable format which typically consists of 12 or 24 randomly chosen words from a predefined word list. The seed phrase is a backup mechanism that allows users to restore their wallet and access their funds by generating the private keys. These words are generated using cryptographic algorithms that ensure they are unique and provide sufficient entropy to secure the private keys.

It is crucial to keep the seed phrase secure and confidential because anyone who possesses it can regenerate the private keys and gain access to the associated funds, irregardless of whether they are using the same wallet you currently use. It is recommended to store the seed phrase in a safe and offline location, such as writing it down on a piece of paper and keeping it in a secure place like a safe deposit box. Experts also advise storage in multiple locations, to protect yourself from a natural disaster destroying the paper the phrase is written on.

{% hint style="danger" %}
Vechain nor any of it's affliates will ever request you to share your seed phrase.\
\
Never share your seed phrase, this will most likely result in a loss of assets.
{% endhint %}

### Vechain Wallets

Vechain has a selection of wallets for you to use to securely and conveniently manage your vechain based assets.

<table data-view="cards"><thead><tr><th align="center"></th><th data-hidden data-card-target data-type="content-ref"></th></tr></thead><tbody><tr><td align="center">Sync</td><td><a href="sync/">sync</a></td></tr><tr><td align="center">Sync2</td><td><a href="sync2/">sync2</a></td></tr><tr><td align="center">VeWorld</td><td><a href="veworld.md">veworld.md</a></td></tr></tbody></table>

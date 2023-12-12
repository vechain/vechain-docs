---
description: >-
  This article will help you to understand how to use connex to build a dApp and
  also how it interacts with the user, application, and Sync2.
---

# Build a dApp by using Connex

## Prerequisites <a href="#something-you-might" id="something-you-might"></a>

1. Create a testnet wallet
   1. Download Sync2 [here](https://sync.vecha.in/)
   2. Launch Sync2
   3. Sync2 - [setup](../../core-concepts/wallets/sync2/user-guide/setup.md)
   4. Sync2 - [create testnet wallet](../../core-concepts/wallets/sync2/user-guide/wallet.md#custom-network-wallet)
2. Claim testnet token
   * Visit [Testnet faucet ](https://faucet.vecha.in/)- _sign certificate_

### Learn & play <a href="#learn-play" id="learn-play"></a>

#### connex.thor.ticker <a href="#connex-thor-ticker" id="connex-thor-ticker"></a>

The ticker is a concept that describes chain increment. When there is a new block added to the chain, the ticker will be triggered. This API will create a ticker that has a function that creates a Promise that will resolve when a new block is truly added, please be advised that it never rejects.

{% embed url="https://codepen.io/xjwx89/embed/rNGwvvL?default-tab=result&theme-id=light" %}

> 📖 Tips
>
> * **progress**: A number \[0-1] indicates the syncing progress of the currently connected node

ref: [connex API - create a ticker](../sdks-and-providers/connex/api-specification.md#create-a-ticker)

***

#### connex.thor.account <a href="#connex-thor-account" id="connex-thor-account"></a>

Account visitor is a bunch of APIs to get account details and interact with account methods.

{% embed url="https://codepen.io/xjwx89/embed/eYvGJJR?default-tab=result&theme-id=light" %}

> 📖 Tips
>
> * **balance**: hex form of VET balance in unit _wei_
> * **energy**: hex form of VTHO balance in unit _wei_
> * **hasCode**: when it equal to _true_, it means that its a smart contract

ref: [connex API - account visitor](../sdks-and-providers/connex/api-specification.md#account-visitor)

***

#### connex.thor.transaction <a href="#connex-thor-transaction" id="connex-thor-transaction"></a>

Transaction visitor is a bunch of APIs to get transaction details.

{% embed url="https://codepen.io/xjwx89/embed/gOmqjXm?default-tab=result&theme-id=light" %}

📖 Tips

> Transaction receipt
>
> * **reverted**: Several reasons can cause the transaction to revert. It means that the transaction data is passed through to a virtual machine(aka. VM) but not able to process. The most common reasons are `insufficient balance` and smart contract `not able to execute data`.
> * **gasPayer**: the address which paid the transaction fee. It is an important factor to determine the transaction is whether using fee delegation or not. If the transaction is paid by another address, the `txOrigin` and `gasPayer` will be different..
> * **txOrigin**: the address which signed the transaction

ref: [connex API - transaction visitor](../sdks-and-providers/connex/api-specification.md#transaction-visitor)

***

#### connex.thor.filter <a href="#connex-thor-filter" id="connex-thor-filter"></a>

It allows you to filter transfer and event logs on the blockchain. The filter usually works with `Connex.thor.account`, either creates a filter from an event or packs criteria and then assembles several criteria and sets them to a filter.

> 📖 Tips
>
> * **criteria**: is a set of an array which contain a `event.criteria` or `transfer.criteria`. The items in the criteria array will be combined by `OR` operator to filter the events:\
>   _example:_\
>   _\[{"ConA": "A"}, {"ConB": "B", "ConC": "C"}] is 'ConA=A `OR` (ConB=B `AND` ConC=C)'_
> * **filterRange**: Filtering a specific time frame transfer or event logs by setting `block number` or `timestamp` in second to the filter

**• transfer**

Filter VET transfer by setting the criteria to `txOrigin`,`sender`, and `recipient`.In addition, set the `filterRange` of filter to determine the transfer flog in the specific period

{% embed url="https://codepen.io/xjwx89/embed/RwVagQX?default-tab=result&theme-id=light" %}

**• event**

Filter event by setting criteria base on the contract methods(Contract ABI).

{% embed url="https://codepen.io/xjwx89/embed/xxdOxya?default-tab=result&theme-id=light" %}

ref: [connex API - filter](../sdks-and-providers/connex/api-specification.md#filter)

***

#### connex.vendor <a href="#connex-vendor" id="connex-vendor"></a>

In some cases, the application may not need the ability to access the entire blockchain. You can just create `connex.vendor` module instead of `connex.thor` module.`connex.vendor` is a way that allows dapps to interact with a _user_ such as signing a certificate or transaction.

**Certificate: connex.vendor.sign**

The certificate is a message signing-based mechanism that can easily request the user's `identification`(_address_) or user to agree to the `agreements`.

{% embed url="https://codepen.io/xjwx89/embed/xxqxPBv?default-tab=result&theme-id=light" %}

ref: [connex API - certificate signing service](../sdks-and-providers/connex/api-specification.md#certificate-signing-service)

***

**Transaction: connex.vendor.sign**

Signing a transaction is the most common interaction between dApp and user.A transaction may contains _one_ more _multiple_ clauses(operation) that requesting the user to _confirm_(sign) the transaction.

{% embed url="https://codepen.io/xjwx89/embed/OJprbQX?default-tab=result&theme-id=light" %}

📖 Tips

> * Transaction can contains multiple clauses and each clause contains three majors content: `to` ,`value` and `data`.
> * Provide a brief `comment` to the transaction or a clause to help the user to understand
> * Provide a `link` to reveal transaction-related information, the link will be used for connex to assemble a callback url by replacing the placeholder _{txid}_ by Transaction ID

ref: [connex API - transaction signing service](../sdks-and-providers/connex/api-specification.md#transaction-signing-service)

***

### Demos <a href="#demos" id="demos"></a>

#### 1. Buy an item with user login <a href="#_1-buy-an-item-with-user-login" id="_1-buy-an-item-with-user-login"></a>

{% embed url="https://codepen.io/xjwx89/embed/OJpeRmb?default-tab=result&theme-id=light" %}

#### 2. Token transfer <a href="#_2-token-transfer" id="_2-token-transfer"></a>

{% embed url="https://codepen.io/xjwx89/embed/RwpzWaq?default-tab=result&theme-id=light" %}

#### 3. Buy me a coffee <a href="#_3-buy-me-a-coffee" id="_3-buy-me-a-coffee"></a>

{% embed url="https://codepen.io/xjwx89/embed/PopgXWj?default-tab=result&theme-id=light" %}

**4. Address avatar**

> Address avatar is generated by [Picasso ](https://github.com/vechain/picasso)a general purpose deterministic identity icon library in svg format

{% embed url="https://codepen.io/xjwx89/embed/xxqBrwQ?default-tab=result&theme-id=light" %}

5\. Sign tx and check receipt

{% embed url="https://codepen.io/xjwx89/embed/vYmGymd?default-tab=result&theme-id=light" %}

#### 6. Estimate the transaction fee <a href="#_6-estimate-the-transaction-fee" id="_6-estimate-the-transaction-fee"></a>

> GasPriceCoef can be adjust by the user, thus, the result of the transaction fee is the minimum cost of the transaction.

{% embed url="https://codepen.io/xjwx89/embed/zYENZGE?default-tab=result&theme-id=light" %}

**Prerequisites**:

1. Need to know the _**Base gas price**_ from [params](../../start-building/tutorials/broken-reference/) contract
2. According to [transaction calculation](../../core-concepts/transactions/transaction-calculation.md)
   * we need to calculate the _**intrinsic gas**_
   * we need to know the _**vm gasUsed**_ (aka. virtual machine execution cost)

**Step 1: Get base gas price**

{% embed url="https://codepen.io/xjwx89/embed/RwLKREe?default-tab=result&theme-id=light" %}

**Step 2: Get intrinsic gas**

{% embed url="https://codepen.io/xjwx89/embed/QWqdKeq?default-tab=result&theme-id=light" %}

**Step 3: Get vm gas used**

{% embed url="https://codepen.io/xjwx89/embed/GRMrjzp?default-tab=result&theme-id=light" %}

**7. Enforce signer**

{% embed url="https://codepen.io/xjwx89/embed/rNGwvvL?default-tab=result&theme-id=light" %}

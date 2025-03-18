---
description: How to sign a transaction on VeWorld
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Signing

## Content type <a href="#content-type" id="content-type"></a>

There are two major types of signing contents:

| Type        | Purpose                                       |
| ----------- | --------------------------------------------- |
| Transaction | **Create** / **Transfer** / **Contract Call** |
| Certificate | **Identification** / **Agreement**            |

## Create a Token Transaction

{% tabs %}
{% tab title="Mobile" %}
Steps for creating a transaction:

1. Go to Dashboard
2. Tap **Send** button
3. Choose the asset you would like to send (VET, VTHO or a custom token you own), then tap **Next** button
4. Select the amount (in FIAT or token unit), then tap **Next** button
5. Enter or select the address you want to send tokens, then tap **Next** button
6. Select the delegation model you want
7. Select the priority for this transaction. It will change the fee you are paying
8. Check the details, then tap **Confirm** button
9. Authenticate with your security method, and wait for the confirm screen. You may see a link to the block explorer for the transaction details.
{% endtab %}

{% tab title="Browser Extension" %}
Steps for creating a transaction:

1. Go to Dashboard
2. Tap **Send** button
3. Choose the asset you would like to send (VET, VTHO or a custom token you own), then click **Next** button
4. Paste the address or vetdomain you want to send tokens to
5. Select the amount of tokens you want to send to, then click **Next** button
6. Select the delegation model you want, then click the **Sign & Send** button
7. Authenticate with your password, and wait for the confirm screen. You may see a link to the block explorer for the transaction details.
{% endtab %}
{% endtabs %}

## Create a NFT Transaction

{% tabs %}
{% tab title="Mobile" %}
1. Go to NFTs and choose the NFT you would like to send
2. Tap **Send** button
3. Enter or select the address you want to send tokens, then tap **Next** button
4. Select the delegation model you want
5. Select the priority for this transaction. It will change the fee you are paying
6. Check the details, then tap **Confirm** button
7. Authenticate with your security method, and wait for the confirm screen. You may see a link to the block explorer for the transaction details.
{% endtab %}

{% tab title="Browser Extension" %}
1. Go to NFTs and choose the NFT you would like to send
2. Click **Send NFT** button
3. Paste or select the destination address, then click **Send NFT** button
4. Select the delegation model you want, then click the **Sign & Send** button
5. Authenticate with your password, and wait for the confirm screen. You may see a link to the block explorer for the transaction details.
{% endtab %}
{% endtabs %}

## How to sign a certificate

{% tabs %}
{% tab title="Mobile" %}
1. Go to the **Discovery section** and go to your desired DApp
2. Connect your VeWorld wallet
3. If it's the first time that you interact with that DApp, you'll be asked to sign a certificate
4. Select the account you want to connect with, then tap **Connect**
5. You can check the details, then click "Sign"
6. Authenticate with your security method, and you'll be redirect to the DApp
{% endtab %}

{% tab title="Browser Extension" %}
1. Open in your browser your desired DApp
2. Connect your VeWorld wallet
3. If it's the first time that you interact with that DApp, you'll be asked to sign a certificate
4. You can check the details, then click "Sign"
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Signing a certificate doesn't result in a transaction. Such operations are stored in your wallet history only. There will be no trace onchain so that you don't need to pay any gas fees to approve them.
{% endhint %}

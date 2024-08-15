---
description: How to create, import and export wallets on VeWorld
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

# Wallet

## Create a new wallet

VeWorld is available as a mobile wallet and as a browser extension. The process to create a wallet is similar, the following sections will cover the differences

{% tabs %}
{% tab title="Mobile" %}
| Fresh Start                                                                                                                                                                                                                                      | Add a new one                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>The first time you install the app you should:</p><ol><li>Tap the <strong>Get Started</strong> button</li><li>Follow the steps below</li><li>Protect your wallet by choosing your favorite method (FaceId, Fingerprint or password)</li></ol> | <p>If you already have a wallet on VeWorld, and you want to create a new one:</p><ol><li>From your dashboard tap the top-right wallet icon <img src="../../../../.gitbook/assets/account_balance_wallet.svg" alt=""></li><li>Tap the <strong>Add Wallet</strong> button</li><li>Follow the steps below</li></ol> |

**Steps for a new wallet:**

1. Tap the **Create new wallet** button
{% endtab %}

{% tab title="Browser Extension" %}
| Fresh Start                                                                                                                                                                                                                                                      | Add a new one                                                                                                                                                                                                                                                                                                                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>The first time you install the extension you should:</p><ol><li>Follow and complete or skip the <em>welcome wizard</em></li><li>Type your favorite password twice and then click the <strong>CONFIRM</strong> button</li><li>Follow the steps below</li></ol> | <p>If you already have a wallet on VeWorld, and you want to create a new one:</p><ol><li>From your dashboard tap the top-right 3-dots icon <img src="../../../../.gitbook/assets/more_vert.svg" alt=""></li><li>Select <strong>Manage Wallets</strong></li><li>Click the <strong>Add Wallet</strong> button</li><li>Follow the steps below</li></ol> |

**Steps for a new wallet:**

1. Click the **Create wallet** button
2. Follow and complete or skip the _security wizard_
3. Read and store your mnemonic
4. Mark the checkbox that states you saved your mnemonic safely
5. Pass the quiz with the 3 words from your mnemonic
6. Click the **GO TO HOMEPAGE** button
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Once the wallet is created, we recommend you backup it immediately.

The mnemonic words store all the information needed at any point in time to recover your wallet.

The mnemonic must be stored in a secure place, preferably offline. The mnemonic allows you to regain wallet access in a scenario where your device is lost, stolen, or unusable due to any reason.
{% endhint %}

## Import a wallet

### Import a local wallet

{% tabs %}
{% tab title="Mobile" %}
| Fresh Start                                                                                                                                                                                                                                      | Add a new one                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>The first time you install the app you should:</p><ol><li>Tap the <strong>Get Started</strong> button</li><li>Follow the steps below</li><li>Protect your wallet by choosing your favorite method (FaceId, Fingerprint or password)</li></ol> | <p>If you already have a wallet on VeWorld, and you want to import a new one:</p><ol><li>From your dashboard tap the top-right wallet icon <img src="../../../../.gitbook/assets/account_balance_wallet.svg" alt=""></li><li>Tap the <strong>Add Wallet</strong> button</li><li>Follow the steps below</li></ol> |

Steps for importing a local wallet from **mnemonic**:

1. Tap the **Import Wallet** button
2. Tap **Local wallet**
3. Paste or type your saved mnemonic and then tap **VERIFY** button

Steps for importing a local wallet from **private key**:

1. Tap the **Import Wallet** button
2. Tap **Local wallet**
3. Paste your saved private key and then tap **VERIFY** button

Steps for importing a local wallet from a **keystore file**:

1. Tap the **Import Wallet** button
2. Tap **Local wallet**
3. Paste the content of your saved keystore file and then tap **VERIFY** button
{% endtab %}

{% tab title="Browser Extension" %}
| Fresh Start                                                                                                                                                                                                                                                                                                                                               | Add a new one                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>The first time you install the app you should:</p><ol><li>Follow and complete or skip the <em>welcome wizard</em></li><li>Type your favorite password twice and then click the <strong>CONFIRM</strong> button</li><li>Protect your wallet by choosing your favorite method (FaceId, Fingerprint or password)</li><li>Follow the steps below</li></ol> | <p>If you already have a wallet on VeWorld, and you want to create a new one:</p><ol><li>From your dashboard tap the top-right 3-dots icon <img src="../../../../.gitbook/assets/more_vert.svg" alt=""></li><li>Tap the <strong>Add Wallet</strong> button</li><li>Follow the steps below</li></ol> |

Steps for importing a local wallet from **mnemonic**:

1. Click the **Import wallet** button
2. In the first section _Local Wallet_ click the **Import Wallet** button
3. In the first section _Mnemonic_ click the **Import from Mnemonic** button
4. Type or paste your mnemonic then click the **Verify** button
5. Type your wallet password

Steps for importing a local wallet from **private key**:

1. Click the **Import wallet** button
2. In the first section _Local Wallet_ click the **Import Wallet** button
3. In the second section _Private Key or Keystore file_ click the **Import from Private Key** button
4. Paste your privatekey then click the **Verify** button
5. Type your wallet password

Steps for importing a local wallet from **keystore file**:

1. Click the **Import wallet** button
2. In the first section _Local Wallet_ click the **Import Wallet** button
3. In the second section _Private Key or Keystore file_ click the **Import from keystore file** button
4. Upload your keystore file then click the **Decrypt** button
5. Type your wallet password
{% endtab %}
{% endtabs %}

### Import a Ledger wallet

{% tabs %}
{% tab title="Mobile" %}
| Fresh Start                                                                                                                                                                                                                                      | Add a new one                                                                                                                                                                                                                                                                                                    |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>The first time you install the app you should:</p><ol><li>Tap the <strong>Get Started</strong> button</li><li>Follow the steps below</li><li>Protect your wallet by choosing your favorite method (FaceId, Fingerprint or password)</li></ol> | <p>If you already have a wallet on VeWorld, and you want to import a new one:</p><ol><li>From your dashboard tap the top-right wallet icon <img src="../../../../.gitbook/assets/account_balance_wallet.svg" alt=""></li><li>Tap the <strong>Add Wallet</strong> button</li><li>Follow the steps below</li></ol> |

Steps for importing a Ledger wallet:

1. Tap the **Import Wallet** button
2. Tap the **Hardware Wallet** button
3. Select your Ledger, then tap the **Import** button
4. Follow the instructions and tap the **Continue** button
5. Select your desired Account, then tap the **Import** button
6. Tap the **GO TO YOUR WALLET** button
{% endtab %}

{% tab title="Browser Extension" %}
| Fresh Start                                                                                                                                                                                                                                                                                                                                               | Add a new one                                                                                                                                                                                                                                                                                       |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p>The first time you install the app you should:</p><ol><li>Follow and complete or skip the <em>welcome wizard</em></li><li>Type your favorite password twice and then click the <strong>CONFIRM</strong> button</li><li>Protect your wallet by choosing your favorite method (FaceId, Fingerprint or password)</li><li>Follow the steps below</li></ol> | <p>If you already have a wallet on VeWorld, and you want to create a new one:</p><ol><li>From your dashboard tap the top-right 3-dots icon <img src="../../../../.gitbook/assets/more_vert.svg" alt=""></li><li>Tap the <strong>Add Wallet</strong> button</li><li>Follow the steps below</li></ol> |

Steps for importing a Ledger wallet:

1. In the second section click the **Import wallet** button
2. In the second section _Hardware Wallet_ click the **Import Wallet** button
3. Follow the instructions and click the **Ledger** button
4. Follow the instructions and click the **Continue** button
5. Select your desired account then click the **Add** button
{% endtab %}
{% endtabs %}

### Import an Observable wallet

{% tabs %}
{% tab title="Mobile" %}
Steps for importing an observable wallet:

1. From your dashboard tap the top-right wallet icon ![](../../../../.gitbook/assets/account\_balance\_wallet.svg)
2. Tap the **Add Wallet** button
3. Tap the **Observe Wallet** button
4. Tap **Local wallet**
5. Paste the desired address, then tap **IMPORT** button
{% endtab %}

{% tab title="Browser Extension" %}
Not available yet on the Extension.
{% endtab %}
{% endtabs %}

## Export a wallet

{% tabs %}
{% tab title="Mobile" %}
Steps for exporting a local wallet:

1. Tap the bottom right icon ![](../../../../.gitbook/assets/settings.svg) to the **Settings** page
2. Tap **Privacy and Security** from the menu
3. Tap **Backup your mnemonic phrase**
4. Select the local wallet you want to export
5. Pass the authentication (fingerprint, faceid or password)
6. Paste or type your saved mnemonic and then tap **VERIFY** button
7. Read or copy to clipboard your mnemonic
{% endtab %}

{% tab title="Browser Extension" %}
Steps for exporting a local wallet:

1. Click the bottom right icon ![](../../../../.gitbook/assets/settings.svg) to **Settings** page
2. Click **Privacy and Security** from menu
3. Click **Backup mnemonic**
4. Select the local wallet you want to export, then click the **Continue** button
5. Type your password
6. Read or copy to clipbaord your mnemonic
{% endtab %}
{% endtabs %}

## Manage your wallets

With VeWorld you can handle multiple wallets and multiple accounts.

{% hint style="info" %}
Acconts of the same wallet share the same mnemonic. Different wallets have different mnemonic.
{% endhint %}

Feel free to self-organize your wallets as you prefer.

{% tabs %}
{% tab title="Mobile" %}
Change the order of your wallets

1. From your dashboard tap the top-right wallet icon ![](../../../../.gitbook/assets/account\_balance\_wallet.svg)
2. Tap the icon order-change ![](../../../../.gitbook/assets/low\_priority.svg)
3. Move your wallets to your favorite order
4. Tap the **Save** button

Rename a wallet

* From your dashboard tap the top-right wallet icon ![](../../../../.gitbook/assets/account\_balance\_wallet.svg)
* Select the wallet by pressing the pencil icon
* Change the name of your wallet

Add an account to a wallet

* From your dashboard tap the top-right wallet icon ![](../../../../.gitbook/assets/account\_balance\_wallet.svg)
* Select the wallet
* Tap the **Add Account** button
* (optional) Rename it by tapping the name of the new account

Remove a wallet

* From your dashboard tap the top-right wallet icon ![](../../../../.gitbook/assets/account\_balance\_wallet.svg)
* Hold for a second the wallet you want to remove and swipe to the left
* Press the trash icon
* Confirm by tapping the **Remove Wallet** button
{% endtab %}

{% tab title="Browser Extension" %}
Change the order of your wallets: not available on Extension.

Rename a wallet

* From your dashboard click the top-right wallet icon![](../../../../.gitbook/assets/more\_vert.svg)
* Click on **Manage Wallets**
* Click on the pencil icon of the wallet you want to change
* Type the new name, then click the **Save Changes** button

Add an account to a wallet

* From your dashboard click the top-right wallet icon![](../../../../.gitbook/assets/more\_vert.svg)
* Click on **Manage Wallets**
* Click the **Add Account** link close to the desired wallet
* (optional) Rename the account by clicking the pencil icon

Remove a wallet: not available on Extension
{% endtab %}
{% endtabs %}

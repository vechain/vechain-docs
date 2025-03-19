---
description: How to customize your wallet
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

# Settings

{% tabs %}
{% tab title="Mobile" %}
### General

**Conversion Currency**

You can choose among the supported FIAT currencies (EUR, USD)

**Currency Format**  

You can choose how the fiat value of your assets appears in the wallet.  

- **Comma:** Uses a comma as a separator for the decimal value (e.g., 9.999,99).  
- **Dot:** Uses a dot as a separator for the decimal value (e.g., 9,999.99).  
- **System:** Uses your device's system settings to automatically set the preference based on your region.  

**Symbol Position**  

You can choose where the €/$ symbol is displayed in relation to the fiat value of your assets.  

- **Before amount:** The symbol appears before the amount (e.g., $9999).  
- **After amount:** The symbol appears after the amount (e.g., 9999$).  

**Theme**

You can anytime switch between the dark or light theme, or just use your device settings.

**App Language**

VeWorld is now a multi-language wallet and language preferences can be set in the general settings section.

## 🌍 Supported Languages
- 🇬🇧 English  
- 🇯🇵 Japanese  
- 🇻🇳 Vietnamese  
- 🇩🇪 German  
- 🇳🇱 Dutch  
- 🇰🇷 Korean  
- 🇮🇹 Italian  
- 🇨🇳 Chinese  
- 🇸🇪 Swedish  
- 🇫🇷 French  
- 🇹🇼 Taiwanese  
- 🇪🇸 Spanish  
- 🇹🇷 Turkish  
- 🇮🇳 Hindi  
- 🇵🇱 Polish  
- 🇵🇹 Portuguese  
- 🇷🇺 Russian  

🚨 **Dev Alert**

To create a more immersive and consistent user experience, when opening a dApp from VeWorld mobile, we have implemented a way to provide the current language preference of VeWorld to the dApp. There are two ways to retrieve this information, depending on whether your app is **server-side rendered (SSR)** or **client-side rendered (CSR, non-SSR)**.

**Server side rendered (SSR) Apps**

If your application is SSR, you can obtain the language preference from the `Accept-Language` header. This will provide the current locale set in VeWorld.  

**Client-Side Rendered (CSR) / Frontend Apps (Non-SSR)**

If your application its not SSR, to get access to the current language used in VeWorld you can do it simply using the **injected JavaScript property** that you can get it using window.vechain.acceptLanguage.


**Reset**

You can hard reset your wallet, and clear all your local data. This action cannot be reverted.

{% hint style="warning" %}
If you are going to reset your wallet without your backups properly saved, you'll loose access to all your assets.
{% endhint %}

### Transaction

**Default delegation**

You can select the default delegation for your transactions.

**Delegations URLs**

You can create a shortlist of delegation urls you could choose easily from.

### Networks

**Select**

You can choose between Mainnet or Testnet. You could also use a custom node.

### Contacts

You can manage a list of favourite contacts, to make the trasaction creation process easier.

### Security and Privacy

**Security Method**

You can choose your favorite security method. Downgrading the level of security is not allowed.

**Backup mnemonic**

You can export a local wallet; your password will be required.

### Connected Applications\*\*

You can see and manage the list of DApps you interacted with.

### About VeWorld

Here you can see:

* the release number of your current version.
* the Official Website
* the privacy policy
* the help platform
{% endtab %}

{% tab title="Browser Extension" %}
### General

**Conversion Currency**

You can choose among the supported FIAT currencies (EUR, USD)

**Symbol Position**  

You can choose where the €/$ symbol is displayed in relation to the fiat value of your assets.  

- **Before amount:** The symbol appears before the amount (e.g., $9999).  
- **After amount:** The symbol appears after the amount (e.g., 9999$).  

**App Language**

VeWorld is now a multi-language wallet and language preferences can be set in the general settings section.

## 🌍 Supported Languages
- 🇬🇧 English  
- 🇯🇵 Japanese  
- 🇻🇳 Vietnamese  
- 🇩🇪 German  
- 🇳🇱 Dutch  
- 🇰🇷 Korean  
- 🇮🇹 Italian  
- 🇨🇳 Chinese  
- 🇸🇪 Swedish  
- 🇫🇷 French  
- 🇹🇼 Taiwanese  
- 🇪🇸 Spanish  
- 🇹🇷 Turkish  
- 🇮🇳 Hindi  
- 🇵🇱 Polish  
- 🇵🇹 Portuguese  
- 🇷🇺 Russian  

**Hide tokens without balance**

If your balance of a selected token is zero, it won't get it displayed on the dashboard.

**Enable DEV mode**

You can execute transactions even when warnings would block you from doing so. A failing reason will be shown after the transaction fails.

**Theme**

You can anytime switch between the dark or light theme, or just use your device settings.

**State Logs**

State logs contain your public account addresses and sent transactions. You can download log file for diagnosis purposes.

**Reset**

You can hard reset your wallet, and clear all your local data. This action cannot be reverted.

{% hint style="warning" %}
If you are going to reset your wallet without your backups properly saved, you'll loose access to all your assets.
{% endhint %}

### Transaction

**Default delegation**

You can select the default delegation for your transactions.

**Delegations URLs**

You can create a shortlist of delegation urls you could choose easily from.

### Networks

**Select**

You can choose between Mainnet or Testnet. You could also use a custom node.

**Indicators**

Display an indicator when transacting on another network

**Conversion**

Show fiat exchange rates when on other networks

### Contacts

You can manage a list of favourite contacts, to make the trasaction creation process easier.

### Security and Privacy

**Password authorisation for transactions**

Require the extension password when performing transactions with local wallets

**Change Password**

You can change your local password

**Backup mnemonic**

You can export a local wallet; your password will be required.

**Analytics tracking**

You can allow or block the tracking of your wallet. No personal data are collected.

### Connected Applications\*\*

You can see and manage the list of DApps you interacted with.

### About VeWorld

Here you can see the release number of your current version.

### Bug Report

You can open a ticket for an issue or suggestions.
{% endtab %}
{% endtabs %}

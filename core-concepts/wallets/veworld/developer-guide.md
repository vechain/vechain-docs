# Developer Guide

## How can I add VeWorld Wallet integration into my dApp?

You can look at our [dAppKit](../../../developer-resources/sdks-and-providers/dapp-kit/README.md).

The vechain dApp kit is a frontend library designed to make it easy to build dApps on the VechainThor blockchain. This documentation provides a comprehensive guide to using the dApp kit library, including installation, usage instructions, and details about its key features and methods.

## How can I open a dApp in Mobile Browser?

We developed two universal link standards (with or without the redirect), that should support your marketing needs.

### Solution 1

Here's an example: [https://www.veworld.com/discover/browser/ul/https%3A%2F%2Fmugshot.vet](https://www.veworld.com/discover/browser/ul/https%3A%2F%2Fmugshot.vet)

If you open this link in your mobile device and VeWorld is installed, the user will be redirected to the desired dApp. If it isn't installed, the user will be leaded to veworld.com website to let him install the wallet.

As you can see the url structure is `https://www.veworld.com/discover/browser/ul/` + `Your URL encoded`.

### Solution 2

Here's an example: [https://www.veworld.com/discover/browser/redirect/ul/https%3A%2F%2Fmugshot.vet](https://www.veworld.com/discover/browser/redirect/ul/https%3A%2F%2Fmugshot.vet)
With this solution the user will be leaded to the dApp Url instead of veworld.com (if there's no VeWorld in the device).

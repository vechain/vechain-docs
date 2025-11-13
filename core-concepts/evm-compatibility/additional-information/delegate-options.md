# Delegate Options

Vechain supports delegating transaction fees to a different address in order for users to be able to easily use services without the friction of high transaction fees. We have added an option in our `hardhat-toolbox` plugin in order for a user to be able to use delegate options when using our plugin. The following is part of a sample `hardhat.config.js` file with empty delegate options.

```javascript
vechain: {
  url: "http://127.0.0.1:8669",
  accounts: {
    mnemonic: "denial kitchen pet squirrel other broom bar gas better priority spoil cross",
    count: 10,
  },
  restful: true,
  gas: 10000000,
  delegate: {
    url: "",
    signer : ""
  },
},
```

The relevant options in this case are the delegate url and delegate signer options. The signer should contain the address of the delegator or sponsor what will pay for the transaction fees and the url should contain the url of the delegator's service.

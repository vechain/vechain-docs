# Configure and Run the Trampoline Wallet

## Get Resources

Clone [Trampoline's repository](https://github.com/eth-infinitism/trampoline):

```bash
git clone git@github.com:eth-infinitism/trampoline.git
```

## Configure and run

* Install dependencies

```bash
cd trampoline && yarn install
```

* Modify `src/exconfig.ts` to include:
* Where the `Account_Factory_Address` is the address of the `SimpleAccountFactory` from [this](../../../start-building/tutorials/account-abstraction/broken-reference/) tutorial.

```typescript
export default {
  ...,
  factory_address: '<ACCOUNT_FACTORY_ADDRESS>',
  ....
  network: {
    chainID: '246',
    family: 'EVM',
    name: 'VeChain',
    provider: 'http:/localhost:8669',
    entryPointAddress: '<ENTRYPOINT_ADDRESS>',
    bundler: 'http://localhost:3000/rpc',
    baseAsset: {
      symbol: 'VET',
      name: 'VET',
      decimals: 18,
      image:
        'https://www.vechain.org/wp-content/uploads/2023/03/254Risorsa-2.svg',
    },
  },
};
```

* Start and wait for the build to finish

```bash
yarn start
```

* Sample output

```
yarn run v1.22.19
$ QUIET=false NODE_ENV=development run-p devtools "dev {@}" --
$ npx redux-devtools --hostname=localhost --port=8000 --open
$ npx hardhat clean && npx hardhat compile && webpack --config webpack.config.js --watch
[ReduxDevTools] Start server...
--------------------------------------------------------------------------------

   [Done] Migrations are finished

Generating typings for: 1 artifacts in dir: src/pages/Account/account-api/typechain-types for target: ethers-v5
Successfully generated 6 typings!
Compiled 1 Solidity file successfully
assets by info 552 KiB [immutable]
  assets by path *.woff2 259 KiB 28 assets
  assets by path *.woff 256 KiB 4 assets
  + 2 assets
assets by path *.js 47.9 MiB
  assets by chunk 1.78 MiB (id hint: vendors) 5 assets
  + 8 assets
assets by path *.html 980 bytes
  asset app.html 397 bytes [emitted]
  asset options.html 298 bytes [emitted]
  asset popup.html 285 bytes [emitted]
asset icon-128.png 44.7 KiB [emitted] [from: src/assets/img/icon-128.png] [copied]
asset icon-34.png 11.6 KiB [emitted] [from: src/assets/img/icon-34.png] [copied]
asset dapp_favicon_default@2x.png 2.69 KiB [emitted] [from: src/assets/img/dapp_favicon_default@2x.png] [copied]
asset manifest.json 578 bytes [emitted] [from: src/manifest.json] [copied]
12660 modules
webpack 5.75.0 compiled successfully in 14830 ms
```

## Run Chrome Extension

Trampoline has been verified to work in Chromium, the examples can be applied to other browsers as well.

* Navigate to `chrome://extensions/` and enable Developer Mode

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

* Select `Load Unpacked,` then navigate to, and select `trampoline/build` which should open

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

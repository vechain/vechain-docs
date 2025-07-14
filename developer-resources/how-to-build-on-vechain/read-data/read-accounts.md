# Read Accounts

An account can be classified as either an externally owned account or a smart contract. Externally owned accounts typically consist of private keys generated in wallets, whereas smart contracts are deployed with specific program code.

The distinction between the two can be made by examining an account's `hasCode` flag. If it's `true`, it indicates that a smart contract is deployed at that address. For smart contracts, the byte code can also be retrieved.

An account possesses three key attributes:

* **hasCode** to indicate a smart contract at the address
* **balance** to represent the VET balance
* **energy** to denote the VTHO balance

The balance is stored as a hex-encoded BigInt, which can be converted into a human-readable format using `BigInt(balance)`. It's important to note that numbers are stored with all their decimals, and for a more readable version, 18 decimal places should be considered.

Here's an example snippet for accessing account details for the VTHO contract:

```js
const contract = await thor.accounts.getAccount(
  '0x0000000000000000000000000000456e65726779' // <- whatever EOA or Smart contract
);
const bytecode = await thor.accounts.getBytecode(
  '0x0000000000000000000000000000456e65726779' // <- whatever Smart contract
);
```

Test it yourself:

{% embed url="https://stackblitz.com/edit/ts-vechain-academy-get-account-info?embed=1&file=index.ts&hideExplorer=1&hideNavigation=1&view=editor" %}

Type definition and documentation of all attributes:

* [Account Detail](https://vechain.github.io/vechain-sdk-js/classes/_vechain_sdk_network.AccountDetail.html)

The same information is available using the JSON-API:

* [GET /accounts/{address}](https://mainnet.vechain.org/accounts/0x0000000000000000000000000000456e65726779)
* [GET /accounts/{address}/code](https://mainnet.vechain.org/accounts/0x0000000000000000000000000000456e65726779/code)

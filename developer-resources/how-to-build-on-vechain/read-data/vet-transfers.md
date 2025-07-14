# VET Transfers

## `filterTransferLogs(criteria)`

The VeChain token `VET` does not have a contract tied to it, so its transfers must be accessed from a different source.

Using `logs.filterTransferLogs` gives you access to the transfers, with the same filter options, but the `criteriaSet` is specifically tailored for transfer events.

Each criteria may include:

* **recipient**: the address that receives VET
* **txOrigin**: the address that initiated the transfer transaction
* **sender**: the address that sent the VET

A sample request with all filters would appear as follows:

```js
// access VET transfers
const logs = await thor.logs.filterTransferLogs({
  options: {
    offset: 0,
    limit: 3,
  },
  range: {
    unit: 'block',
    from: 0,
    to: 20000000,
  },
  criteriaSet: [
    {
      // VET receiver
      recipient: '0x000000000000000000000000000000000000dead',

      // transaction signer/origin
      txOrigin: '0x19135a7c5c51950b3aa4b8de5076dd7e5fb630d4',

      // VET sender
      sender: '0x19135a7c5c51950b3aa4b8de5076dd7e5fb630d4',
    },
  ],
  order: 'asc',
});
```

Multiple optional criteria can be configured to filter for various addresses.

Type definition and documentation of all options and results:

* [Filter Transfer Log Options](https://vechain.github.io/vechain-sdk-js/interfaces/_vechain_sdk_network.FilterTransferLogsOptions.html)
* [Transfer Logs](https://vechain.github.io/vechain-sdk-js/interfaces/_vechain_sdk_network.TransferLogs.html)

### Example Project

{% embed url="https://stackblitz.com/edit/ts-vechain-academy-read-logs-vet-transfers?embed=1&file=index.ts&hideExplorer=1&hideNavigation=1&view=editor" %}

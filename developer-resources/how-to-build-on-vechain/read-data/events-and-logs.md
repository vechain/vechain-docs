# Events & Logs

Events are signals that are emitted from smart contracts. Every event is logged, immutable and accessible using a blockchain node only. Smart contracts can not access events themselves.

Client-Applications can either listen to events and act accordingly or use logged events to access historical data.

The example uses a public contract and paginates thru the results.

## Example Data

This example used below will utilize the VTHO contract, which manages VeChain's VTHO Token.

* Smart Contract Address: `0x0000000000000000000000000000456e65726779`
* The contract's source code can be found on GitHub at: [https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol](https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol)
* Its Application Binary Interface (ABI) is shared on b32, a repository that gathers publicly available interfaces for VeChain projects: [https://gitabihub.com/vechain/b32/blob/master/ABIs/energy.json](https://github.com/vechain/b32/blob/master/ABIs/energy.json)

## `contracts.load(address, abi)`

A contract instance using address and ABI definition provides instant access to logs.

### Create Contract Object

To filter events, just like with any other interaction, a contract object needs to be created. It requires to specify a network first, because in general a contract with a specific address only exists on one network

```javascript
import { HttpClient, ThorClient } from '@vechain/sdk-network';
import { ErrorDecoder } from 'ethers-decode-error';
import energyAbi from './energy.json' assert { type: 'json' };

const thor = ThorClient.at('https://testnet.vechain.org/');
const vtho = thor.contracts.load(
  '0x0000000000000000000000000000456e65726779',
  energyAbi
);

```

{% hint style="info" %}
The Contract-Loader always requires a JSON ABI Definition.

Fragments are not supported.
{% endhint %}

### `contract.filters.<EventName>(output)`

The filters provide a simple way to access events in a human-readable way and to populate log requests with the correct criteria. The feature is available for every "event available in the ABI of the contract. In the case of VTHO `Transfers` and `Approvals`, emitted every time a user calls _transfer_ and _approve_ respectively.

For example, a filter for all `Transfers` can be created using:

```ts
const allTransfers = vtho.filters.Transfer()
const filteredTransfers = vtho.filters.Transfer(<from>, <to>)
```

Another example filters for all transfers to a specific address:

```ts
const filteredTransfers = vtho.filters.Transfer(null, <to>)
```

`_to` is the second output of the ABI. Unwanted filters needs to be skipped by passing null. \
There's a third one for the Transfer event, which is `_value`.&#x20;

To filter all transfers of a specific value use:

```typescript
const filteredTransfers = vtho.filters.Transfer(null, null, <value>)
```

### Get Logs

To receive the logs from the blockchain, the built filter object provides a `.get()` function. Calling it will return the list of matching events.

```ts
const allTransfers = vtho.filters.Transfer()
const result = await allTransfers.get()
```

For pagination, there are three optional parameters that allow filtering for a specific range, paginating, and ordering the result set. All options are optional:

```ts
.get(
 { unit?: 'block' | 'time', from?: number, to?: number },
 { offset?: number, limit?: number },
 'asc' | 'desc'
)
```

### Browse Results

`.get()` returns a list of results because it can support multiple requests as well.

The data is available in both raw and decoded forms:

```ts
const transfers = vtho.filters

  // pass filters in the order of the input definition for the event
  // skip values by passing null or undefined
  .Transfer(null, '0x0000000000000000000000000000456e65726779');

const results = await transfers.get(null, { limit: 2})

results.forEach(result => {
    result.forEach(log => {
        // raw log data
        console.log(log)

        // access to decoded data
        console.log("Transfer", log.decodedData._from, log.decodedData._to, log.decodedData._value)
    })
})

```

### Example Project

{% embed url="https://stackblitz.com/edit/vechain-energy-example-snippets-1puuxszb?ctl=1&embed=1&file=index.mjs&hideExplorer=1&view=editor" %}

### `filterEventLogs()`: Multiple Events in one Request

With `filterEventLogs()`, logs for multiple events can be requested in a single request, improving network performance and simplifying interaction.

For example, requesting VTHO Transfers from and to an address in one request:

```ts
const results = await thor.logs.filterEventLogs({
  criteriaSet: [
    ...vtho.filters.Transfer(ZERO_ADDRESS).criteriaSet, // FROM Zero
    ...vtho.filters.Transfer(null, ZERO_ADDRESS).criteriaSet, // TO Zero
  ],
  range: {
    unit: 'block',
    from: 1_000_000,
    to: 20_000_000,
  },
});

results.forEach((result) => {
  result.forEach((log) => {
    console.log(
      'Transfer',
      log.decodedData._from,
      log.decodedData._to,
      log.decodedData._value
    );
  });
});
```

## `filterRawEventLogs(criteria)`

### Request Logs

Due to the potentially large amount of log entries, it is essential to implement filtering and pagination mechanisms for efficient data access.

To access and retrieve logs, the `logs.filterRawEventLogs` function allows filtering based on a specified range and enables pagination by utilizing offset and limits.

Illustrated in the following example is the process of retrieving transfer events for VTHO tokens. Initially, the event that requires filtering must be encoded into a byte format.

```js
import { ABIEvent } from '@vechain/sdk-core';

const event = new ABIEvent(
  'event Transfer(address indexed from, address indexed to, uint256 amount)'
);
const encodedTopics = event.encodeFilterTopics([])
```

`indexed` variables can be filtered directly in the filter request, providing fast access to a subset of information. The list argument on the encoding can provide them.

Our example will filter for the second variable `to`:

```js
const encodedTopics = event.encodeFilterTopics([
  // first indexed value is "from", set to null to not use it
  null,

  // second indexed value is "to"
  '0x0000000000000000000000000000456e65726779',
]);
```

With the encoded version `logs.filterRawEventLogs` can be called to return all matching logs:

```js
const filteredLogs = await thor.logs.filterRawEventLogs({
  criteriaSet: [
    // filter by address and topics, empty topics are ignored
    {
      address: '0x0000000000000000000000000000456e65726779',
      topic0: encodedTopics[0],
      topic1: encodedTopics[1],
      topic2: encodedTopics[2],
      topic3: encodedTopics[3],
      topic4: encodedTopics[4],
    },
  ]
});
```

For pagination `options` (`{ offset?: number, limit?: number }`) and `order` (`'asc' | 'desc'`) can be passed as additional parameter. Additionally the logs can be restricted to a certain block range by defining a `range` (`{ unit?: 'block' | 'time', from?: number, to?: number }`).

You can find the full documentation in the description of the [Filter Event Logs Options](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.FilterEventLogsOptions.html).

### **Handle Response**

The response needs to be decoded using the event definition to gain access to all information. `event.decodeEventLog(log)` can be used on a selected event or in our example on all returned logs:

```js
const decodedLogs = filteredLogs.map(log => event.decodeEventLog(log))
```

Each decoded log will have an attribute for each event variable, like `decodedLog.from` and can alternatively be accessed as list in the order of the event parameter definition (`decodedLog[0]` equals `from`).

The types of the results are fully documented in the [Event Logs Interface.](https://tsdocs.dev/docs/@vechain/sdk-network/latest/interfaces/network.EventLogs.html)

### Example Project

{% embed url="https://stackblitz.com/edit/vechain-energy-example-snippets-rjc98gta?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

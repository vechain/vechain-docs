# Events & Logs

Events are signals that are emitted from smart contracts. Every event is logged, immutable and accessible using a blockchain node only. Smart contracts can not access events themself.

Client-Applications can either listen to events and act accordingly or use logged events to access historical data.

The example uses a public contract and paginates thru the results.

## Example Data

This example used below will utilize the VTHO contract, which manages Vechain's VTHO Token.

* Smart Contract Address: `0x0000000000000000000000000000456e65726779`
* The contract's source code can be found on GitHub at: [https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol](https://github.com/vechain/thor/blob/f58c17ae50f1ec8698d9daf6e05076d17dcafeaf/builtin/gen/energy.sol)
* Its Application Binary Interface (ABI) is shared on b32, a repository that gathers publicly available interfaces for Vechain projects: [https://github.com/vechain/b32/blob/master/ABIs/energy.json](https://github.com/vechain/b32/blob/master/ABIs/energy.json)

## `filterEventLogs(criteria)`

### Request Logs

Due to the potentially large amount of log entries, it is essential to implement filtering and pagination mechanisms for efficient data access.

To access and retrieve logs, the `logs.filterEventLogs` function allows filtering based on a specified range and enables pagination by utilizing offset and limits.

Illustrated in the following example is the process of retrieving transfer events for VTHO tokens. Initially, the event that requires filtering must be encoded into a byte format.

```js
import { abi } from '@vechain/sdk-core';

const event = new abi.Event(
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

With the encoded version `logs.filterEventLogs` can be called to return all matching logs:

```js
const filteredLogs = await thor.logs.filterEventLogs({
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

{% embed url="https://stackblitz.com/edit/vechain-sdk-read-logs-filtereventlogs?ctl=1&embed=1&file=index.mjs&hideExplorer=1&hideNavigation=1&view=editor" %}

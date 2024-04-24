# Listen to Changes

WebSockets provide the ability to receive a stream of all changes on Vechain, reducing the number of network requests that are normally associated with polling data at regular intervals.

The available streams for changes are:

1. Events that are emitted from contracts
2. Blocks appended to the Blockchain
3. VET Transfers occurring between addresses
4. Transactions added to the transaction pools
5. Beats of new blocks which can be used to check if the block contains a specific account

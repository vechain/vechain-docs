# Update Subgraph

To update a subgraph without causing service interruptions, deploy it to a different namespace.

Subgraphs are identified by their IPFS CID. Re-compiling and uploading the same subgraph to IPFS will always result in the same CID.

The graph node points subgraph namespaces to the IPFS CID, allowing multiple namespaces to use the same subgraph index.

This method allows for seamless updates. Deploy new subgraphs to a staging namespace first. Once they are fully synchronized and tested, deploy them to the production namespace. This way, the production namespace will immediately point to the already synchronized subgraph.

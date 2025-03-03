# Practical Implications for Developers: Key Considerations

Developers migrating from Ethereum or building new dApps on VeChainThor must consider these differences:

1. **Transaction Structure:**

Ethereum transactions are _incompatible_ with VeChainThor. Developers _must_ construct transactions using the VeChainThor format. Libraries provided in vechain-sdk-j are essential for this. Here follows the transaction body structure:

<table><thead><tr><th width="153">Field</th><th width="147">Type</th><th width="135">JSON Key</th><th>Description</th></tr></thead><tbody><tr><td>ChainTag</td><td>byte</td><td>chainTag</td><td>Identifies the blockchain network the transaction is targeting.</td></tr><tr><td>BlockRef</td><td>string</td><td>blockRef</td><td>Reference to a specific block to maintain ordering and prevent replay attacks.</td></tr><tr><td>Expiration</td><td>uint32</td><td>expiration</td><td>Number of blocks until the transaction expires.</td></tr><tr><td>Clauses</td><td>[]*JSONClause</td><td>clauses</td><td>Array of operation clauses (each clause represents a contract call or transfer).</td></tr><tr><td>GasPriceCoef</td><td>uint8</td><td>gasPriceCoef</td><td>Multiplier adjusting the base gas price, affecting transaction priority.</td></tr><tr><td>Gas</td><td>uint64</td><td>gas</td><td>Maximum amount of gas allocated for execution.</td></tr><tr><td>Origin</td><td>thor.Address</td><td>origin</td><td>Address initiating the transaction.</td></tr><tr><td>Delegator</td><td>*thor.Address</td><td>delegator</td><td>(Optional) If present, indicates a delegator executing on behalf of origin.</td></tr><tr><td>Nonce</td><td>math.HexOrDecimal64</td><td>nonce</td><td>A unique number preventing transaction replay attacks.</td></tr><tr><td>DependsOn</td><td>*thor.Bytes32</td><td>dependsOn</td><td>(Optional) Specifies a dependency on another transaction’s hash.</td></tr></tbody></table>

2. **RPC Compatibility and the SDK RPC Proxy:**  &#x20;

The SDK RPC Proxy offers _partial_ Ethereum JSON-RPC compatibility. _Not all methods are supported_, and some have different behaviors or limitations. Consult the official VeChainThor documentation for the updated list of supported methods (see Section [RPC Methods](rpc-methods-detailed-breakdown.md)).

3. &#x20;**Gas Calculation and VTHO:**&#x20;

Gas costs are paid in VTHO, not VET. Developers need to ensure their accounts have sufficient VTHO. Use VeChainThor-specific APIs to estimate VTHO costs. A feeDelegation service can be used to overcome the need, and the specific provider configuration is supported in the [VeChain SDK](https://github.com/vechain/vechain-sdk-js).

4. **Smart Contract Compilation:**&#x20;

VeChainThor supports Solidity up to the Paris EVM version.

---
description: Transactions related functions.
---

# Transactions

The VeChain SDK provides comprehensive support for handling transactions. Developers can initialize a transaction by assembling the transaction body, adding clauses, and finally signing and sending the transaction. 

> ⚠️ **Warning:**
> All the examples listed below refer to low level transaction building. The VeChain SDK provides built-in methods to sign and send transactions. Please refer to the contracts section for more information.


To break it down:

1. **Initializing a Transaction**: Developers can create a transaction by specifying the necessary details in the transaction body. This includes setting the chain tag, block reference, expiration, gas price coefficient, gas limit, and other relevant transaction parameters.
2. **Adding Clauses**: Clauses are the individual actions that the transaction will perform on the VeChainThor blockchain. Each clause contains information such as the recipient's address, the amount of VET to be transferred, and additional data, if required.
3. **Signing the Transaction**: After assembling the transaction body with the appropriate clauses, developers can sign the transaction using their private key. Signing the transaction ensures its authenticity and prevents tampering during transmission.

## Example: Signing and Decoding
In this example a simple transaction with a single clause is created, signed, encoded and then decoded

```typescript { name=sign-decode, category=example }
// 1 - Create the transaction clauses
const transaction = {
    clauses: [
        Clause.transferVET(
            Address.of('0xb717b660cd51109334bd10b2c168986055f58c1a'),
            VET.of(1)
        ) as TransactionClause
    ],
    simulateTransactionOptions: {
        caller: senderAccount.address
    }
};

// 2 - Estimate gas
const gasResult = await thorSoloClient.gas.estimateGas(
    transaction.clauses,
    transaction.simulateTransactionOptions.caller
);

// 3 - Build transaction body
const txBody = await thorSoloClient.transactions.buildTransactionBody(
    transaction.clauses,
    gasResult.totalGas
);

// 4 - Sign the transaction
const signer = await provider.getSigner(senderAccount.address);

const rawSignedTransaction = await signer.signTransaction(
    signerUtils.transactionBodyToTransactionRequestInput(
        txBody,
        senderAccount.address
    )
);

const signedTransaction = Transaction.decode(
    HexUInt.of(rawSignedTransaction.slice(2)).bytes,
    true
);

// 5 - Send the transaction
const sendTransactionResult =
    await thorSoloClient.transactions.sendTransaction(signedTransaction);
```

## Example: Multiple Clauses
On the VeChainThor blockchain a transaction can be composed of multiple clauses. \
Clauses are a feature of the VeChainThor blockchain that increase the scalability of the blockchain by enabling the sending of multiple payloads to different recipients within a single transaction.

```typescript { name=multiple-clauses, category=example }
// 1 - Define multiple clauses

const clauses: TransactionClause[] = [
    Clause.transferVET(
        Address.of('0x7567d83b7b8d80addcb281a71d54fc7b3364ffed'),
        VET.of(10000)
    ) as TransactionClause,
    Clause.transferToken(
        Address.of(VTHO_ADDRESS),
        Address.of('0x7567d83b7b8d80addcb281a71d54fc7b3364ffed'),
        VTHO.of(10000)
    ) as TransactionClause
];

// 2 - Calculate intrinsic gas of both clauses

const gas = Number(Transaction.intrinsicGas(clauses).wei);

// 3 - Body of transaction

const body: TransactionBody = {
    chainTag: networkInfo.mainnet.chainTag,
    blockRef: '0x0000000000000000',
    expiration: 32,
    clauses,
    gasPriceCoef: 0,
    gas,
    dependsOn: null,
    nonce: 12345678
};

// Create private key
const privateKey = await Secp256k1.generatePrivateKey();

// 4 - Sign transaction

const signedTransaction = Transaction.of(body).sign(privateKey);

// 5 - Encode transaction

const encodedRaw = signedTransaction.encoded;

// 6 - Decode transaction

const decodedTx = Transaction.decode(encodedRaw, true);
```

## Example: Fee Delegation
Fee delegation is a feature on the VeChainThor blockchain which enables the transaction sender to request another entity, a sponsor, to pay for the transaction fee on the sender's behalf.

```typescript { name=fee-delegation, category=example }
// Sender account with private key
const senderAccount = {
    privateKey:
        'f9fc826b63a35413541d92d2bfb6661128cd5075fcdca583446d20c59994ba26',
    address: '0x7a28e7361fd10f4f058f9fefc77544349ecff5d6'
};

// 1 - Create thor client for solo network
const thorSoloClient = ThorClient.fromUrl(THOR_SOLO_URL, {
    isPollingEnabled: false
});

// 2 - Define clause and estimate gas

const clauses: TransactionClause[] = [
    Clause.transferVET(
        Address.of('0x7567d83b7b8d80addcb281a71d54fc7b3364ffed'),
        VET.of(10000)
    ) as TransactionClause
];

// Get gas estimate
const gasResult = await thorSoloClient.gas.estimateGas(
    clauses,
    senderAccount.address
);

// 3 - Define transaction body

const body: TransactionBody = {
    chainTag: networkInfo.mainnet.chainTag,
    blockRef: '0x0000000000000000',
    expiration: 0,
    clauses,
    gasPriceCoef: 0,
    gas: gasResult.totalGas,
    dependsOn: null,
    nonce: 1,
    reserved: {
        features: 1 // set the transaction to be delegated
    }
};

// 4 - Create private keys of sender and delegate

const nodeDelegate = HDKey.fromMnemonic(Mnemonic.of());
const delegatorPrivateKey = nodeDelegate.privateKey;

// 5 - Get address of delegate

const delegatorAddress = Address.ofPublicKey(nodeDelegate.publicKey).toString();

// 6 - Sign transaction as sender and delegate

const signedTransaction = Transaction.of(body).signWithDelegator(
    HexUInt.of(senderAccount.privateKey).bytes,
    HexUInt.of(delegatorPrivateKey).bytes
);

// 7 - Encode transaction

const encodedRaw = signedTransaction.encoded;

// 8 - Decode transaction and check

const decodedTx = Transaction.decode(encodedRaw, true);
```

## Example: BlockRef and Expiration
Using the _BlockRef_ and _Expiration_ fields a transaction can be set to be processed or expired by a particular block. _BlockRef_ should match the first eight bytes of the ID of the block. The sum of _BlockRef_ and _Expiration_ defines the height of the last block that the transaction can be included.

```typescript { name=blockref-expiration, category=example }
// 1 - Define clauses

const clauses: TransactionClause[] = [
    Clause.transferVET(
        Address.of('0x7567d83b7b8d80addcb281a71d54fc7b3364ffed'),
        VET.of(1000)
    ) as TransactionClause
];

// 2 - Define transaction body

const body: TransactionBody = {
    chainTag: networkInfo.mainnet.chainTag,
    blockRef: '0x00ffecb8ac3142c4', // first 8 bytes of block id from block #16772280
    expiration: 32, // tx will expire after block #16772280 + 32
    clauses,
    gasPriceCoef: 0,
    gas: HexUInt.of(Transaction.intrinsicGas(clauses).wei).toString(), // use thor.gas.estimateGas() for better estimation
    dependsOn: null,
    nonce: 1
};

// 3 - Create private key

const privateKey = await Secp256k1.generatePrivateKey();

// 4 - Sign transaction

const signedTransaction = Transaction.of(body).sign(privateKey);

// 5 - Encode transaction

const encodedRaw = signedTransaction.encoded;

// 6 - Decode transaction and check

const decodedTx = Transaction.decode(encodedRaw, true);
```

## Example: Transaction Dependency
A transaction can be set to only be processed after another transaction, therefore defining an execution order for transactions. The _DependsOn_ field is the Id of the transaction on which the current transaction depends on. If the transaction does not depend on others _DependsOn_ can be set to _null_

```typescript { name=tx-dependency, category=example }
// 1 - Define transaction clauses

const txAClauses: TransactionClause[] = [
    Clause.transferVET(
        Address.of('0x7567d83b7b8d80addcb281a71d54fc7b3364ffed'),
        VET.of(1000)
    ) as TransactionClause
];
const txBClauses: TransactionClause[] = [
    Clause.transferVET(
        Address.of('0x7ccadeea14dd6727845b58f8aa7aad0f41a002a2'),
        VET.of(1)
    )
];

// 2 - Define transaction A with no dependencies

// @NOTE: This transaction has nonce = 1
const txABody: TransactionBody = {
    chainTag: networkInfo.mainnet.chainTag,
    blockRef: '0x0000000000000000',
    expiration: 0,
    clauses: txAClauses,
    gasPriceCoef: 0,
    gas: HexUInt.of(Transaction.intrinsicGas(txAClauses).wei).toString(), // use thor.gas.estimateGas() for better estimation
    dependsOn: null,
    nonce: 1
};

// 3 - Define transaction B with nonce = 2

// @NOTE: at the moment dependsOn is null
const txBBody: TransactionBody = {
    chainTag: networkInfo.mainnet.chainTag,
    blockRef: '0x0000000000000000',
    expiration: 0,
    clauses: txBClauses,
    gasPriceCoef: 0,
    gas: HexUInt.of(Transaction.intrinsicGas(txBClauses).wei).toString(), // use thor.gas.estimateGas() for better estimation
    dependsOn: null,
    nonce: 2
};

// Define the senders private key
const senderPrivateKey = await Secp256k1.generatePrivateKey();

// To define transaction B as dependent on transaction
// it's necessary to sign transaction A, and then get its Id
// and set that Id into transaction B's dependsOn field

// 4 - Get Tx A id

const txASigned = Transaction.of(txABody).sign(senderPrivateKey);

// 5 - Set it inside tx B

txBBody.dependsOn = txASigned.id.toString();

// 6 - Sign Tx B

const txBSigned = Transaction.of(txBBody).sign(senderPrivateKey);

// 7 - encode Tx B

const rawTxB = txBSigned.encoded;

// Check (we can decode Tx B)
const decodedTx = Transaction.decode(rawTxB, true);
```

## Example: Transaction Simulation
Simulation can be used to check if a transaction will fail before sending it. It can also be used to determine the gas cost of the transaction.
Additional fields are needed in the transaction object for the simulation and these conform to the _SimulateTransactionOptions_ interface.
Note - the result of a transaction might be different depending on the state(block) you are executing against.

```typescript { name=simulation, category=example }
// In this example we simulate a transaction of sending 1 VET to another account

// 1 - Create thor client for solo network
const thorSoloClient = ThorClient.fromUrl(THOR_SOLO_URL);

// 2 - create the transaction for a VET transfer
const transaction1 = {
    clauses: [
        Clause.transferVET(
            Address.of('0xb717b660cd51109334bd10b2c168986055f58c1a'),
            VET.of(1)
        ) as TransactionClause
    ],
    // Please note - this field one of the optional fields that may be passed (see SimulateTransactionOptions),
    // and is only required if you want to simulate a transaction
    simulateTransactionOptions: {
        caller: '0x7a28e7361fd10f4f058f9fefc77544349ecff5d6'
    }
};

// 3 - Simulate the transaction
const simulatedTx1 = await thorSoloClient.transactions.simulateTransaction(
    transaction1.clauses,
    {
        ...transaction1.simulateTransactionOptions
    }
);

```

2. **Delegation with Private Key**: Here, we'll extend the previous example by incorporating fee delegation. The transaction sender will delegate the transaction fee payment to another entity (delegator), and we'll guide you through the steps of building, signing, and sending such a transaction.

```typescript { name=full-flow-delegator-private-key, category=example }
import { expect } from 'expect';

// START_SNIPPET: FullFlowDelegatorPrivateKeySnippet

// 1 - Create the thor client
const thorSoloClient = ThorClient.fromUrl(THOR_SOLO_URL, {
    isPollingEnabled: false
});

// Sender account with private key
const senderAccount: { privateKey: string; address: string } = {
    privateKey:
        'f9fc826b63a35413541d92d2bfb6661128cd5075fcdca583446d20c59994ba26',
    address: '0x7a28e7361fd10f4f058f9fefc77544349ecff5d6'
};

// Delegator account with private key
const delegatorAccount: { privateKey: string; address: string } = {
    privateKey:
        '521b7793c6eb27d137b617627c6b85d57c0aa303380e9ca4e30a30302fbc6676',
    address: '0x062F167A905C1484DE7e75B88EDC7439f82117DE'
};

// Create the provider (used in this case to sign the transaction with getSigner() method)
const providerWithDelegationEnabled = new VeChainProvider(
    // Thor client used by the provider
    thorSoloClient,

    // Internal wallet used by the provider (needed to call the getSigner() method)
    new ProviderInternalBaseWallet(
        [
            {
                privateKey: HexUInt.of(senderAccount.privateKey).bytes,
                address: senderAccount.address
            }
        ],
        {
            delegator: {
                delegatorPrivateKey: delegatorAccount.privateKey
            }
        }
    ),

    // Enable fee delegation
    true
);

// 2 - Create the transaction clauses
const transaction = {
    clauses: [
        Clause.transferVET(
            Address.of('0xb717b660cd51109334bd10b2c168986055f58c1a'),
            VET.of(1)
        ) as TransactionClause
    ],
    simulateTransactionOptions: {
        caller: senderAccount.address
    }
};

// 3 - Estimate gas
const gasResult = await thorSoloClient.gas.estimateGas(
    transaction.clauses,
    transaction.simulateTransactionOptions.caller
);

// 4 - Build transaction body
const txBody = await thorSoloClient.transactions.buildTransactionBody(
    transaction.clauses,
    gasResult.totalGas,
    {
        isDelegated: true
    }
);

// 4 - Sign the transaction
const signer = await providerWithDelegationEnabled.getSigner(
    senderAccount.address
);

const rawDelegateSigned = await signer.signTransaction(
    signerUtils.transactionBodyToTransactionRequestInput(
        txBody,
        senderAccount.address
    )
);

const delegatedSigned = Transaction.decode(
    HexUInt.of(rawDelegateSigned.slice(2)).bytes,
    true
);

// 5 - Send the transaction
const sendTransactionResult =
    await thorSoloClient.transactions.sendTransaction(delegatedSigned);

// 6 - Wait for transaction receipt
const txReceipt = await thorSoloClient.transactions.waitForTransaction(
    sendTransactionResult.id
);
```

3. **Delegation with URL**: This example will showcase the use of a delegation URL for fee delegation. The sender will specify a delegation URL in the `signTransaction` options, allowing a designated sponsor to pay the transaction fee. We'll cover the full process, from building clauses to verifying the transaction on-chain.

```typescript { name=full-flow-delegator-url, category=example }
import { expect } from 'expect';

// START_SNIPPET: FullFlowDelegatorUrlSnippet

// 1 - Create the thor client
const thorClient = ThorClient.fromUrl(TESTNET_URL, {
    isPollingEnabled: false
});

// Sender account with private key
const senderAccount: {
    mnemonic: string;
    privateKey: string;
    address: string;
} = {
    mnemonic:
        'fat draw position use tenant force south job notice soul time fruit',
    privateKey:
        '2153c1e49c14d92e8b558750e4ec3dc9b5a6ac4c13d24a71e0fa4f90f4a384b5',
    address: '0x571E3E1fBE342891778151f037967E107fb89bd0'
};

// Delegator account with private key
const delegatorAccount = {
    URL: 'https://sponsor-testnet.vechain.energy/by/269'
};

// Create the provider (used in this case to sign the transaction with getSigner() method)
const providerWithDelegationEnabled = new VeChainProvider(
    // Thor client used by the provider
    thorClient,

    // Internal wallet used by the provider (needed to call the getSigner() method)
    new ProviderInternalBaseWallet(
        [
            {
                privateKey: HexUInt.of(senderAccount.privateKey).bytes,
                address: senderAccount.address
            }
        ],
        {
            delegator: {
                delegatorUrl: delegatorAccount.URL
            }
        }
    ),

    // Enable fee delegation
    true
);

// 2 - Create the transaction clauses
const transaction = {
    clauses: [
        Clause.transferVET(
            Address.of('0xb717b660cd51109334bd10b2c168986055f58c1a'),
            VET.of(1)
        ) as TransactionClause
    ],
    simulateTransactionOptions: {
        caller: senderAccount.address
    }
};

// 3 - Estimate gas
const gasResult = await thorClient.gas.estimateGas(
    transaction.clauses,
    senderAccount.address
);

// 4 - Build transaction body
const txBody = await thorClient.transactions.buildTransactionBody(
    transaction.clauses,
    gasResult.totalGas,
    {
        isDelegated: true
    }
);

// 4 - Sign the transaction
const signer = await providerWithDelegationEnabled.getSigner(
    senderAccount.address
);

const rawDelegateSigned = await signer.signTransaction(
    signerUtils.transactionBodyToTransactionRequestInput(
        txBody,
        senderAccount.address
    )
);

const delegatedSigned = Transaction.decode(
    HexUInt.of(rawDelegateSigned.slice(2)).bytes,
    true
);

// 5 - Send the transaction
const sendTransactionResult =
    await thorClient.transactions.sendTransaction(delegatedSigned);

// 6 - Wait for transaction receipt
const txReceipt = await thorClient.transactions.waitForTransaction(
    sendTransactionResult.id
);
```

By examining these complete examples, developers can gain a comprehensive understanding of transaction handling in the VeChain SDK. Each example demonstrates the steps involved in initiating, signing, and sending transactions, as well as the nuances associated with fee delegation.

# Errors handling on transactions
You can find the transaction revert reason by using `getRevertReason` method with the transaction hash.

```typescript { name=revert-reason, category=example }
// Define transaction id's
const transactionHash =
    '0x0a5177fb83346bb6ff7ca8408889f0c99f44b2b1b5c8bf6f0eb53c4b2e81d98d';

// Get the revert reason
const revertReason =
    await thorClient.transactions.getRevertReason(transactionHash);
console.log(revertReason);
```

This method will return the revert reason of the transaction if it failed, otherwise it will return `null`.

### Decoding revert reason when simulating a transaction
Even when using the `simulateTransaction` method you can find the revert reason.

```typescript { name=revert-reason-with-simulation, category=example }
const simulatedTx: TransactionSimulationResult[] =
    await thorSoloClient.transactions.simulateTransaction([
        {
            to: '0x0000000000000000000000000000456e65726779',
            value: '0',
            data: ABIContract.ofAbi(energyABI)
                .encodeFunctionInput('transfer', [
                    '0x9e7911de289c3c856ce7f421034f66b6cde49c39',
                    Units.parseEther('1000000000').bi
                ])
                .toString()
        }
    ]);

const revertReason = thorSoloClient.transactions.decodeRevertReason(
    simulatedTx[0].data
);
```

In this case there is only a `TransactionSimulationResult`, so no need to loop.

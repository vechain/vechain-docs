# Buy me a Coffee

## Buy me a Coffee with dApp-Kit

The outcome of this tutorial is a React application capable of identifying a user's wallet, sending tokens, and verifying the transaction on the VeChain network.

You can open the resulting project on [GitHub](https://github.com/ifavo/example-buy-me-a-coffee) to check on all steps in parallel while reading each section:

Here is the sequence we are building during this Tutorial:

{% @mermaid/diagram content="sequenceDiagram
participant User
participant Wallet
participant App
participant Blockchain
participant GitHub

note over User, GitHub: Starting the App
User->>App: open app
App->>GitHub: get list of tokens
GitHub-->>App: list of tokens
App-->>User: show tokens and form to enter amount

note over User, App: User Login
User->>App: log in
App->>Wallet: ask for user verification
Wallet->>User: verify identity
User-->>Wallet: approve verification
Wallet-->>App: verification approved
App-->>User: show user's wallet address

note over User, Blockchain: Token Transfer
User->>App: initiate token transfer
App->>Wallet: request transaction signature
Wallet->>User: request signature
User-->>Wallet: provide signature
Wallet-->>Blockchain: send transaction
Blockchain-->>Wallet: transaction ID or error message
Wallet-->>User: show confirmation
Wallet-->>App: send transaction ID or error message

loop until transaction is confirmed
  App->>Blockchain: check transaction status
  Blockchain-->>App: pending, successful, or failed
end

App-->>User: show transaction result" %}

## Preparation

This tutorial is based on a pre-existing React project that has already been configured with widely-used libraries. It will focus on incorporating VeChain-specific modules into this project. Therefore, only information related to VeChain will be covered in this article. It assumes a basic understanding of React, such as managing states and passing props, which will not be explained.

* **@vechain/dapp-kit-react** - A collection of React hooks and components designed to facilitate the integration of the dApp kit into React applications.
* **@vechain/dapp-kit-ui** - A set of UI components aimed at simplifying the process of wallet selection and connection.
* **@vechain/sdk-core** - A library focused on providing features specific to VeChain.
* **@vechain/sdk-network** - A library created to streamline communication with VeChain nodes.

Install all these modules with npm:

```shell
npm install --save @vechain/dapp-kit-react @vechain/dapp-kit-ui @vechain/sdk-core @vechain/sdk-network
```

### Integrating the dApp-Kit

{% hint style="info" %}
You can read more about the dApp-Kit in their [docs section](https://docs.vechain.org/developer-resources/sdks-and-providers/dapp-kit/dapp-kit-1).
{% endhint %}

To connect your application to VeChain you will wrap it into a provider that will share a single connection and user authentification globally.

In our example app, this is done within the [`App.tsx`](https://github.com/ifavo/example-buy-me-a-coffee/blob/main/src/App.tsx).

Import the Provider:

```tsx
import { DAppKitProvider } from "@vechain/dapp-kit-react";
```

And wrap your content with it:

```tsx
    <DAppKitProvider
        // the network & node to connect to
        nodeUrl="https://testnet.vechain.org
        genesis="test"

        // remember last connected address on page reload
        usePersistence={true}
    >
        {children}
    </DAppKitProvider>
```

Consequently, you will have the capability to utilize functions such as `useWallet()` for user identification or `useConnex()` for interacting with VeChain.

### Integrating `useQuery`

By using [`@tanstack/react-query`](https://tanstack.com/query/latest), we will access VeChain nodes directly to retrieve some data from the public infrastructure. Just like with dApp-Kit, you need a provider that enables shared fetch and cache management.

Import the Provider and establish a default client configuration:

```tsx
import { QueryClient, QueryClientProvider } from "@tanstack/react-query";
const queryClient = new QueryClient();
```

And wrap your dApp-Kit Provider with it:

```tsx
<QueryClientProvider client={queryClient}>
  <DAppKitProvider>..</DAppKitProvider>
</QueryClientProvider>
```

### Authentification

The entire authentication procedure is contained within a React component offered by the dApp-Kit.

The [`WalletButton`](https://docs.vechain.org/developer-resources/sdks-and-providers/dapp-kit/dapp-kit-1/react/usage#walletbutton) generates a button that prompts for connection or displays the address of the signed-in user.

By using this feature, our streamlined Menu will present either a connect button or the user's address within this one component.

```tsx
import { WalletButton } from "@vechain/dapp-kit-react";

export default function LayoutMenu() {
  return <WalletButton />;
}
```

By utilizing the [`useWallet()`](https://docs.vechain.org/developer-resources/sdks-and-providers/dapp-kit/dapp-kit-1/react/usage#usewallet) hook, we can already make use of the dApp-Kit's functionality to display a hint for signing in within our primary component.

```tsx
import { useWallet } from "@vechain/dapp-kit-react";
export default function BuyCoffee() {
  // get the connected wallet
  const { account } = useWallet();

  // if there is no wallet connected, ask the user to connect first
  if (!account) {
    return "Please connect your wallet to continue.";
  }

  return "Placeholder";
}
```

### Select Token from Registry

VeChain curates a public repository of tokens on [GitHub](https://github.com/vechain/token-registry) to streamline token interaction within decentralized applications (dApps).

{% hint style="info" %}
Have you published a new Token on VeChain? You are welcome to create a pull request to add it to the public registry!
{% endhint %}

We will utilize it to dynamically retrieve all recognized tokens within the application and enable the user to purchase a coffee using a token of their choosing.

To obtain the list, we will employ the `useQuery()` function:

```tsx
// fetch the token registry, to display a list of tokens
const tokenRegistry = useQuery({
  queryKey: ["tokenRegistry"],
  queryFn: async () =>
    fetch(`https://vechain.github.io/token-registry/main.json`).then((res) =>
      res.json()
    ),
});
```

The code snippet retrieves the list and returns its content. `useQuery()` offers useful functionalities such as a loading indicator, error handling, and automated retry attempts.

A loading indicator will be displayed during the loading process:

```tsx
if (tokenRegistry.isLoading) {
  return <IconLoading />;
}
```

In order to show the data, it can be presented in a dropdown menu:

```tsx
<>
  <label htmlFor="token" className="sr-only">
    Token
  </label>
  <select name="token" id="token">
    <option value="">VET</option>
    {tokenRegistry.data?.map((token) => (
      <option key={token.address} value={token.address}>
        {token.symbol}
      </option>
    ))}
  </select>
</>
```

We will display `VET` as a blank choice for utilizing VeChain's native token as a payment option if no token has been chosen. The complete component, along with its state management, can be found in the [`src/BuyCoffee/SelectToken.tsx` file on GitHub](https://github.com/ifavo/example-buy-me-a-coffee/blob/main/src/BuyCoffee/SelectToken.tsx).

### Read Token Balance

To assist users in determining the amount to send, we will retrieve the VET or Token balance of the currently signed-in user.

Utilizing `useConnex()` and `useWallet()`, we will request the account details and present the outcome in a user-friendly manner using `unitsUtil`, a utility function from the VeChain SDK:

```js
// import hooks
import { useConnex, useWallet } from '@vechain/dapp-kit-react';
// ..

// get currently signed in account and the currenct vechain connection
const { account } = useWallet()
const connex = useConnex()
```

Read VET Balance by requesting account details:

```js
connex.thor.account(account).get()
    .then(({ balance }) => {
        console.log('VET Balance:', balance)
    })
```

For tokens, we will execute a function on the contract by defining an interface that remains consistent across all tokens.

```js
connex.thor.account(token.address)
    .method(
        {
            "inputs": [{ "name": "owner", "type": "address" }],
            "name": "balanceOf",
            "outputs": [{ "name": "balance", "type": "uint256" }]
        })
    .call(account)
    .then(({ decoded: { balance } }) => {
        console.log('Token Balance', balance)
    })
```

Further details on the [Account Visitor can be found in various sections of the documentation](https://docs.vechain.org/developer-resources/sdks-and-providers/connex/api-specification#account-visitor).

The output of both functions is a BigNumber representation of the value, either in hexadecimal or as a 256-byte integer value that may be challenging for a user to interpret. The `@vechain/sdk-core` library provides `unitsUtils` to convert the balance into a readable format:

* `unitsUtils.formatVET(balance)` transforms the balance into a complete VET number by dividing it by 18 decimal places.
* `unitsUtils.formatUnits(balance, token.decimals)` converts the balance into a complete number with a specified custom decimal value from the token registry.

For the full implementation of this functionality, refer to [`src/BuyCoffee/Balance.tsx`](https://github.com/ifavo/example-buy-me-a-coffee/blob/main/src/BuyCoffee/Balance.tsx) in the GitHub demonstration project.

### Prepare Token Sending

The [`@vechain/sdk-core`](https://www.npmjs.com/package/@vechain/sdk-core) library offers tools to easily create blockchain commands.

A "clause" is a single command, similar to a function call, that's included in a transaction. The `clauseBuilder` helps create these commands in a more straightforward way. Additionally, `unitsUtils` helps adjust user inputs to the correct format for the blockchain:

* `unitsUtils.parseVET(amount)` – Since VET tokens are divided into 18 decimal places, this function adjusts the input number to include these decimals, converting it into a format the blockchain can understand.
* `clauseBuilder.transferVET(recipient, parsedVET)` – This command creates instructions to send VET tokens to another wallet.
* `unitsUtils.parseUnits(amount, decimals)` – For tokens with a different number of decimal places, this function allows specifying the exact number of decimals to correctly format the amount.
* `clauseBuilder.transferToken(token, recipient, parsedAmount)` – This command generates instructions to send a specified amount of a particular token to another wallet.

{% hint style="info" %}
To explore more about the clauseBuilder and its additional functionalities, check out the [tsdocs](https://tsdocs.dev/docs/@vechain/sdk-core/1.0.0-beta.3/variables/core.clauseBuilder.html).
{% endhint %}

For our Buy me a Coffee with any token app this will translate into this snippet:

```tsx
const clauses = [
  // if a token was selected, transfer the token
  selectedToken
    ? // the clauseBuilder helps build the data for the transaction
      clauseBuilder.transferToken(
        selectedToken.address,
        RECIPIENT_ADDRESS,
        unitsUtils.parseUnits(amount, selectedToken.decimals)
      )
    : // or use the clauseBuilder to transfer VET by default
      clauseBuilder.transferVET(RECIPIENT_ADDRESS, unitsUtils.parseVET(amount)),
];
```

A valuable feature of VeChain Wallets is their ability to include comments, which explain individual clauses or entire transactions to the user.

By adding a `comment` attribute to the clause object, Wallets will display it alongside each clause for the user.

### Sending Tokens

Function calls on the Blockchain are executed by sending a transaction, which incurs a VTHO charge for each action based on the associated workload. To verify its identity, a transaction must be signed with the sender's private key.

After setting up the `DAppKitProvider`, we can use the `useConnex()` hook to connect to VeChain.

To have the user sign and send a transaction, we use `await connex.vendor.sign('tx', clauses).request()`.

Here's what happens during this process:

1. `sign('tx', clauses)` creates a transaction object with the specified clauses, using the blockchain settings from `DAppKitProvider`.
2. `request()` asks the user's wallet to get the user's signature for the transaction. This function is async, because it will wait until the wallet interaction is completed.
3. The wallet shows the transaction details to the user. If the user agrees and signs it, the transaction is forwarded to a VeChain node.
4. The VeChain node confirms the transaction by returning a transaction ID. This ID can be used to track the transaction's status.

### Track Transaction Status

By utilizing the transaction ID, progress can be monitored through a request for a receipt.

By using the `useQuery()` function, an updated receipt will be retrieved at regular intervals. Given that new blocks are included into VeChain approximately every 10 seconds, a transaction is typically included after that time.

Utilizing a public node as a direct method offers an alternative way of connecting to VeChain. Each node offers a public JSON API, which allows for retrieving raw data.

```tsx
import type { TransactionReceipt } from '@vechain/sdk-network';

// ..

const receipt = useQuery<TransactionReceipt | null>({
    queryKey: ['transaction', txId],
    queryFn: async () => fetch(`${NODE_URL}/transactions/${txId}/receipt`).then((res) => res.json()) as Promise<TransactionReceipt | null>,
    refetchInterval: 7000,
    placeholderData: (previousData) => previousData,
    enabled: Boolean(txId) && !hasReceipt
})
```

The [`Transaction Receipt`](https://tsdocs.dev/docs/@vechain/sdk-network/1.0.0-beta.3/interfaces/network.TransactionReceipt.html) provides details regarding the fundamental transaction information along with its outcomes. When checking the success of the transaction, we will specifically examine the `reverted` indicator in the receipt.

Initially, before the transaction is confirmed, the receipt will be absent, resulting in three possible states:

1. When no receipt is available, the status is `pending`.
2. If the receipt is present and the `reverted` flag is marked as `true`, the status is `reverted`.
3. In case the receipt exists and the `reverted` flag is set to `false`, the status is `success`.

```tsx
const status = !receipt.data ? 'pending' : receipt.data?.reverted ? 'reverted' : 'success'
```

A React component displaying status for the user can be found in the sample project at [`src/BuyCoffee/Transaction.tsx`](https://github.com/ifavo/example-buy-me-a-coffee/blob/main/src/BuyCoffee/Transaction.tsx).

## Proof of Concept Completed

The preceding sections have shown a rudimentary application that communicates with VeChain:

* It outlined the process of establishing VeChain Connectivity within a React Application.
* Demonstrated how to identify a user's wallet address.
* Utilized the public token registry to show a list VeChain Tokens.
* Interact with the Blockchain to read an accounts balance or call a contract function and read its reply.
* Creating transactions to send VET or other ecosystem tokens.
* Monitored the status of a transaction to confirm its completion.

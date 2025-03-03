# Key Architectural Differences and Optimizations

VeChainThor introduces several key features that differentiate it from Ethereum:

1. **Two-Token System (VET & VTHO):**

* **VET (VeChain Token):** The primary reserve of value token. VET has a maximum fixed supply of around 86 billion tokens which have already been minted. No more VET will be created.
* **VTHO (VeChainThor Energy):** Functions as a “gas token,” is an ERC20 native currency used to pay for the cost of computation (gas) on the blockchain. Transactions consume VTHO, a portion of which gets burned. VET holders generate VTHO over time (at a rate of 0.000432 VTHO per VET per day).
* **Benefit:** Decouples transaction costs (VTHO) from the price volatility of the main asset (VET), leading to more predictable and stable transaction fees for businesses.
* **Implication:** Developers must manage both VET and VTHO.

2. &#x20;**Multi-Clause Transactions (MCT) and Multi-Task Transactions (MTT):**

* **Ethereum:** Typically, one transaction performs one action.
* **VeChainThor (MCT):** Allows multiple _clauses_ within a single transaction, each performing a separate action (e.g., transferring tokens to different recipients, calling different contract functions).
* **VeChainThor (MTT):** An extension of MCT. With MTT, users can batch multiple clauses that involve transfers to various recipients and call functions of different contracts, all packed in one transaction and executed atomically.
* **Benefit:** Dramatically improves efficiency and reduces transaction overhead for complex operations, particularly beneficial for supply chain applications.
* **Implication:** Developers can design more efficient workflows but need to deal with a different transaction structure also when the clause is 1. The transaction envelope is different.

3. **API-Based Architecture (RESTful API vs. JSON-RPC):**

* **Ethereum:** Primarily relies on JSON-RPC for blockchain interaction.
* **VeChainThor:** Emphasizes a RESTful API, a more common standard in enterprise systems.
* **Benefit:** Easier integration with existing enterprise infrastructure and backend systems. RESTful APIs are generally considered more developer-friendly.
* **Implication:** While an SDK RPC Proxy provides _partial_ support for Ethereum's JSON-RPC methods, developers should prioritize the RESTful API for best performance and integration. Not all JSON-RPC methods are supported, and some have limitations.

4. **Transaction Dependency:**

* &#x20;**VeChainThor:** Allows developers to specify that one transaction depends on the successful execution of another.
* &#x20;**Benefit:** Ensures ordered execution of transactions, crucial for complex workflows where the sequence of operations matters.
* **Implication:** Developers can build more reliable and predictable applications by defining transaction dependencies.

5. **Transaction Expiration:**

* **VeChainThor:** Transactions can be given an expiration time. If not included in a block within that timeframe, they expire.
* **Benefit:** Prevents stale transactions from clogging the network and provides more control over transaction validity.
* I**mplication:** Developers can force a more efficient transaction flow, and can be set to null when it’s not required. But the transaction envelope is different.

6. **Hashing Algorithm:**

* **VeChain:** Uses blake2b for hashing.
* **Ethereum:** Uses keccak-256.

7. **Nonce Handling:**

* **VeChain:**  Can be set to random. Ensuring transaction uniqueness is determined by content rather than nonce.
* **Ethereum:** Uses an incrementing nonce, requiring strict tracking of transaction history.


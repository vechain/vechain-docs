# Interact with dApps

When you are going to interact with a dApp, Once the dApp sends the signing request to sync, it will automatically pop up a signing window and request you to sign the transaction/content. when the signing details are popped-up, it will show clauses/contents which you need to sign.

Note

* All the signed transaction/certificate are stored in local, therefore, it only shows the transaction/content which is the same computer as you signed the transaction.
* Before signing a transaction or a certificate, you need to create or import a wallet first.

## Signing a Transaction <a href="#signing-a-transaction" id="signing-a-transaction"></a>

On the left side, it shows the transaction summary; number of clauses; the description of each clause. On the right side, you can select which wallet is going to sign the transaction and also transaction priority

#### Local Wallets <a href="#local-wallets" id="local-wallets"></a>

1. Review the content
2. Choose the Wallet type `Local`
3. Choose a wallet to sign the transaction
4. Modify the priority if needed
5. Input wallet's password
6. Click **SIGN**

#### Ledger <a href="#ledger" id="ledger"></a>

1. Review the content
2. Choose the Wallet type `Device Name`
3. Choose a wallet to sign the transaction
4. Modify the priority if needed
5. Connect your device and follow the steps
6. Confirm the transaction on your device

### Signing a Certificate <a href="#signing-a-certificate" id="signing-a-certificate"></a>

The certificate is a message signing based mechanism which can easily provide your identification or you to agree to your terms or agreements to the dApp.

#### Local Wallets <a href="#local-wallets-2" id="local-wallets-2"></a>

1. Check the type of certificate ( <img src="../../../../.gitbook/assets/download (8) (1).png" alt="" data-size="line"> / <img src="../../../../.gitbook/assets/download (9) (1).png" alt="" data-size="line"> )
2. Review the content
3. Choose the Wallet type `Local`
4. Choose a wallet to sign the certificate
5. Input wallet's password
6. Click **SIGN**

#### Ledger <a href="#ledger-2" id="ledger-2"></a>

1. Check the type of certificate( <img src="../../../../.gitbook/assets/download (8) (1).png" alt="" data-size="line"> / <img src="../../../../.gitbook/assets/download (9) (1).png" alt="" data-size="line"> )
2. Review the content
3. Choose the Wallet type `LedgerName`
4. Choose a wallet to sign the certificate
5. Connect your device and follow the steps
6. Confirm the transaction on your device

### Keep Local Wallet Unlocked <a href="#keep-local-wallet-unlocked" id="keep-local-wallet-unlocked"></a>

When you checked the "Keep unlocked in 5 minutes" feature, the wallet remains unlocked until the last signed transaction/certificates time plus 5 minutes.

If you wish to lock the wallet again but the wallet still in the unlocked period, you can close Sync to enforce the wallet lock again.

> Note
>
> * locked period means that you need to enter your wallet's password to sign the transaction/certificates.
> * unlocked period: you can sign the transaction/certificate without entering the wallet's password.

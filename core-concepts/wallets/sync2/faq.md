# FAQ

## Add custom network <a href="#add-custom-network" id="add-custom-network"></a>

See [Add node](user-guide/settings.md#add-node) for more details

## Custom wallet <a href="#custom-wallet" id="custom-wallet"></a>

See [custom network wallet](user-guide/wallet.md#custom-network-wallet) for more details

## Signing warning <a href="#signing-warning" id="signing-warning"></a>

Many reasons may cause the transaction failed/reverted. below are some causes:

### Insufficient VTHO <a href="#insufficient-vtho" id="insufficient-vtho"></a>

it means that the address does not have enough VTHO to send the transaction. Please make sure you have enough VTHO before sending the transaction.

### Failed to request transaction fee delegation <a href="#failed-to-request-transaction-fee-delegation" id="failed-to-request-transaction-fee-delegation"></a>

Network condition may affect connection between Sync2 and fee delegation service. You may try the following:

1. Retry signing process
2. Check your network connection status
3. Disconnect Wi-Fi and try with cellular data

### Requested address not owned <a href="#requested-address-not-owned" id="requested-address-not-owned"></a>

Before the user confirms the transaction/certificate details, Sync2 will automatically ensure the designated signer(address) exists in Sync2.

## Ledger troubleshooting <a href="#ledger-troubleshoots" id="ledger-troubleshoots"></a>

### INS\_NOT\_SUPPORTED (0x6d00) <a href="#ins-not-supported-0x6d00" id="ins-not-supported-0x6d00"></a>

* Ensuring your device runs the latest firmware version.
* Reinstalling the apps on your device so you run the latest versions. Uninstalling apps does not affect your crypto assets, that are secured on the blockchain.

### INCORRECT\_DATA (0x6a80) <a href="#incorrect-data-0x6a80" id="incorrect-data-0x6a80"></a>

1. Navigate to VeChain App on your Ledger device
2. Navigate to Setting
3. Set **Contract data** to **Yes**
4. Set **Multi-clause** to **Yes**

### Unable to connect your device <a href="#unable-to-connect-your-device" id="unable-to-connect-your-device"></a>

* Close other applications (Ledger apps, crypto wallets, Geth, Parity, Mist, Bitcoin Core, etc).
* Turn OFF VPN and anti-virus temporarily. If that works, make sure to whitelist Sync.
* Change the USB cable if possible. Try removing any dongles or docks you're using.
* Try different USB ports.
* Restart your computer.
* Try another computer.

### Check status failed <a href="#check-status-failed" id="check-status-failed"></a>

The error "**checking status failed**" shown during the Ledger connection, it means that the device you are trying to connect **IS NOT** the device that belongs to the wallet you imported. In other words, it's a brand new ledger device you never imported. Please check that your Ledger device is the proper device that belongs to the selected account(imported wallet). The easiest way to identify the issue is [import your ledger device](user-guide/wallet.md#link-ledger-device) again and compare the wallet address.

Reset your Ledger device:

1. Reset your Ledger device by entering three wrong PIN codes.
2. [Restore from recovery phrase](https://support.ledger.com/hc/en-us/articles/4404382560913-Restore-from-recovery-phrase?support=true)

{% hint style="info" %}
In case you have multiple Ledger hardware wallets set up with different recovery phrases, you should connect the device holding the recovery phrase used to import the account.
{% endhint %}

### Mis-transfer the funds to ethereum address <a href="#mis-transfer-the-funds-to-ethereum-address" id="mis-transfer-the-funds-to-ethereum-address"></a>

Please check the [Ledger support-Export your accounts](https://support.ledger.com/hc/en-us/articles/115005297709-Export-your-accounts) instruction. Once the private key / keystore is exported, import to Sync wallet.

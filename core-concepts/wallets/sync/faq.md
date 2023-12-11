# FAQ

## Does new sync has a folder store the keystore file ? <a href="#does-new-sync-has-a-folder-store-the-keystore-file" id="does-new-sync-has-a-folder-store-the-keystore-file"></a>

No, only if user backup(export) the wallet will generate the keystore file.

Please check [Export wallet](user-guide/wallet.md#export-keystore)

## How to connect custom node ? <a href="#how-to-connect-custom-node" id="how-to-connect-custom-node"></a>

1. [Run thor](../../../developer-resources/tutorials/how-to-run-a-thor-solo-node/)
2. Open Sync
3. Follow the step to [add custom node](user-guide/browser-dapps-and-web.md#connect-to-a-node)

## Certificate of Identification / Agreement <a href="#certificate-of-identification-agreement" id="certificate-of-identification-agreement"></a>

The certificate is a message signing based mechanism which can easily request a user's identification(address) or a user agree to dApp term of use or service.

The purpose of the certificate of identification is a way that allows dApps to send you a random challenge to prove that you are the owner of the wallet. **It proves that you are the owner of the wallet.**

On other hands, the certificate of agreement is a certificate that you agree to dApp's term of use or service. The agreement come in many forms before you agree to the content, please always review the content which provided by dApp. Once you signed the agreement. **it proves that you are the wallet owner and agree to the dApp's term of use or service.**

## How to get test token ? <a href="#how-to-get-test-token" id="how-to-get-test-token"></a>

You can visit [Faucet](https://faucet.vecha.in/)

## How to open developer tools? <a href="#how-to-open-developer-tools" id="how-to-open-developer-tools"></a>

### **Main Processor(ONLY Available in Dev Mode)**

1. Move your cursor to tab area
2. Right click the mouse
3. Click "**Inspect Element**"

### **Web Content**

1. At upper right, Click <img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADAAAAAwCAYAAABXAvmHAAAABGdBTUEAALGPC/xhBQAAAAFzUkdCAK7OHOkAAAAgY0hSTQAAeiYAAICEAAD6AAAAgOgAAHUwAADqYAAAOpgAABdwnLpRPAAAAAZiS0dEAAAAAAAA+UO7fwAAAAlwSFlzAAAASAAAAEgARslrPgAAALtJREFUaN7t1jEKwkAURdGrdlrFZcT1mN3YuAoXIVmIlY2QLVhZxUrQIlbBDARmGAbv6ZKB/P+KDA8kSf9skei7FdAA9fe5A1rgXkKACjgAm9H7J3AEHjGHLRMEaH4sD7AG9rGHpQhQB852JQQIeZcQoAuc3UoI0DL8sGM9cI49bJUgQA9cGG6jLfACrsCJyDeQJLvQ5PJ2oZwB7EK5A9iF5rALSYWzC00sbxfKGcAulDuAXWgOu5AkqWgfHD423xLS/bIAAAAldEVYdGRhdGU6Y3JlYXRlADIwMTktMDEtMTRUMDI6NTc6MjQrMDA6MDAV2juNAAAAJXRFWHRkYXRlOm1vZGlmeQAyMDE5LTAxLTE0VDAyOjU3OjI0KzAwOjAwZIeDMQAAACh0RVh0c3ZnOmJhc2UtdXJpAGZpbGU6Ly8vdG1wL21hZ2ljay1VYjFzVjRNcm821ZwAAAAASUVORK5CYII=" alt="" data-size="line">
2. Click"**Toggle Developer Tools**"

## Transaction Related

### How to transfer all VTHO? <a href="#how-to-transfer-all-vtho" id="how-to-transfer-all-vtho"></a>

Due to the transaction required VTHO to send a transaction, you need to deduct the transaction fee (VTHO) before sending it.

$$T_{amount} = VTHO_{total} - VTHO_{fee}$$

### Insufficient energy while signing a transaction <a href="#insufficient-energy-while-signing-a-transaction" id="insufficient-energy-while-signing-a-transaction"></a>

If you see this error during the signing process, it means that "Not enough VTHO to send transaction." Please make sure you have enough VTHO before sending the transaction.

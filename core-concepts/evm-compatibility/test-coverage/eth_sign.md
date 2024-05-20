# eth\_sign

## Description

The `eth_sign` issue arises due to the fact that Vechain and Ethereum use different hash functions, more information on this subject [here](https://github.com/vechain/vechain-docs/blob/main/core-concepts/evm-compatibility/test-coverage/broken-reference/README.md). This failure is justifiable as it is a design difference between the two chains. To fix the failing tests, we imported Ethereum's hash function and replaced the `eth_sign` method with one that generates signatures using the required hash function.

The following changes we made:

#### In `compatProvider.ts`

In `web3-providers-connex/src/compatProvider.ts` we changed the error response returned to the following:

```javascript
.catch(err => callback(err, {
				id: payload.id,
				jsonrpc: '2.0',
				error: err
			}));
```

#### In `provider.ts`

In `web3-providers-connex/src/provider.ts` we imported `hashEthMessage` and `bufferToHex` from `utils.js`

```javascript
import { hexToNumber, getErrMsg, toSubscription, toHex, hashEthMessage, bufferToHex } from './utils';
```

We also added the method `eth_sign` in the method map

```javascript
this._methodMap['eth_sign'] = this._sign;
```

and defined the function in the same file

```javascript
private _sign = async (params: any) => {
		if (!this.wallet || this.wallet.list.length === 0) {
			throw new Error("no wallet specified");
		}

		const address = params[0];
		const message = params[1];

		const key = this.wallet.list.find((key) => key.address == address);

		if (key === undefined) {
			throw new Error(`key undefined for address ${address}`)
		}

		const hash = hashEthMessage(message);

		if (hash === undefined) {
			throw new Error("undefined hash");
		}

		const hashStriped = hash?.substring(2);
		const buf = Buffer.from(hashStriped!, 'hex');

		const signature = await key.sign(buf);
		signature[64] += 27;

		return bufferToHex(signature);
	}
```

#### In `utils.ts`

In `web3-providers-connex/src/utils.ts` we imported `keccak256` from 'thor-devkit'.

```javascript
import { abi, keccak256, Transaction } from 'thor-devkit';
```

Then we defined two new functions `hashEthMessage` that hashes a string with Ethereum's hash function and a helper function `bufferToHex`.

```javascript
export function bufferToHex(buf: Buffer) : string {
	return '0x' + buf.toString('hex');
}

export function hashEthMessage(data: string) : string {
	const messageHex = web3Utils.isHexStrict(data) ? data : web3Utils.utf8ToHex(data);
	const messageBytes = web3Utils.hexToBytes(messageHex);
	const messageBuffer = Buffer.from(messageBytes);
	const preamble = '\x19Ethereum Signed Message:\n' + messageBytes.length;
	const preambleBuffer = Buffer.from(preamble);
	const ethMessage = Buffer.concat([preambleBuffer, messageBuffer]);
	return bufferToHex(keccak256(ethMessage));
```

#### In `getChainId.test.ts`

The final change was in `web3-providers-connex/test/web3/getChainId.test.ts` where we replaced the main-net URL with the local instance of thor instead.

```javascript
const net = new SimpleNet("http://127.0.0.1:8669");
```

## Contracts Affected

| Contract Name    |
| ---------------- |
| SignatureChecker |

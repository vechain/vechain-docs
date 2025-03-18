# Name Service Lookups

The SDK provides programmatic access to the VeChain Name Service (VNS) at [vet.domains](https://vet.domains).

Name Services provide the ability to use human-readable names that point to addresses.

## Resolve Names

`vnsUtils` is available within the network module and can be used with a ThorClient.

After importing and connecting the ThorClient, `resolveName` and `resolveNames` provide access to resolve single or multiple names. If a name is not known or configured, `null` is returned instead of an address.

```ts
import { ThorClient, vnsUtils } from '@vechain/sdk-network';
const thor = ThorClient.at('https://mainnet.vechain.org');

console.log('resolveName', await vnsUtils.resolveName(thor, 'test.vet'));
console.log('resolveNames', await vnsUtils.resolveNames(thor, ['test.vet']));
console.log(
  'resolveName',
  await vnsUtils.resolveName(thor, '_invalid_test.vet')
);
```

## Lookup Addresses

After importing and connecting the ThorClient, `lookupAddress` and `lookupAddresses` provide access to resolve single or multiple addresses. If an address has no (valid) primary name, a `null` is returned instead of a string.

```ts
import { ThorClient, vnsUtils } from '@vechain/sdk-network';
const thor = ThorClient.at('https://mainnet.vechain.org');

console.log(
  'lookupAddress',
  await vnsUtils.lookupAddress(
    thor,
    '0x105199a26b10e55300CB71B46c5B5e867b7dF427'
  )
);
console.log(
  'lookupAddresses',
  await vnsUtils.lookupAddresses(thor, [
    '0x105199a26b10e55300CB71B46c5B5e867b7dF427',
  ])
);
console.log(
  'lookupAddress',
  await vnsUtils.lookupAddress(
    thor,
    '0x0000000000000000000000000000000000000000'
  )
);

```

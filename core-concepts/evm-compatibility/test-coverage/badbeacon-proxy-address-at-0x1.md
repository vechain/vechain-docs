# BadBeacon proxy address at 0x1

## Description

The issue described in this section occurs because the `BadBeaconNotContract` returned an invalid address. The necessary change in order to fix this issue was to replace the returned address `0x1` with `0xFFF`.

```solidity
contract BadBeaconNotContract {
    function implementation() external pure returns (address) {
        return address(0xFFF);
    }
```

## Contracts Affected

| Contract Name |
|---------------|
| BeaconProxy   |

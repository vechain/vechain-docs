---
description: use variables to customise your components
---

# Theme Variables

black mode palette:

[https://coolors.co/404040-2a2a2a-ffffff-888888](https://coolors.co/404040-2a2a2a-ffffff-888888)

light mode palette

[https://coolors.co/f2f2f2-ffffff-2a2a2a-747474](https://coolors.co/f2f2f2-ffffff-2a2a2a-747474)

***

### Use themeVariables

```typescript
import {CustomizedStyle, DAppKitUI, DAppKitUIOptions} from '@vechain/dapp-kit-ui';

const styles: CustomizedStyle = {
  '--vwk-modal-z-index': '9999',
}

const vechainDAppKitOptions: DAppKitUIOptions = {
    node: 'https://testnet.vechain.org/',
    genesis: 'test',
    themeVariables: {
        '--vdk-color-dark-primary': '#404040',
        '--vdk-color-dark-primary-hover': '#454545',
        '--vdk-color-dark-primary-active': '#4a4a4a',
        '--vdk-color-dark-secondary': '#2a2a2a',
        '--vdk-color-dark-tertiary': '#ffffff',
        '--vdk-color-dark-quaternary': '#888888',
        '--vdk-color-light-primary': '#f2f2f2',
        '--vdk-color-light-primary-hover': '#eeeeee',
        '--vdk-color-light-primary-active': '#eaeaea',
        '--vdk-color-light-secondary': '#ffffff',
        '--vdk-color-light-tertiary': '#2a2a2a',
        '--vdk-color-light-quaternary': '#747474',
        '--vdk-color-walletconnectblue': '#3496ff',
        '--vdk-font-family': "Inter, sans-serif",
        '--vdk-font-size-medium': '14px',
        '--vdk-font-size-large': '18px',
        '--vdk-font-weight-medium': '500',
        '--vdk-modal-z-index': '200',
    },
};

DAppKitUI.configure(vechainWalletKitOptions);
```

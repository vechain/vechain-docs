---
description: 'this are the most important changes between v0 and v1:'
---

# V0 to V1

### Overview

We changed how we handle the modal, rendering it as a separate component instead of rendering it right below the button.

Because of that, we decided to pass all the configurations to the DappKitUI.configure function instead of passing them to the components.

We cleaned and simplified the naming conventions.

### React

we changed the component name

`ConnectButtonWithModal` -> `WalletButton`

### Vanilla

we changed the component name

`vwk-vechain-dapp-connect-kit` -> `vdk-button`

### Configuration

these are the added configurations for the DappKitUI.configure function:

```typescript
// OPTIONAL: theme variables (check theme variables section)
themeVariables={ThemeVariables}
// OPTIONAL: app current language
language="en";
// OPTIONAL: i18n default object (check i18n section)
i18n={defaultI18n}
// OPTIONAL: where to render the modal, document.body is the default
modalParent={document.body}
// OPTIONAL: handle source click to customise wallet connect
onSourceClick={source => void}
```

CSS variables configuration is now removed and replaced by the above [themeVariables](theme.md) object

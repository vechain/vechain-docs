---
description: use CSS variables to customise your components
---

# Theme

variables that can be customized:

```css
:root {
    # color variables
    --vwk-color-dark-primary: #404040;
    --vwk-color-dark-primary-hover: #454545;
    --vwk-color-dark-primary-active: #4a4a4a;
    --vwk-color-dark-secondary: #2a2a2a;
    --vwk-color-dark-tertiary: #ffffff;
    --vwk-color-dark-quaternary: #888888;
    --vwk-color-light-primary: #f2f2f2;
    --vwk-color-light-primary-hover: #eeeeee;
    --vwk-color-light-primary-active: #eaeaea;
    --vwk-color-light-secondary: #ffffff;
    --vwk-color-light-tertiary: #2a2a2a;
    --vwk-color-light-quaternary: #747474;
    --vwk-color-walletconnectblue: #3496ff;
    
    # font variables
    --vwk-font-family: 'Inter', sans-serif;
    --vwk-font-size-medium: 14px;
    --vwk-font-size-large: 18px;
    --vwk-font-weight-medium: 500;

}
```

example of a vechain theme:

```css
:root {
    --vwk-color-dark-primary: linear-gradient(
        90deg,
        rgba(40, 0, 140, 1) 16%,
        rgba(0, 190, 215, 1) 60%,
        rgba(130, 190, 0, 1) 100%
    );
    --vwk-color-dark-primary-hover: linear-gradient(
        90deg,
        rgba(40, 0, 140, 1) 16%,
        rgba(0, 190, 215, 1) 60%,
        rgba(130, 190, 0, 1) 100%
    );
    --vwk-color-dark-primary-active: linear-gradient(
        90deg,
        rgba(40, 0, 140, 1) 16%,
        rgba(0, 190, 215, 1) 60%,
        rgba(130, 190, 0, 1) 100%
    );
    --vwk-color-dark-secondary: #2a2a2a;
    --vwk-color-dark-tertiary: #ffffff;
    --vwk-color-dark-quaternary: #888888;
    --vwk-color-light-primary: linear-gradient(
        90deg,
        rgba(0, 190, 215, 1) 60%,
        rgba(130, 190, 0, 1) 100%
    );
    --vwk-color-light-primary-hover: linear-gradient(
        90deg,
        rgba(0, 190, 215, 1) 60%,
        rgba(130, 190, 0, 1) 100%
    );
    --vwk-color-light-primary-active: linear-gradient(
        90deg,
        rgba(0, 190, 215, 1) 60%,
        rgba(130, 190, 0, 1) 100%
    );
    --vwk-color-light-secondary: #ffffff;
    --vwk-color-light-tertiary: #2a2a2a;
    --vwk-color-light-quaternary: #747474;
}
```

---
description: >-
  dApp-kit has been built on top of Connex, which will require crypto, buffer,
  http, https and some other node polyfills, check example app configuration
  files if you are stuck.
---

# Node Polyfills

### 1) Require is not a function

this usually happens when working with [vite](https://vitejs.dev/) bundler. This config fixes it:

**vite.config.ts**

```typescript
export default defineConfig({
    ...
    build: {
        commonjsOptions: {
            transformMixedEsModules: true,
        },
    }
    ...
})
```

### 2) \[crypto, http, https, stream, etc...] module not found

you miss some node polyfills, the fix depends on the bundler

example for vite bundler using \`vite-plugin-node-polyfills\`:

**vite.config.ts**

```typescript
import { nodePolyfills } from 'vite-plugin-node-polyfills';

export default defineConfig({
    plugins: [nodePolyfills()],
    ...
})
```

### 3) Can't find variable \[Buffer, process, global]

it's a common issue when you miss other node polyfills.\
in Angular we fixed it like so:

**src/polyfills.ts**

```typescript
(window as any).global = window;
global.Buffer = global.Buffer || require('buffer').Buffer;
(window as any).process = {
    env: { DEBUG: undefined },
    version: '', // to avoid undefined.slice error
};
```

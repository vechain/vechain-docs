---
description: >-
  How to install thor-devkit.js in order to use it with TypeScript or
  Javascript.
---

# Installation

If using TypeScript follow the NPM installation steps, for JavaScript follow the CommonJS (CJS) installation steps.

{% hint style="info" %}
Should you wish to implement this in a pure JavaScript project, it is recommended to use CommonJS (CJS) imports. Potential complications might arise with ES Module (ESM) imports.
{% endhint %}

## NPM

```bash
npm i thor-devkit
```

Upon installation, you may utilize the subsequent code snippet to verify the proper functioning within your TypeScript project:

```typescript
import { keccak256 } from 'thor-devkit'

console.log(keccak256('hello world').toString('hex')) 
// 47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad
```

## CJS

1. Set "commonjs" type in \`package.json\` file:

```json
{
    ...
    "type": "commonjs",
    ...
}
```

2. Use **require** instead of **import**:

```javascript
// ESM
import { keccak256 } from 'thor-devkit'

console.log(keccak256('hello world').toString('hex')) 
// 47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad

// CJS
const keccak256 = require('thor-devkit').keccak256

console.log(keccak256('hello world').toString('hex'))
// 47173285a8d7341e5e972fc677286384f802f8ef42a5ec5f03bbfa254cb01fad
```

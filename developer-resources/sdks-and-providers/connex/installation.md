---
description: How to install Connex.
---

# Installation

Connex is available to developers in several ways. The installation approach does not influence or modify the Connex features. Connex can be installed in any of the following ways:

1. **Browser Implementation:** This conventional utilization aligns with dApp development similar to the EIP-1193 standard. In this context, Connex facilitates connections with Sync/Sync2 or VeWorld. This approach has two Sub-approaches:
   1. NPM
   2. Using Content Delivery Network (CDN)
2. **Framework:** This technique empowers the instantiation of a Connex instance from the ground up. It is commonly employed for NodeJS projects and command line interface (CLI) applications.

{% hint style="info" %}
The below snippets contain links to veblocks nodes feel free to connect to any of the public nodes [nodes.md](../../nodes.md "mention")
{% endhint %}

## Connex Browser implementation

### NPM

```bash
npm i @vechain/connex
```

Below is a snippet using Connex and React:

```javascript
import { Connex } from '@vechain/connex'
import { useMemo } from 'react'

/**
 * Connex instance
 */
const connexInstance = new Connex({
  node: 'https://mainnet.veblocks.net/',
  network: 'main'
})

export default function SimpleComponentWithConnex() {

  // Better to use useMemo to avoid re-rendering
  const connex: Connex = useMemo(() => {
    return connexInstance
  }, [connexInstance])

  return (
    <>
      <div>
        <p>{connex.thor.genesis.id}</p>
      </div>
    </>
  )
}
```

### CDN

The Connex library can be seamlessly integrated by employing the subsequent CDN hyperlink:

```html
<!-- install the latest v2 -->
<script src="https://unpkg.com/@vechain/connex@2" />
```

Below is a snippet using Connex and HTML:

```html
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>Connex Test Project</title>

    <!-- install the latest v2 -->
    <script src="https://unpkg.com/@vechain/connex@2"></script>
</head>

<body>
    <script>
        // Initialize Connex on mainnet
        const connex = new Connex({
            node: 'https://mainnet.veblocks.net/',
            network: 'main'
        })

        // Simple log of genesis block id
        console.log(connex.thor.genesis.id)
    </script>
</body>

</html>
```

## Framework

```bash
npm i @vechain/connex-framework @vechain/connex-driver
```

You can create a low level Connex instance using the following example:

```javascript
import { Driver, SimpleNet } from '@vechain/connex-driver'
import { Framework } from '@vechain/connex-framework'

// Init newtork and driver
const network = new SimpleNet('https://mainnet.veblocks.net/')
const driver = await Driver.connect(network)

// Init connex instance
const connex = new Framework(driver)

console.log(connex.thor.genesis.id)
```

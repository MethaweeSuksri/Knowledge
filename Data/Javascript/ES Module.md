---
status: done
Recall: None
source: trust me bro
---

#runtime #interpreter 

---

# What ESM is

ESM is short for ES module, a way to import javascript program.

## 1. Enable ESM

In `package.json`:

```json
{
  "type": "module"
}
```

---

## 2. Export

```js
// math.js

export function add(a, b) {
  return a + b;
}

export const PI = 3.14;
```

---

## 3. Import

```js
// app.js

import { add, PI } from "./math.js";

console.log(add(2, 3));
console.log(PI);
```

---

## Default export

Export:

```js
// math.js

export default function add(a, b) {
  return a + b;
}
```

Import:

```js
import add from "./math.js";
```

### Remember

```text
Named:
export        → import { name }

Default:
export default → import name
```

And with Node.js ESM, **include `.js` in local imports**:

```js
import { add } from "./math.js";
```
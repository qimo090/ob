---
created: 2024-07-13T15:08
updated: 2024-07-13T19:17
---
# Problem

```ts file:07-create-new-set.problem.ts
import { Equal, Expect } from "../helpers/type-utils";

export const createSet = () => {
  return new Set();
};

const stringSet = createSet<string>();
const numberSet = createSet<number>();
const unknownSet = createSet();

type tests = [
  Expect<Equal<typeof stringSet, Set<string>>>,
  Expect<Equal<typeof numberSet, Set<number>>>,
  Expect<Equal<typeof unknownSet, Set<unknown>>>,
];
```

# Solution
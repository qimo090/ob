---
created: 2024-07-13T15:08
updated: 2024-07-13T21:30
---
# Problem

```ts file:08-default-generics.problem.ts
import { Equal, Expect } from "../helpers/type-utils";

export const createSet = <T>() => {
  return new Set<T>();
};

const numberSet = createSet<number>();
const stringSet = createSet<string>();
const otherStringSet = createSet();

type tests = [
  Expect<Equal<typeof numberSet, Set<number>>>,
  Expect<Equal<typeof stringSet, Set<string>>>,
  Expect<Equal<typeof otherStringSet, Set<string>>>
];
```

# Solution

```ts file:08-default-generics.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";

export const createSet = <T = string>() => {
  return new Set<T>();
};

const numberSet = createSet<number>();
const stringSet = createSet<string>();
const otherStringSet = createSet();

type tests = [
  Expect<Equal<typeof numberSet, Set<number>>>,
  Expect<Equal<typeof stringSet, Set<string>>>,
  Expect<Equal<typeof otherStringSet, Set<string>>>,
];
```
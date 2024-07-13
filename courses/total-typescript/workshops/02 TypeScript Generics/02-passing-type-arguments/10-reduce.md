---
created: 2024-07-13T15:08
updated: 2024-07-13T21:35
---
# Problem

```ts file:10-reduce.problem.ts
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

const array = [
  {
    name: "John",
  },
  {
    name: "Steve",
  },
];

const obj = array.reduce((accum, item) => {
  accum[item.name] = item;
  return accum;
}, {});

it("Should resolve to an object where name is the key", () => {
  expect(obj).toEqual({
    John: {
      name: "John",
    },
    Steve: {
      name: "Steve",
    },
  });

  type tests = [Expect<Equal<typeof obj, Record<string, { name: string }>>>];
});
```

# Solution

```ts file:10-reduce.solution.ts fold
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

const array = [
  {
    name: "John",
  },
  {
    name: "Steve",
  },
];

const obj = array.reduce<Record<string, { name: string }>>((accum, item) => {
  accum[item.name] = item;
  return accum;
}, {});

it("Should resolve to an object where name is the key", () => {
  expect(obj).toEqual({
    John: {
      name: "John",
    },
    Steve: {
      name: "Steve",
    },
  });

  type tests = [Expect<Equal<typeof obj, Record<string, { name: string }>>>];
});
```

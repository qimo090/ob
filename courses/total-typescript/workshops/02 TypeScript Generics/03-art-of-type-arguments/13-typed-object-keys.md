---
created: 2024-07-28T11:09
updated: 2024-07-28T11:18
---
# Problem

```ts file:13-typed-object-keys.problem.ts
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

/**
 * There are two possible solutions to this problem - and it's
 * to do with the way you specify the generic. Can you get
 * both solutions?
 */
const typedObjectKeys = (obj: unknown) => {
  return Object.keys(obj);
};

it("Should return the keys of the object", () => {
  const result1 = typedObjectKeys({
    a: 1,
    b: 2,
  });

  expect(result1).toEqual(["a", "b"]);

  type test = Expect<Equal<typeof result1, Array<"a" | "b">>>;
});
```

# Solution

```ts file:13-typed-object-keys.solution.1.ts fold
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

/**
 * You can either specify the entire object in
 * the generic slot...
 */
const typedObjectKeys = <TObject extends object>(obj: TObject) => {
  return Object.keys(obj) as Array<keyof TObject>;
};

it("Should return the keys of the object", () => {
  const result1 = typedObjectKeys({
    a: 1,
    b: 2,
  });

  expect(result1).toEqual(["a", "b"]);

  type test = Expect<Equal<typeof result1, Array<"a" | "b">>>;
});
```

```ts file:13-typed-object-keys.solution.2.ts fold
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

/**
 * ...or you can specify the keys of the object.
 */
const typedObjectKeys = <TKey extends string>(obj: Record<TKey, any>) => {
  return Object.keys(obj) as Array<TKey>;
};

it("Should return the keys of the object", () => {
  const result1 = typedObjectKeys({
    a: 1,
    b: 2,
  });

  expect(result1).toEqual(["a", "b"]);

  type test = Expect<Equal<typeof result1, Array<"a" | "b">>>;
});
```
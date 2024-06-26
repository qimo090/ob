---
created: 2024-06-26T22:30
updated: 2024-06-26T22:32
tags:
  - TypeScript
  - TypeScript/Generic
---
# Problem

```ts file:01-return-what-i-pass-in.problem.ts
import { Equal, Expect } from "../helpers/type-utils";

const returnWhatIPassIn = (t: unknown) => {
  return t;
};

const one = returnWhatIPassIn(1);
const matt = returnWhatIPassIn("matt");

type tests = [Expect<Equal<typeof one, 1>>, Expect<Equal<typeof matt, "matt">>];
```

# Solution

```ts file:01-return-what-i-pass-in.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";

const returnWhatIPassIn = <T>(t: T) => {
  return t;
};

const one = returnWhatIPassIn(1);
const matt = returnWhatIPassIn("matt");

type tests = [Expect<Equal<typeof one, 1>>, Expect<Equal<typeof matt, "matt">>];
```
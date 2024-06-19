---
created: 2024-06-10T18:15
updated: 2024-06-12T22:37
tags:
  - TypeScript
  - TypeScript/ConditionalTypes
url: https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#handbook-content
---
# Problem

```ts file:21-conditional-types.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type YouSayGoodbyeAndISayHello = unknown;  
  
type tests = [  
  Expect<Equal<YouSayGoodbyeAndISayHello<"hello">, "goodbye">>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<"goodbye">, "hello">>,  
];
```

# Solution

```ts file:21-conditional-types.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type YouSayGoodbyeAndISayHello<T> = T extends "hello" ? "goodbye" : "hello";  
  
type tests = [  
  Expect<Equal<YouSayGoodbyeAndISayHello<"hello">, "goodbye">>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<"goodbye">, "hello">>,  
];
```
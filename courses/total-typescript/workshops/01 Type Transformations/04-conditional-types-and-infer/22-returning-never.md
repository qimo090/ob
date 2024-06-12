---
created: 2024-06-12T22:24
updated: 2024-06-12T22:36
tags:
  - TypeScript
  - TypeScript/ConditionalTypes
url: https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#handbook-content
---
# Problem

```ts file:22-returning-never.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type YouSayGoodbyeAndISayHello<T> = T extends "hello" ? "goodbye" : "hello";  
  
type tests = [  
  Expect<Equal<YouSayGoodbyeAndISayHello<"hello">, "goodbye">>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<"goodbye">, "hello">>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<"alright pal">, never>>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<1>, never>>,  
];
```

# Solution 

```ts file:22-returning-never.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type YouSayGoodbyeAndISayHello<T> = T extends "hello" | "goodbye"  
  ? T extends "hello"  
    ? "goodbye"  
    : "hello"  
  : never;  
  
type tests = [  
  Expect<Equal<YouSayGoodbyeAndISayHello<"hello">, "goodbye">>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<"goodbye">, "hello">>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<"alright pal">, never>>,  
  Expect<Equal<YouSayGoodbyeAndISayHello<1>, never>>,  
];
```
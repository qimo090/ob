---
created: 2024-06-12T22:35
updated: 2024-06-12T22:43
tags:
  - TypeScript
  - TypeScript/Infer
url: https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types
---
# Problem

```ts file:23-infer-with-raw-values.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type GetDataValue<T> = unknown;  
  
type tests = [  
  Expect<Equal<GetDataValue<{ data: "hello" }>, "hello">>,  
  Expect<Equal<GetDataValue<{ data: { name: "hello" } }>, { name: "hello" }>>,  
  Expect<  
    Equal<  
      GetDataValue<{ data: { name: "hello"; age: 20 } }>,  
      { name: "hello"; age: 20 }  
    >  
  >,  
  // Expect that if you pass in string, it  
  // should return never  Expect<Equal<GetDataValue<string>, never>>,  
];
```

# Solution

```ts file fold
import { Equal, Expect } from "../helpers/type-utils";  
  
// type GetDataValue<T> = T extends { data: any } ? T["data"] : never;  
type GetDataValue<T> = T extends { data: infer TData } ? TData : never;  
  
type tests = [  
  Expect<Equal<GetDataValue<{ data: "hello" }>, "hello">>,  
  Expect<Equal<GetDataValue<{ data: { name: "hello" } }>, { name: "hello" }>>,  
  Expect<  
    Equal<  
      GetDataValue<{ data: { name: "hello"; age: 20 } }>,  
      { name: "hello"; age: 20 }  
    >  
  >,  
  // Expect that if you pass in string, it  
  // should return never  Expect<Equal<GetDataValue<string>, never>>,  
];
```
---
created: 2024-06-10T13:53
updated: 2024-06-10T13:56
tags:
  - TypeScript
  - TypeScript/Generic
url: https://www.typescriptlang.org/docs/handbook/2/generics.html
---
# Problem

```ts file:20-type-helpers-pattern.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type ReturnWhatIPassIn = unknown;  
  
type tests = [  
  Expect<Equal<ReturnWhatIPassIn<1>, 1>>,  
  Expect<Equal<ReturnWhatIPassIn<"1">, "1">>,  
  Expect<Equal<ReturnWhatIPassIn<true>, true>>,  
  Expect<Equal<ReturnWhatIPassIn<false>, false>>,  
  Expect<Equal<ReturnWhatIPassIn<null>, null>>,  
];
```

# Solution

```ts file:20-type-helpers-pattern.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type ReturnWhatIPassIn<T> = T;  
  
type tests = [  
  Expect<Equal<ReturnWhatIPassIn<1>, 1>>,  
  Expect<Equal<ReturnWhatIPassIn<"1">, "1">>,  
  Expect<Equal<ReturnWhatIPassIn<true>, true>>,  
  Expect<Equal<ReturnWhatIPassIn<false>, false>>,  
  Expect<Equal<ReturnWhatIPassIn<null>, null>>,  
];
```
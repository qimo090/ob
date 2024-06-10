---
created: 2024-06-10T11:08
updated: 2024-06-10T11:11
---
# Problem

```ts file:13-get-array-value.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
const fruits = ["apple", "banana", "orange"];  
  
type AppleOrBanana = unknown;  
type Fruit = unknown;  
  
type tests = [  
  Expect<Equal<AppleOrBanana, "apple" | "banana">>,  
  Expect<Equal<Fruit, "apple" | "banana" | "orange">>,  
];
```

# Solution

```ts file:13-get-array-value.solution.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
const fruits = ["apple", "banana", "orange"] as const;  
  
type AppleOrBanana = typeof fruits[0 | 1];  
type Fruit = typeof fruits[number];  
  
type tests = [  
  Expect<Equal<AppleOrBanana, "apple" | "banana">>,  
  Expect<Equal<Fruit, "apple" | "banana" | "orange">>,  
];
```
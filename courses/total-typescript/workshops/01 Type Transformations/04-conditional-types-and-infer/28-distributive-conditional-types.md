---
created: 2024-06-12T23:14
updated: 2024-06-12T23:20
---
# Problem

```ts file:28-distributive-conditional-types.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Fruit = "apple" | "banana" | "orange";  
  
type AppleOrBanana = Fruit extends "apple" | "banana" ? Fruit : never;  
  
type tests = [Expect<Equal<AppleOrBanana, "apple" | "banana">>];
```

# Solution

```ts file:28-distributive-conditional-types.solution.1.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Fruit = "apple" | "banana" | "orange";  
  
type AppleOrBanana = Fruit extends infer T  
  ? T extends "apple" | "banana"  
    ? T  
    : never  
  : never;  
  
type tests = [Expect<Equal<AppleOrBanana, "apple" | "banana">>];
```

```ts file:28-distributive-conditional-types.solution.2.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Fruit = "apple" | "banana" | "orange";  
  
type GetAppleOrBanana<T> = T extends "apple" | "banana" ? T : never;  
  
type AppleOrBanana = GetAppleOrBanana<Fruit>;  
  
type tests = [Expect<Equal<AppleOrBanana, "apple" | "banana">>];
```
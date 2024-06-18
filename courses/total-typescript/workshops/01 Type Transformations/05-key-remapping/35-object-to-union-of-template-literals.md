---
created: 2024-06-18T23:46
updated: 2024-06-18T23:49
---
# Problem

```ts file:35-object-to-union-of-template-literals.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
interface FruitMap {  
  apple: "red";  
  banana: "yellow";  
  orange: "orange";  
}  
  
type TransformedFruit = unknown;  
  
type tests = [  
  Expect<  
    Equal<TransformedFruit, "apple:red" | "banana:yellow" | "orange:orange">  
  >,  
];
```

# Solution

```ts file:35-object-to-union-of-template-literals.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
interface FruitMap {  
  apple: "red";  
  banana: "yellow";  
  orange: "orange";  
}  
  
type TransformedFruit = {  
  [F in keyof FruitMap]: `${F}:${FruitMap[F]}`;  
}[keyof FruitMap];  
  
type tests = [  
  Expect<  
    Equal<TransformedFruit, "apple:red" | "banana:yellow" | "orange:orange">  
  >,  
];
```
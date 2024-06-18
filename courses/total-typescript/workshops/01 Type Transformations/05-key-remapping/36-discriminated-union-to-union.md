---
created: 2024-06-18T23:46
updated: 2024-06-19T00:00
---
# Problem

```ts file:36-discriminated-union-to-union.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Fruit =  
  | {  
      name: "apple";  
      color: "red";  
    }  
  | {  
      name: "banana";  
      color: "yellow";  
    }  
  | {  
      name: "orange";  
      color: "orange";  
    };  
  
type TransformedFruit = unknown;  
  
type tests = [  
  Expect<  
    Equal<TransformedFruit, "apple:red" | "banana:yellow" | "orange:orange">  
  >,  
];
```

# Solution

```ts file:36-discriminated-union-to-union.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Fruit =  
  | {  
      name: "apple";  
      color: "red";  
    }  
  | {  
      name: "banana";  
      color: "yellow";  
    }  
  | {  
      name: "orange";  
      color: "orange";  
    };  
  
type TransformedFruit = {  
  [F in Fruit as F["name"]]: `${F["name"]}:${F["color"]}`;  
}[Fruit["name"]];  
  
type tests = [  
  Expect<  
    Equal<TransformedFruit, "apple:red" | "banana:yellow" | "orange:orange">  
  >  
];
```
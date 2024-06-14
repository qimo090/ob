---
created: 2024-06-15T00:36
updated: 2024-06-15T00:36
---
# Problem

```ts file:30-k-in-keyof.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
interface Attributes {  
  firstName: string;  
  lastName: string;  
  age: number;  
}  
  
type AttributeGetters = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      AttributeGetters,  
      {  
        firstName: () => string;  
        lastName: () => string;  
        age: () => number;  
      }  
    >  
  >  
];
```

# Solution

```ts file:30-k-in-keyof.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
interface Attributes {  
  firstName: string;  
  lastName: string;  
  age: number;  
}  
  
type AttributeGetters = {  
  [K in keyof Attributes]: () => Attributes[K];  
};  
  
type tests = [  
  Expect<  
    Equal<  
      AttributeGetters,  
      {  
        firstName: () => string;  
        lastName: () => string;  
        age: () => number;  
      }  
    >  
  >,  
];
```
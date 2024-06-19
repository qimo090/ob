---
created: 2024-06-18T23:35
updated: 2024-06-18T23:46
---
# Problem

```ts file:34-object-to-union-of-tuples.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
interface Values {  
  email: string;  
  firstName: string;  
  lastName: string;  
}  
  
type ValuesAsUnionOfTuples = {  
  [K in keyof Values]: [K, Values[K]];  
};  
  
type tests = [  
  Expect<  
    Equal<  
      ValuesAsUnionOfTuples,  
      ["email", string] | ["firstName", string] | ["lastName", string]  
    >  >  
];
```

# Solution

```ts file:34-object-to-union-of-tuples.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
interface Values {  
  email: string;  
  firstName: string;  
  lastName: string;  
}  
  
type ValuesAsUnionOfTuples = {  
  [V in keyof Values]: [V, Values[V]];  
}[keyof Values];  
  
type tests = [  
  Expect<  
    Equal<  
      ValuesAsUnionOfTuples,  
      ["email", string] | ["firstName", string] | ["lastName", string]  
    >  >,  
];
```
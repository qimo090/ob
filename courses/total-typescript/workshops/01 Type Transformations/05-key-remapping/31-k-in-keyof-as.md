---
created: 2024-06-15T00:42
updated: 2024-06-15T00:43
---
# Problem

```ts file:31-k-in-keyof-as.problem.ts
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
        getFirstName: () => string;  
        getLastName: () => string;  
        getAge: () => number;  
      }  
    >  
  >  
];
```

# Solution

```ts file:31-k-in-keyof-as.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
interface Attributes {  
  firstName: string;  
  lastName: string;  
  age: number;  
}  
  
type AttributeGetters = {  
  [K in keyof Attributes as `get${Capitalize<K>}`]: () => Attributes[K];  
};  
  
type tests = [  
  Expect<  
    Equal<  
      AttributeGetters,  
      {  
        getFirstName: () => string;  
        getLastName: () => string;  
        getAge: () => number;  
      }  
    >  
  >,  
];
```
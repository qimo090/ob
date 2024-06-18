---
created: 2024-06-19T00:02
updated: 2024-06-19T00:04
---
# Problem

```ts file:38-mutually-exclusive-properties.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
interface Attributes {  
  id: string;  
  email: string;  
  username: string;  
}  
  
/**  
 * How do we create a type helper that represents a union * of all possible combinations of Attributes? */type MutuallyExclusive<T> = unknown;  
  
type ExclusiveAttributes = MutuallyExclusive<Attributes>;  
  
type tests = [  
  Expect<  
    Equal<  
      ExclusiveAttributes,  
      | {  
          id: string;  
        }  
      | {  
          email: string;  
        }  
      | {  
          username: string;  
        }  
    >  
  >,  
];
```

# Solution

```ts file:38-mutually-exclusive-properties.solution.ts fold

```
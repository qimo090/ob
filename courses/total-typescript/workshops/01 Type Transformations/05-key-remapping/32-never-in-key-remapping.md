---
created: 2024-06-15T00:43
updated: 2024-06-15T00:43
---
# Problem

```ts file:32-never-in-key-remapping.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
interface Example {  
  name: string;  
  age: number;  
  id: string;  
  organisationId: string;  
  groupId: string;  
}  
  
type OnlyIdKeys<T> = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      OnlyIdKeys<Example>,  
      {  
        id: string;  
        organisationId: string;  
        groupId: string;  
      }  
    >  
  >,  
  Expect<Equal<OnlyIdKeys<{}>, {}>>  
];
```
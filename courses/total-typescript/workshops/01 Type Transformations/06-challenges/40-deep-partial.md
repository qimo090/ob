---
created: 2024-06-19T00:03
updated: 2024-06-19T00:04
---
# Problem

```ts file:40-deep-partial.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type DeepPartial<T> = unknown;  
  
type MyType = {  
  a: string;  
  b: number;  
  c: {  
    d: string;  
    e: {  
      f: string;  
      g: {  
        h: string;  
        i: string;  
      }[];  
    };  
  };  
};  
  
type Result = DeepPartial<MyType>;  
  
type tests = [  
  Expect<  
    Equal<  
      Result,  
      {  
        a?: string;  
        b?: number;  
        c?: {  
          d?: string;  
          e?: {  
            f?: string;  
            g?: {  
              h?: string;  
              i?: string;  
            }[];  
          };  
        };  
      }  
    >  
  >  
];
```

# solution

```ts file:40-deep-partial.solution.ts fold
```
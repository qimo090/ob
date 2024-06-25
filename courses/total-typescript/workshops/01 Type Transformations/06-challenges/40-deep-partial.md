---
created: 2024-06-19T00:03
updated: 2024-06-25T23:10
tags:
  - TypeScript
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
import { Equal, Expect } from "../helpers/type-utils";

type DeepPartial<T> = T extends Array<infer U>
  ? Array<DeepPartial<U>>
  : { [K in keyof T]?: DeepPartial<T[K]> };

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
  >,
];
```
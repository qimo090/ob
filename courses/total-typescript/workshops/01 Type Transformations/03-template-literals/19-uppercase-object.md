---
tags:
  - TypeScript
  - TypeScript/Uppercase
url: https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html#uppercasestringtype
created: 2024-06-10T12:48
updated: 2024-06-10T13:42
---
# Problem

```ts file:19-uppercase-object.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Event = `log_in` | "log_out" | "sign_up";  
  
type ObjectOfKeys = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      ObjectOfKeys,  
      {  
        LOG_IN: string;  
        LOG_OUT: string;  
        SIGN_UP: string;  
      }  
    >  
  >,  
];
```

# Solution

``` ts file:19-uppercase-object.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Event = `log_in` | "log_out" | "sign_up";  
  
type ObjectOfKeys = Record<Uppercase<Event>, string>;  
  
type tests = [  
  Expect<  
    Equal<  
      ObjectOfKeys,  
      {  
        LOG_IN: string;  
        LOG_OUT: string;  
        SIGN_UP: string;  
      }  
    >  
  >  
];
```

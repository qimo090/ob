---
created: 2024-06-10T12:48
updated: 2024-06-10T12:48
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

``` ts file fold
```
---
created: 2024-06-19T00:02
updated: 2024-06-19T00:04
---
# Problem

```ts file:39-discriminated-union-with-unique-values-to-object.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Route =  
  | {  
      route: "/";  
      search: {  
        page: string;  
        perPage: string;  
      };  
    }  
  | { route: "/about" }  
  | { route: "/admin" }  
  | { route: "/admin/users" };  
  
type RoutesObject = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      RoutesObject,  
      {  
        "/": {  
          page: string;  
          perPage: string;  
        };  
        "/about": never;  
        "/admin": never;  
        "/admin/users": never;  
      }  
    >  
  >,  
];
```

# Solution

```ts file:39-discriminated-union-with-unique-values-to-object.solution.ts fold
```
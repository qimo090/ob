---
created: 2024-06-15T00:31
updated: 2024-06-15T00:34
---
# Problem

```ts file:29-union-to-object.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Route = "/" | "/about" | "/admin" | "/admin/users";  
  
type RoutesObject = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      RoutesObject,  
      {  
        "/": "/";  
        "/about": "/about";  
        "/admin": "/admin";  
        "/admin/users": "/admin/users";  
      }  
    >  
  >,  
];
```

# Solution

```ts file:29-union-to-object.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Route = "/" | "/about" | "/admin" | "/admin/users";  
  
type RoutesObject = {  
  [R in Route]: R;  
};  
  
type tests = [  
  Expect<  
    Equal<  
      RoutesObject,  
      {  
        "/": "/";  
        "/about": "/about";  
        "/admin": "/admin";  
        "/admin/users": "/admin/users";  
      }  
    >  
  >,  
];
```
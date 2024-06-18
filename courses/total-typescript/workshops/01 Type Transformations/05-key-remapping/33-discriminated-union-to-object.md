---
created: 2024-06-18T23:30
updated: 2024-06-18T23:34
---
# Problem

```ts file:33-discriminated-union-to-object.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Route =  
  | {  
      route: "/";  
      search: {  
        page: string;  
        perPage: string;  
      };  
    }  
  | { route: "/about"; search: {} }  
  | { route: "/admin"; search: {} }  
  | { route: "/admin/users"; search: {} };  
  
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
        "/about": {};  
        "/admin": {};  
        "/admin/users": {};  
      }  
    >  
  >  
];
```

# Solution

```ts file:33-discriminated-union-to-object.solution.1.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Route =  
  | {  
      route: "/";  
      search: {  
        page: string;  
        perPage: string;  
      };  
    }  
  | { route: "/about"; search: {} }  
  | { route: "/admin"; search: {} }  
  | { route: "/admin/users"; search: {} };  
  
/**  
 * This is useful, but less powerful than solution 2: 
 */
type RoutesObject = {  
  [R in Route["route"]]: Extract<Route, { route: R }>["search"];  
};  
  
type tests = [  
  Expect<  
    Equal<  
      RoutesObject,  
      {  
        "/": {  
          page: string;  
          perPage: string;  
        };  
        "/about": {};  
        "/admin": {};  
        "/admin/users": {};  
      }  
    >  
  >,  
];
```

```ts file:33-discriminated-union-to-object.solution.2.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Route =  
  | {  
      route: "/";  
      search: {  
        page: string;  
        perPage: string;  
      };  
    }  
  | { route: "/about"; search: {} }  
  | { route: "/admin"; search: {} }  
  | { route: "/admin/users"; search: {} };  
  
/**  
 * Here, R represents the individual Route. The lesson here * is that the thing we're iterating DOESN'T have to be a 
 * string | number | symbol, as long as the thing we cast it to 
 * is. 
 */
type RoutesObject = {  
  [R in Route as R["route"]]: R["search"];  
};  
  
type tests = [  
  Expect<  
    Equal<  
      RoutesObject,  
      {  
        "/": {  
          page: string;  
          perPage: string;  
        };  
        "/about": {};  
        "/admin": {};  
        "/admin/users": {};  
      }  
    >  
  >,  
];
```
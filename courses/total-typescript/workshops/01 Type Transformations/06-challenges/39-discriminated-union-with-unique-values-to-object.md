---
created: 2024-06-19T00:02
updated: 2024-06-25T23:09
tags:
  - TypeScript
  - TypeScript/DiscriminatedUnions
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

type RoutesObject = {
  [R in Route as R["route"]]: R extends { search: infer S } ? S : never;
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
        "/about": never;
        "/admin": never;
        "/admin/users": never;
      }
    >
  >
];
```
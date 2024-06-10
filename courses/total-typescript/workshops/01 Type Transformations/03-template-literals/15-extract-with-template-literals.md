---
created: 2024-06-10T12:27
updated: 2024-06-10T12:32
---

# Problem

```ts file:15-extract-with-template-literals.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Routes = "/users" | "/users/:id" | "/posts" | "/posts/:id";  
  
type DynamicRoutes = unknown;  
  
type tests = [Expect<Equal<DynamicRoutes, "/users/:id" | "/posts/:id">>];
```

# Solution

```ts file:15-extract-with-template-literals.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Routes = "/users" | "/users/:id" | "/posts" | "/posts/:id";  
  
type DynamicRoutes = Extract<Routes, `${string}:${string}`>;  
  
type tests = [Expect<Equal<DynamicRoutes, "/users/:id" | "/posts/:id">>];
```
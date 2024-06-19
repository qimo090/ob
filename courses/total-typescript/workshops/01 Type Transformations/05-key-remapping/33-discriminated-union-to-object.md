---
created: 2024-06-18T23:30
updated: 2024-06-20T01:09
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

# 用法解析

在你提供的TypeScript代码中，`as` 关键字用于在映射类型中重新映射键。具体来说，它用于将原始类型的某个属性值作为新类型的键。这种用法在TypeScript中被称为 "键重映射"（key remapping）。

### 代码解释

让我们逐步解析代码，特别关注 `as` 关键字的使用。

```typescript
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
```

这里定义了一个联合类型 `Route`，它表示四种不同的路由，每种路由都有一个 `route` 属性和一个 `search` 属性。

```typescript
/**  
 * Here, R represents the individual Route. The lesson here * is that the thing we're iterating DOESN'T have to be a 
 * string | number | symbol, as long as the thing we cast it to 
 * is. 
 */
type RoutesObject = {  
  [R in Route as R["route"]]: R["search"];  
};
```

在这个部分，我们定义了一个映射类型 `RoutesObject`。这里的 `R` 代表 `Route` 联合类型中的每一个成员。

- `[R in Route]`：这是一个标准的映射类型语法，它遍历 `Route` 联合类型中的每一个成员。
- `as R["route"]`：这里的 `as` 关键字用于键重映射。它将原本的键（即 `R`）替换为 `R["route"]` 的值。换句话说，`R["route"]` 的值将成为新类型的键。
- `R["search"]`：这是新类型的值，它对应于 `R` 类型中的 `search` 属性。

通过这种方式，`RoutesObject` 类型将会如下所示：

```typescript
type RoutesObject = {  
  "/": {  
    page: string;  
    perPage: string;  
  };  
  "/about": {};  
  "/admin": {};  
  "/admin/users": {};  
};
```

每个键是 `route` 的值，而每个值是对应的 `search` 对象。

```typescript
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

最后，这里有一个类型测试，使用 `Expect` 和 `Equal` 来确保 `RoutesObject` 类型与预期的类型相等。如果类型匹配，测试将通过，否则会失败。

### 总结

在上述代码中，`as` 关键字用于将映射类型中的键重映射为 `R["route"]` 的值。这种用法在处理复杂类型转换时非常有用，特别是在需要根据某个属性的值来动态生成类型键的情况下。
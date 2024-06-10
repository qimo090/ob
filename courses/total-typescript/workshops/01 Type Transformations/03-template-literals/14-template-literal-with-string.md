---
tags:
  - TypeScript
  - TemplateLiteral
url: https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html
created: 2024-06-10T12:02
updated: 2024-06-10T12:06
---
# Problem

```ts file:14-template-literal-with-string.problem.ts
type Route = unknown;  
  
export const goToRoute = (route: Route) => {};  
  
// Should succeed:  
  
goToRoute("/users");  
goToRoute("/");  
goToRoute("/admin/users");  
  
// Should error:  
  
// @ts-expect-error  
goToRoute("users/1");  
// @ts-expect-error  
goToRoute("http://facebook.com");
```

# Solution

```ts file
type Route = `/${string}`;  
  
export const goToRoute = (route: Route) => {};  
  
// Should succeed:  
  
goToRoute("/users");  
goToRoute("/");  
goToRoute("/admin/users");  
  
// Should error:  
  
// @ts-expect-error  
goToRoute("users/1");  
// @ts-expect-error  
goToRoute("http://facebook.com");
```

# 解析

`Template Literal` 

文档：[https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html](https://www.typescriptlang.org/docs/handbook/2/template-literal-types.html)


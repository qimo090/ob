---
created: 2024-06-08T00:01
updated: 2024-06-08T00:14
---
# Problem

```ts file:Problem
/**  
 * It's important to understand the terminology around unions: * * One of the type declarations below is a union. * One of the type declarations below is a discriminated union. * One of the type declarations below is an enum. * * Which is which? */  
type A =  
  | {  
      type: "a";  
      a: string;  
    }  
  | {  
      type: "b";  
      b: string;  
    }  
  | {  
      type: "c";  
      c: string;  
    };  
  
type B = "a" | "b" | "c";  
  
enum C {  
  A = "a",  
  B = "b",  
  C = "c",  
}  
  
export {};
```

# Solution

# 解析

## `discriminated union` 判别联合类型

文档：[https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions)



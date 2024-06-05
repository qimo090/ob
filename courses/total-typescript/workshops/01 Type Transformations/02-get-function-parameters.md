---
created: 2024-06-03T22:54
updated: 2024-06-05T23:17
---
# Problem

```ts file:problem
import { Equal, Expect } from "../helpers/type-utils";  
  
const makeQuery = (  
  url: string,  
  opts?: {  
    method?: string;  
    headers?: {  
      [key: string]: string;  
    };  
    body?: string;  
  },  
) => {};  
  
type MakeQueryParameters = unknown;  
  
type tests = [
  Expect<  
    Equal<  
      MakeQueryParameters,  
      [  
        url: string,  
        opts?: {  
          method?: string;  
          headers?: {  
            [key: string]: string;  
          };  
          body?: string;  
        },  
      ]  
    >  >,  
];
```

# Solution

```ts file:solution fold
import { Equal, Expect } from "../helpers/type-utils";  
  
const makeQuery = (  
  url: string,  
  opts?: {  
    method?: string;  
    headers?: {  
      [key: string]: string;  
    };  
    body?: string;  
  },  
) => {};  
  
type MakeQueryParameters = Parameters<typeof makeQuery>;  
  
type tests = [  
  Expect<  
    Equal<  
      MakeQueryParameters,  
      [  
        url: string,  
        opts?: {  
          method?: string;  
          headers?: {  
            [key: string]: string;  
          };  
          body?: string;  
        },  
      ]  
    >  >,  
];
```

# 解析

`Parameters`

文档：[https://www.typescriptlang.org/docs/handbook/utility-types.html#parameterstype](https://www.typescriptlang.org/docs/handbook/utility-types.html#parameterstype)

`Parameters` 是 TypeScript 中的一个内置工具类型，用于提取函数类型的参数类型。它接收一个函数类型，并生成一个由该函数所有参数类型组成的元组类型。这对于处理和重用函数参数类型非常有用。下面是详细的介绍与使用示例。

### 基本用法

假设你有一个函数：
```ts
function exampleFunction(name: string, age: number): void {
  console.log(`Name: ${name}, Age: ${age}`); 
}
```
你可以使用 `Parameters` 提取这个函数的参数类型：
```ts
type UserParams = Parameters<typeof exampleFunction>;
// type UserParams = [name: string, age: number]
```
### 工作原理
`Parameters` 的定义如下：
```ts
type Parameters<T extends (...args: any) => any> = T extends (...args: infer P) => any ? P : never;
```

### 使用示例

#### 基本示例

假设有一个函数：

```typescript
function exampleFunction(name: string, age: number): void {
  console.log(`Name: ${name}, Age: ${age}`);
}
```

我们可以使用 `Parameters` 来提取 `exampleFunction` 的参数类型：

```typescript
type ExampleFunctionParams = Parameters<typeof exampleFunction>;
// ExampleFunctionParams 的类型为 [string, number]
```

#### 应用场景

1. **重用参数类型**：

当我们需要创建另一个函数，其参数与 `exampleFunction` 相同，可以使用 `Parameters` 来重用参数类型：

```typescript
function anotherFunction(...args: Parameters<typeof exampleFunction>): void {
  // 可以直接使用传入的参数
  exampleFunction(...args);
}
```

2. **结合其他类型工具**：

可以将 `Parameters` 与其他工具类型结合使用。例如，获取某个类中方法的参数类型：

```typescript
class MyClass {
  myMethod(a: number, b: string): void {}
}

type MyMethodParams = Parameters<MyClass['myMethod']>;
// MyMethodParams 的类型为 [number, string]
```

3. **创建类型安全的回调**：

使用 `Parameters` 可以确保回调函数的参数类型一致：

```typescript
function callWithExampleParams(callback: (...args: Parameters<typeof exampleFunction>) => void) {
  callback("John", 25);
}

callWithExampleParams((name, age) => {
  console.log(`Name: ${name}, Age: ${age}`);
});
```

### 总结

`Parameters` 是一个非常强大的工具类型，能够提高代码的类型安全性和可重用性。通过提取函数的参数类型并在不同的上下文中使用，可以有效减少重复代码，确保类型一致性。
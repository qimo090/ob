---
url: https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype
tags:
  - TypeScript
  - TypeScript/Awaited
created: 2024-06-05T22:56
updated: 2024-06-10T13:38
---
# Problem

```ts file:problem
import { Equal, Expect } from "../helpers/type-utils";  
  
const getUser = () => {  
  return Promise.resolve({  
    id: "123",  
    name: "John",  
    email: "john@example.com",  
  });  
};  
  
type ReturnValue = ReturnType<typeof getUser>;  
  
type tests = [  
  Expect<Equal<ReturnValue, { id: string; name: string; email: string }>>,  
];
```

# Solution

```ts file:solution fold
import { Equal, Expect } from '../helpers/type-utils'  
  
const getUser = () => {  
  return Promise.resolve({  
    id: '123',  
    name: 'John',  
    email: 'john@example.com',  
  })  
}  
  
type ReturnValue = Awaited<ReturnType<typeof getUser>>;  
  
type tests = [  
  Expect<Equal<ReturnValue, { id: string; name: string; email: string }>>,  
];
```

# 解析

 `Awaited`

文档：[https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype](https://www.typescriptlang.org/docs/handbook/utility-types.html#awaitedtype)

在 TypeScript 中，`Awaited` 是一个内置的条件类型，用于提取 `Promise` 对象的解析类型。它可以用于处理异步操作的返回值，特别是在处理 `async`/`await` 语法时非常有用。

> [!note]
> `Awaited` 会递归地解开 `Promise` 

### 语法

```typescript
type Awaited<T> = T extends null | undefined 
	? T 
	: T extends object & { then(onfulfilled: infer F, ...args: any): any } 
	? F extends (value: infer V, ...args: any) => any 
		? Awaited<V> 
		: never 
	: T;
```

这个类型定义看起来很复杂，但实际上它只是在检查 T 是否是一个 `Promise` 类型。如果是，它就会 ***递归*** 地解开 `Promise` 类型，直到获取到内部的值类型。
### 使用示例

假设我们有一个返回 `Promise` 的函数：

```typescript
async function fetchData(): Promise<string> {
  return "Hello, World!";
}
```

我们可以使用 `Awaited` 提取 `fetchData` 函数返回的 `Promise` 的解析类型：

```typescript
type Data = Awaited<ReturnType<typeof fetchData>>;
// Data 的类型是 string
```
### 示例代码

```typescript
async function exampleFunction(): Promise<number> {
  return 42;
}

type ExampleType = Awaited<ReturnType<typeof exampleFunction>>;
// ExampleType 的类型是 number

async function anotherFunction() {
  const result: ExampleType = await exampleFunction();
  console.log(result); // 42
}

anotherFunction();
```

在上面的示例中，`Awaited<ReturnType<typeof exampleFunction>>` 提取了 `exampleFunction` 返回的 `Promise` 的解析类型，并将其赋值给 `ExampleType`。这样，我们就可以在 `anotherFunction` 中使用 `ExampleType` 来确保 `await exampleFunction()` 返回值的类型正确。

Example

```ts
type A = Awaited<Promise<string>>;
// type A = string

type B = Awaited<Promise<Promise<number>>>;
// type B = number

type C = Awaited<boolean | Promise<number>>;
// type C = number | boolean
```

### 应用场景

1. **处理异步函数的返回类型**：当你需要获取异步函数的返回值类型时，`Awaited` 非常有用。
2. **类型推断**：在编写泛型函数或类型时，可以使用 `Awaited` 来推断异步操作的返回类型。
3. **类型安全**：确保在处理 `Promise` 时，能够正确地获取其解析值的类型，从而提高类型安全性。

总之，`Awaited` 是一个非常有用的工具类型，特别是在处理异步编程时，可以帮助我们更好地管理和使用 `Promise` 的解析类型。
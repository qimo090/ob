---
created: 2024-06-02T20:33
updated: 2024-06-05T23:17
tags:
  - TypeScript
  - ReturnType
  - UtilityTypes
---
# Problem

```ts file:problem
import { Equal, Expect } from "../helpers/type-utils";  
  
const myFunc = () => {  
  return "hello";  
};  
  
/**  
 * How do we extract MyFuncReturn from myFunc? 
 */
type MyFuncReturn = unknown;  
  
type tests = [Expect<Equal<MyFuncReturn, string>>];
```

# Solution

```ts file:solution fold 
import { Equal, Expect } from "../helpers/type-utils";  
  
const myFunc = () => {  
  return "hello";  
};  
  
/**  
 * How do we extract MyFuncReturn from myFunc? 
 */
type MyFuncReturn = ReturnType<typeof myFunc>;  
  
type tests = [Expect<Equal<MyFuncReturn, string>>];
```

# 解析

`ReturnType`

文档：[https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype](https://www.typescriptlang.org/docs/handbook/utility-types.html#returntypetype)

在TypeScript中，`ReturnType` 是一个内置的类型工具，用于提取函数的返回类型。它是一个条件类型，能够从一个函数类型中推断出其返回值的类型。这对于确保类型一致性和减少重复类型定义非常有用。

### 基本用法

假设你有一个函数：

```typescript
function getUser(id: number) {
  return { id, name: "Alice" };
}
```

你可以使用 `ReturnType` 提取这个函数的返回类型：

```typescript
type User = ReturnType<typeof getUser>;
// User 的类型是 { id: number; name: string; }
```

### 工作原理

`ReturnType` 的定义如下：

```typescript
type ReturnType<T extends (...args: any) => any> = T extends (...args: any) => infer R ? R : any;
```

- `T extends (...args: any) => any`：`T` 必须是一个函数类型。
- `T extends (...args: any) => infer R`：如果 `T` 是一个函数类型，那么推断其返回类型 `R`。
- `R`：如果推断成功，则返回 `R`，否则返回 `any`。

### 示例

以下是一些使用 `ReturnType` 的示例：

#### 示例1：简单函数

```typescript
function add(a: number, b: number): number {
  return a + b;
}

type AddReturnType = ReturnType<typeof add>;
// AddReturnType 的类型是 number
```

#### 示例2：异步函数

```typescript
async function fetchData(url: string): Promise<string> {
  const response = await fetch(url);
  return response.text();
}

type FetchDataReturnType = ReturnType<typeof fetchData>;
// FetchDataReturnType 的类型是 Promise<string>
```

#### 示例3：复杂对象返回类型

```typescript
function createUser(name: string, age: number) {
  return {
    name,
    age,
    createdAt: new Date(),
  };
}

type CreateUserReturnType = ReturnType<typeof createUser>;
// CreateUserReturnType 的类型是 { name: string; age: number; createdAt: Date; }
```

### 注意事项

1. **类型兼容性**：`ReturnType` 只能用于函数类型。如果你尝试使用非函数类型，会导致编译错误。
2. **泛型函数**：对于泛型函数，`ReturnType` 仍然可以正确推断返回类型，但需要注意泛型参数的具体类型。

### 总结

`ReturnType` 是一个强大的工具，能够自动提取函数的返回类型，确保类型一致性，减少重复代码。它在大型代码库中尤其有用，可以帮助你维护类型安全和简洁的代码结构。


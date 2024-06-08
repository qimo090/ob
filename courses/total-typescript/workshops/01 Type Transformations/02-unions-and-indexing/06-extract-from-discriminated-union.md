---
tags:
  - TypeScript
  - Extract
url: https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union
created: 2024-06-08T11:53
updated: 2024-06-08T13:02
---
# Problem

```ts file:problem
import { Equal, Expect } from "../helpers/type-utils";  
  
export type Event =  
  | {  
      type: "click";  
      event: MouseEvent;  
    }  
  | {  
      type: "focus";  
      event: FocusEvent;  
    }  
  | {  
      type: "keydown";  
      event: KeyboardEvent;  
    };  
  
type ClickEvent = unknown;  
  
type tests = [Expect<Equal<ClickEvent, { type: "click"; event: MouseEvent }>>];
```

# Solution

```ts file:solution fold
import { Equal, Expect } from "../helpers/type-utils";  
  
export type Event =  
  | {  
      type: "click";  
      event: MouseEvent;  
    }  
  | {  
      type: "focus";  
      event: FocusEvent;  
    }  
  | {  
      type: "keydown";  
      event: KeyboardEvent;  
    };  
  
type ClickEvent = Extract<Event, { type: 'click' }>;  
  
type tests = [Expect<Equal<ClickEvent, { type: "click"; event: MouseEvent }>>];
```

# 解析

`Extract` 

文档：[https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union](https://www.typescriptlang.org/docs/handbook/utility-types.html#extracttype-union)

`Extract` 是 TypeScript 中的一个条件类型，用于从联合类型中提取那些可以分配给某个类型的子类型。它是一个预定义的条件类型，通常用于类型转换和类型过滤。

### 基本语法

```ts
Extract<T, U>
```

- `T` ：联合类型
- `U` ：要提取的类型

`Extract` 的作用是从联合类型 `T` 中提取出所有可以分配给类型 `U` 的子类型。

### 示例代码

#### 1. 从联合类型中提取特定类型

假设我们有一个联合类型：

```ts
type UnionType = string | number | boolean;
```

我们可以使用 `Extract` 提取出所有的字符串类型：

```ts
type OnlyString = Extract<UnionType, string>;
// 结果是 string
```

#### 2. 提取特定接口类型

假设我们有一组接口和一个联合类型：

```ts
interface Cat {  
  kind: 'cat';  
  meow: () => void;  
}  
  
interface Dog {  
  kind: 'dog';  
  bark: () => void;  
}  
  
interface Bird {  
  kind: 'bird';  
  chirp: () => void;  
}  
  
type Animal = Cat | Dog | Bird;
```

我们可以使用 `Extract` 提取出所有的 `Dog` 类型

```ts
type OnlyDog = Extract<Animal, Dog>; // Dog
```

#### 3. 提取具有特定属性的类型

假设我们有一个联合类型，其中包含不同的对象类型：

```ts
type MixedType =  
  | { id: number; name: string }  
  | { id: string; age: number }  
  | { id: number; age: number };
```

我们可以使用 `Extract` 提取所有具有 `id: number` 属性的类型：

```ts
type WithNumberID = Extract<MixedType, { id: number }>; 
// 结果是 {id: number, name: string} | {id: number, age: number}
```

### 高级用法

#### 1. 与其他条件类型结合使用

`Extract` 可以与其他条件类型结合使用，以实现更复杂的类型操作：

```ts
type Primitive = string | number | boolean | null | undefined;  

type NonNullablePrimitive = Extract<Primitive, NonNullable<Primitive>>;
// 结果是 string | number | boolean
```

#### 2. 在泛型函数中使用

`Extract` 也可以在泛型函数中使用，已实现类型安全的类型过滤：

```ts
function extractType<T, U>(value: T): Extract<T, U> | unknown {  
  if (typeof value !== typeof (null as U)) {  
    return value as Extract<T, U>;  
  }  
  
  return undefined;
}  
  
const result = extractType<string | number | boolean, string>("hello");  
// 结果是 'hello'
```

### 总结

`Extract` 是 TypeScript 中一个非常有用的条件类型，它可以从联合类型中提取出特定的子类型。通过使用 `Extract`，我们可以实现类型过滤和类型转换，从而提高代码的类型安全性和可读性。

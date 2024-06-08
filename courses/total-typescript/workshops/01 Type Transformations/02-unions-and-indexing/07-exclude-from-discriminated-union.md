---
tags:
  - TypeScript
  - Exclude
url: https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers
created: 2024-06-08T20:22
updated: 2024-06-08T20:31
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
  
type NonKeyDownEvents = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      NonKeyDownEvents,  
      | { type: "click"; event: MouseEvent }  
      | { type: "focus"; event: FocusEvent }  
    >  
  >  
];
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
  
// type NonKeyDownEvents = Extract<Event, { type: 'click' } | { type: 'focus'}>;  
type NonKeyDownEvents = Exclude<Event, { type: "keydown" }>;  
  
type tests = [  
  Expect<  
    Equal<  
      NonKeyDownEvents,  
      | { type: "click"; event: MouseEvent }  
      | { type: "focus"; event: FocusEvent }  
    >  
  >  
];
```

# 解析

`Exclude` 

文档：[https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers](https://www.typescriptlang.org/docs/handbook/utility-types.html#excludeuniontype-excludedmembers)

`Exclude` 是 TypeScript 中的一个条件类型，用于从联合类型中排除那些可以分配给某个类型的子类型。它是一个预定义的条件类型，通常用于类型转换和类型过滤。

### 基本语法

```typescript
Exclude<T, U>
```

- `T`：联合类型。
- `U`：要排除的类型。

`Exclude` 的作用是从联合类型 `T` 中排除所有可以分配给类型 `U` 的子类型。

### 示例代码

#### 1. 从联合类型中排除特定类型

假设我们有一个联合类型：

```typescript
type UnionType = string | number | boolean;
```

我们可以使用 `Exclude` 排除所有的字符串类型：

```typescript
type WithoutString = Exclude<UnionType, string>; // 结果是 number | boolean
```

#### 2. 排除特定接口类型

假设我们有一组接口和一个联合类型：

```typescript
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

我们可以使用 `Exclude` 排除所有的 `Dog` 类型：

```typescript
type WithoutDog = Exclude<Animal, Dog>; // 结果是 Cat | Bird
```

#### 3. 排除具有特定属性的类型

假设我们有一个联合类型，其中包含不同的对象类型：

```typescript
type MixedType = { id: number; name: string } | { id: string; age: number } | { id: number; age: number };
```

我们可以使用 `Exclude` 排除所有具有 `id: number` 属性的类型：

```typescript
type WithoutNumberID = Exclude<MixedType, { id: number }>; // 结果是 { id: string; age: number }
```

### 高级用法

#### 1. 与其他条件类型结合使用

`Exclude` 可以与其他条件类型结合使用，以实现更复杂的类型操作：

```typescript
type Primitive = string | number | boolean | null | undefined;
type NonNullablePrimitive = Exclude<Primitive, null | undefined>; // 结果是 string | number | boolean
```

#### 2. 在泛型函数中使用

`Exclude` 也可以在泛型函数中使用，以实现类型安全的类型过滤：

```typescript
function excludeType<T, U>(value: T, typeCheck: (value: T) => value is U): Exclude<T, U> | undefined {
  if (!typeCheck(value)) {
    return value as Exclude<T, U>;
  }
  return undefined;
}

// 使用示例
const isString = (value: any): value is string => typeof value === 'string';

const result = excludeType<string | number | boolean, string>('hello', isString); // 结果是 undefined
const result2 = excludeType<string | number | boolean, string>(42, isString); // 结果是 42
```

### 详细解析

1. **类型谓词**：
   - 我们引入了一个类型谓词函数 `typeCheck`，它接受一个值并返回一个布尔值，以判断该值是否为特定类型。类型谓词函数的签名是 `(value: T) => value is U`。

2. **类型检查**：
   - 在 `excludeType` 函数中，我们使用 `typeCheck` 函数来检查 `value` 是否为类型 `U`。如果不是，则将 `value` 转换为 `Exclude<T, U>` 类型并返回；否则返回 `undefined`。

### 使用示例

我们可以定义不同的类型谓词函数来检查不同的类型：

```typescript
const isString = (value: any): value is string => typeof value === 'string';
const isNumber = (value: any): value is number => typeof value === 'number';

const result1 = excludeType<string | number | boolean, string>('hello', isString); // 结果是 undefined
const result2 = excludeType<string | number | boolean, string>(42, isString); // 结果是 42

const result3 = excludeType<string | number | boolean, number>(42, isNumber); // 结果是 undefined
const result4 = excludeType<string | number | boolean, number>('hello', isNumber); // 结果是 'hello'
```

### 总结

`Exclude` 是 TypeScript 中一个非常有用的条件类型，它可以从联合类型中排除特定的子类型。通过使用 `Exclude`，我们可以实现类型过滤和类型转换，从而提高代码的类型安全性和可读性。

如果你有更多关于 `Exclude` 或其他 TypeScript 的问题，请随时提问！
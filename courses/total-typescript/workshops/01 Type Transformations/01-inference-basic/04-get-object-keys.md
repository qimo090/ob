---
tags:
  - TypeScript
  - TypeScript/KeyOf
url: https://www.typescriptlang.org/docs/handbook/2/keyof-types.html
created: 2024-06-05T23:13
updated: 2024-06-10T13:38
---
# Problem

```ts file:problem 
import { Equal, Expect } from "../helpers/type-utils";  
  
const testingFrameworks = {  
  vitest: {  
    label: "Vitest",  
  },  
  jest: {  
    label: "Jest",  
  },  
  mocha: {  
    label: "Mocha",  
  },  
};  
  
type TestingFramework = unknown;  
  
type tests = [Expect<Equal<TestingFramework, "vitest" | "jest" | "mocha">>];
```

# Solution

```ts file:solution fold
import { Equal, Expect } from "../helpers/type-utils";  
  
const testingFrameworks = {  
  vitest: {  
    label: "Vitest",  
  },  
  jest: {  
    label: "Jest",  
  },  
  mocha: {  
    label: "Mocha",  
  },  
};  
  
type TestingFramework = keyof typeof testingFrameworks;  
  
type tests = [Expect<Equal<TestingFramework, "vitest" | "jest" | "mocha">>];
```

# 解析

`KeyOf`

文档：[https://www.typescriptlang.org/docs/handbook/2/keyof-types.html](https://www.typescriptlang.org/docs/handbook/2/keyof-types.html)

`keyof` 是 TypeScript 中的一个类型操作符，用于获取某个类型的所有键（key）的联合类型。它通常与泛型和映射类型一起使用，可以帮助我们在类型层面上进行更精细的控制和操作。

### 基本用法

假设我们有一个接口：

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}
```

使用 `keyof`，我们可以得到 `Person` 类型的所有键的联合类型：

```typescript
type PersonKeys = keyof Person; // "name" | "age" | "address"
```

### 示例代码

下面是一些使用 `keyof` 的常见场景和示例代码：

#### 1. 获取对象的键

```typescript
interface Person {
  name: string;
  age: number;
  address: string;
}

type PersonKeys = keyof Person; // "name" | "age" | "address"

const key: PersonKeys = "name"; // 这是合法的
// const invalidKey: PersonKeys = "phone"; // 这是非法的，会报错
```

#### 2. 泛型约束

我们可以使用 `keyof` 来约束泛型参数，使其只能是某个对象类型的键：

```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}

const person: Person = {
  name: "John",
  age: 30,
  address: "123 Main St",
};

const name = getProperty(person, "name"); // 返回类型是 string
const age = getProperty(person, "age"); // 返回类型是 number
// const invalid = getProperty(person, "phone"); // 这是非法的，会报错
```

#### 3. 映射类型

`keyof` 通常与映射类型一起使用，来创建新的类型：

```typescript
type ReadonlyPerson = {
  readonly [K in keyof Person]: Person[K];
};

const readonlyPerson: ReadonlyPerson = {
  name: "John",
  age: 30,
  address: "123 Main St",
};

// readonlyPerson.name = "Doe"; // 这是非法的，因为属性是只读的
```

### 总结

`keyof` 是 TypeScript 中一个非常强大的工具，可以帮助我们在类型层面上进行更精细的控制。它可以用于获取类型的键的联合类型，约束泛型参数，以及创建映射类型。通过这些功能，我们可以编写出更安全、可维护的代码。

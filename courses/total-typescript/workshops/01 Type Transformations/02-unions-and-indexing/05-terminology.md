---
tags:
  - TypeScript
  - TypeScript/DiscriminatedUnions
url: https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions
created: 2024-06-08T00:01
updated: 2024-06-10T13:39
---
```ts
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

# 解析

## `discriminated union` 判别联合类型

文档：[https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions](https://www.typescriptlang.org/docs/handbook/typescript-in-5-minutes-func.html#discriminated-unions)

`Discriminated Unions` （判别联合类型）是 TypeScript 中的一种高级类型模式，用于处理多个可能类型的联合类型。它通过每个类型中添加一个公共的、具有不同值的属性（称为判别联合属性）来区分不同的类型，从而实现类型安全的类型检查和类型推断。

### 基本概念

判别联合类型通常由以下三个部分组成：

1. **判别属性**：一个公共的属性，每个类型都有这个属性，但值不同。
2. **联合类型**：包含所有可能类型的联合类型。
3. **类型保护**：通过检查判别属性来缩小类型范围。

### 示例代码

假设我们有一个表示不同形状（圆形、矩形）的联合类型：

```ts file:Shape
interface Circle {  
  kind: 'circle'; // 判别属性  
  radius: number;  
}  
  
interface Rectangle {  
  kind: 'rectangle'; // 判别属性  
  width: number;  
  height: number;  
}  
  
type Shape = Circle | Rectangle;
```

### 使用判别联合类型

我们可以通过判别属性来区分不同的类型，并在类型保护中使用它们：

```ts
function getArea (shape: Shape) {  
  switch (shape.kind) {  
    case 'circle':  
      return Math.PI * shape.radius ** 2  
    case 'rectangle':  
      return shape.width * shape.height  
    default:  
      // 如果我们处理了所有可能的情况，这里就不会执行  
      throw new Error('Unknown shape')  
  }}  
  
// 使用示例  
const myCircle: Circle = { kind: 'circle', radius: 10 }  
const myRectangle: Rectangle = { kind: 'rectangle', width: 10, height: 20 }  
  
console.log(getArea(myCircle)) // 314.1592653589793  
console.log(getArea(myRectangle)) // 200
```

### 类型保护

在上面的示例中，`switch` 语句中的每个 `case` 分支都根据判别属性 `kind` 的值来缩小类型范围。这使得 TypeScript 能够在每个分支中正确推断类型，并提供相应的类型检查和代码补全。

### 使用 `in` 操作符

除了 `switch` 语句，我们还可以使用 `in` 操作符来进行类型保护。

```ts
function getArea (shape: Shape) {  
  if ('radius' in shape) {  
    return Math.PI * shape.radius ** 2  
  } else {  
    return shape.width * shape.height  
  }  
}
```

### 完整性检查

TypeScript 还可以通过 `never` 类型来确保我们处理了所有可能的类型：

```ts
function getArea (shape: Shape) {  
  switch (shape.kind) {  
    case 'circle':  
      return Math.PI * shape.radius ** 2  
    case 'rectangle':  
      return shape.width * shape.height  
    default:  
      // 这里的 shape 应该是 never 类型，如果我们处理了所有可能的类型  
      const _exhaustiveCheck: never = shape  
      return _exhaustiveCheck  
  }  
}
```

### 总结

`Discriminated Unions` 是 TypeScript 中处理多种可能类型的强大工具。通过判别属性和类型保护，我们可以在联合类型实现类型安全的类型检查和类型推断。这不仅提高了代码的可读性和可维护性，还减少了运行时错误的可能性。

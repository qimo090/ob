---
tags:
  - JavaScript
  - JavaScript/Array
url: https://www.30secondsofcode.org/js/s/combine-object-arrays/
created: 2024-03-31T21:25
updated: 2024-06-10T13:43
---
你是否曾经需要组合两个对象数组？也许每个对象都包含有关同一对象的部分信息，并且你希望将它们合并到一个数组中。那么你会怎么做呢？

假设你知道唯一标识每个对象的key，则可以使用 [`Object.values()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values) 和展开运算符 ( [`...`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) ) 来获取两个数组中的所有对象。然后，你可以使用 [`Array.prototype.reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) 根据指定的键组合它们。

对于数组中的每个值，你可以检查该对象是否具有指定的键。如果是，你可以将其添加到累加器对象中，并将其与具有相同键的任何现有对象组合。这将为键属性的每个唯一值生成一个对象。

```js
const combine = (a, b, prop) =>
  Object.values(
    [...a, ...b].reduce((acc, v) => {
      if (v[prop])
        acc[v[prop]] = acc[v[prop]]
          ? { ...acc[v[prop]], ...v }
          : { ...v };
      return acc;
    }, {})
  );

const x = [
  { id: 1, name: 'John' },
  { id: 2, name: 'Maria' }
];
const y = [
  { id: 1, age: 28 },
  { id: 3, age: 26 },
  { age: 3}
];
combine(x, y, 'id');
// [
//  { id: 1, name: 'John', age: 28 },
//  { id: 2, name: 'Maria' },
//  { id: 3, age: 26 }
// ]
```

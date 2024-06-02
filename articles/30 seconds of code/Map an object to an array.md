# Map an object to an array

Tags: Array, JavaScript, Object
URL: https://www.30secondsofcode.org/js/s/listify
Source: 30 seconds of code
Created: July 8, 2023 9:48 AM
Last edited time: July 8, 2023 9:48 AM

Maps an object to an object array, using the provided mapping function.

- Use `Object.entries()` to get an array of the object's key-value pairs.
- Use `Array.prototype.reduce()` to map the array to an object.
- Use `mapFn` to map the keys and values of the object and `Array.prototype.push()` to add the mapped values to the array.

```jsx
const listify = (obj, mapFn) =>
  Object.entries(obj).reduce((acc, [key, value]) => {
    acc.push(mapFn(key, value));
    return acc;
  }, []);
```

```jsx
const people = { John: { age: 42 }, Adam: { age: 39 } };
listify(people, (key, value) => ({ name: key, ...value }));
// [ { name: 'John', age: 42 }, { name: 'Adam', age: 39 } ]
```

---

```jsx
/**
 * @desc Map an object to an array
 * @see https://www.30secondsofcode.org/js/s/listify
 */

// const people = { John: { age: 42 }, Adam: { age: 39 } };
// =>
// [ { name: 'John', age: 42 }, { name: 'Adam', age: 39 } ]

const listify = (obj, mapFn) =>
  Object.entries(obj).reduce((acc, [key, value]) => {
    acc.push(mapFn(key, value));
    return acc;
  }, []);

export default listify;
```

```jsx
import listify from "./listify";

test("listify normal", () => {
  const people = { John: { age: 42 }, Adam: { age: 39 } };
  const result = [
    { name: "John", age: 42 },
    { name: "Adam", age: 39 },
  ];

  expect(listify(people, (key, value) => ({ name: key, ...value }))).toEqual(
    result
  );
});
```
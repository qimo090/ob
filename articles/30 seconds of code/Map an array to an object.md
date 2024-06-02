# Map an array to an object

Tags: Array, JavaScript, Object
URL: https://www.30secondsofcode.org/js/s/objectify
Source: 30 seconds of code
Created: July 8, 2023 9:48 AM
Last edited time: July 8, 2023 9:48 AM

Maps an object array to an object, using the provided mapping functions.

- Use `Array.prototype.reduce()` to map the array to an object.
- Use `mapKey` to map the keys of the object and `mapValue` to map the values.

```jsx
const objectify = (arr, mapKey, mapValue = i => i) =>
  arr.reduce((acc, item) => {
    acc[mapKey(item)] = mapValue(item);
    return acc;
  }, {});
```

```jsx
const people = [ { name: 'John', age: 42 }, { name: 'Adam', age: 39 } ];
objectify(people, p => p.name.toLowerCase());
// { john: { name: 'John', age: 42 }, adam: { name: 'Adam', age: 39 } }
objectify(
  people,
  p => p.name.toLowerCase(),
  p => p.age
);
// { john: 42, adam: 39 }
```

---

```jsx
/**
 * Map an array to an object
 * @see https://www.30secondsofcode.org/js/s/objectify
 */
// const people = [ { name: "John", age: 42 }, { name: "Adam", age: 39 }, ];
//  + objectify(people, (p) => p.name.toLowerCase());
// => { john: { name: 'John', age: 42 }, adam: { name: 'Adam', age: 39 } }

// const people = [ { name: "John", age: 42 }, { name: "Adam", age: 39 }, ];
// + objectify( people, (p) => p.name.toLowerCase(), (p) => p.age);
// => { john: 42, adam: 39 }

const objectify = (arr, mapKey, mapValue = (i) => i) =>
  arr.reduce(
    (acc, cur) => ({
      ...acc,
      [mapKey(cur)]: mapValue(cur),
    }),
    {}
  );

export default objectify;
```

```jsx
import objectify from "./objectify";

describe("objectify", () => {
  test("only mapKey", () => {
    const people = [
      { name: "John", age: 42 },
      { name: "Adam", age: 39 },
    ];
    const result = objectify(people, (p) => p.name.toLowerCase());
    const target = {
      john: { name: "John", age: 42 },
      adam: { name: "Adam", age: 39 },
    };
    expect(result).toEqual(target);
  });

  test("mapKey and mapValue", () => {
    const people = [
      { name: "John", age: 42 },
      { name: "Adam", age: 39 },
    ];
    const result = objectify(
      people,
      (p) => p.name.toLowerCase(),
      (p) => p.age
    );
    const target = { john: 42, adam: 39 };
    expect(result).toEqual(target);
  });
});
```
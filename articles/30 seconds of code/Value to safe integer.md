---
tags:
  - JavaScript
  - Math
url: https://www.30secondsofcode.org/js/s/to-safe-integer
source: 30 seconds of code
created: 2023-07-08T09:48:00
updated: 2024-05-31T22:50
---
[Number.MIN_SAFE_INTEGER - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MIN_SAFE_INTEGER)

[Number.MAX_SAFE_INTEGER - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number/MAX_SAFE_INTEGER)

Converts a value to a safe integer.

- Use `Math.max()` and `Math.min()` to find the closest safe value.
- Use `Math.round()` to convert to an integer.

```jsx
const toSafeInteger = num =>
  Math.round(
    Math.max(Math.min(num, Number.MAX_SAFE_INTEGER), Number.MIN_SAFE_INTEGER)
  );
```

```jsx
toSafeInteger('3.2'); // 3
toSafeInteger(Infinity); // 9007199254740991
```

---

```jsx
const toSafeInteger = (num) =>
  Math.round(
    Math.max(Math.min(num, Number.MAX_SAFE_INTEGER), Number.MIN_SAFE_INTEGER)
  );

export default toSafeInteger; 
```

```jsx
import toSafeInteger from "./toSafeInteger";

describe("Value to safe integer", () => {
  test("normal", () => {
    expect(toSafeInteger("3.2")).toBe(3);
  });

  test("special Infinity", () => {
    expect(toSafeInteger(Infinity)).toBe(9007199254740991);
    expect(toSafeInteger(Infinity)).toBe(Number.MAX_SAFE_INTEGER);
    expect(toSafeInteger(Infinity)).toBe(Math.pow(2, 53) - 1);
  });
});
```
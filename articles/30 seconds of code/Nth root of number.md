# Nth root of number

Tags: JavaScript, Math
URL: https://www.30secondsofcode.org/js/s/nth-root
Source: 30 seconds of code
Created: July 8, 2023 9:48 AM
Last edited time: July 8, 2023 9:48 AM

[Math.pow() - JavaScript | MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/pow)

Calculates the nth root of a given number.

- Use `[Math.pow()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math/pow)` to calculate `x` to the power of `1 / n` which is equal to the nth root of `x`.

```jsx
const nthRoot = (x, n) => Math.pow(x, 1 / n);
```

```jsx
nthRoot(32, 5); // 2
```
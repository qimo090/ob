# Number is power of two

Tags: JavaScript, Math
Source: 30 seconds of code
Created: July 8, 2023 9:48 AM
Last edited time: July 8, 2023 9:48 AM

> 计算是否是 2 的乘方
> 

[按位与（&） - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Bitwise_AND)

Checks if the given number is a power of `2`.

- Use the bitwise binary AND operator (`&`) to determine if `n` is a power of `2`.
- Additionally, check that `n` is not falsy.

```jsx
const isPowerOfTwo = n => !!n && (n & (n - 1)) == 0;
```

```jsx
isPowerOfTwo(0); // false
isPowerOfTwo(1); // true
isPowerOfTwo(8); // true
```
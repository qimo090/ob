# Radians to degrees

Tags: JavaScript, Math
URL: https://www.30secondsofcode.org/js/s/rads-to-degrees
Source: 30 seconds of code
Created: July 8, 2023 9:48 AM
Last edited time: July 8, 2023 9:48 AM

弧度转换成度，π 弧度 = 180 度

$1rad × 180/π = 57.296°$

$πrad × 180/π = 180°$

```jsx
const radsToDegrees = rad => (rad * 180.0) / Math.PI;
```

```jsx
radsToDegrees(Math.PI / 2); // 90
```
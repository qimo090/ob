---
tags:
  - TypeScript
  - KeyOf
created: 2024-06-05T23:13
updated: 2024-06-05T23:19
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


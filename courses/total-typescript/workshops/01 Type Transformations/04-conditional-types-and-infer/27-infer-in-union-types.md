---
created: 2024-06-12T23:09
updated: 2024-06-12T23:14
tags:
  - TypeScript
  - TypeScript/Infer
  - TypeScript/UnionType
---
# Problem

```ts file:27-infer-in-union-types.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
const parser1 = {  
  parse: () => 1,  
};  
  
const parser2 = () => "123";  
  
const parser3 = {  
  extract: () => true,  
};  
  
type GetParserResult<T> = unknown;  
  
type tests = [  
  Expect<Equal<GetParserResult<typeof parser1>, number>>,  
  Expect<Equal<GetParserResult<typeof parser2>, string>>,  
  Expect<Equal<GetParserResult<typeof parser3>, boolean>>,  
];
```

# Solution

```ts file:27-infer-in-union-types.solution.1.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
const parser1 = {  
  parse: () => 1,  
};  
  
const parser2 = () => "123";  
  
const parser3 = {  
  extract: () => true,  
};  
  
type GetParserResult<T> = T extends {  
  parse: () => infer TResult;  
}  
  ? TResult  
  : T extends () => infer TResult  
  ? TResult  
  : T extends {  
      extract: () => infer TResult;  
    }  
  ? TResult  
  : never;  
  
type tests = [  
  Expect<Equal<GetParserResult<typeof parser1>, number>>,  
  Expect<Equal<GetParserResult<typeof parser2>, string>>,  
  Expect<Equal<GetParserResult<typeof parser3>, boolean>>,  
];
```

```ts file:27-infer-in-union-types.solution.2.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
const parser1 = {  
  parse: () => 1,  
};  
  
const parser2 = () => "123";  
  
const parser3 = {  
  extract: () => true,  
};  
  
type GetParserResult<T> = T extends  
  | {  
      parse: () => infer TResult;  
    }  
  | {  
      extract: () => infer TResult;  
    }  
  | (() => infer TResult)  
  ? TResult  
  : never;  
  
type tests = [  
  Expect<Equal<GetParserResult<typeof parser1>, number>>,  
  Expect<Equal<GetParserResult<typeof parser2>, string>>,  
  Expect<Equal<GetParserResult<typeof parser3>, boolean>>,  
];
```
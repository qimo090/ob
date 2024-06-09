---
created: 2024-06-09T22:37
updated: 2024-06-09T22:39
---
# Problem

```ts file:problem
import { Equal, Expect } from "../helpers/type-utils";  
  
export const fakeDataDefaults = {  
  String: "Default string",  
  Int: 1,  
  Float: 1.14,  
  Boolean: true,  
  ID: "id",  
};  
  
export type StringType = unknown;  
export type IntType = unknown;  
export type FloatType = unknown;  
export type BooleanType = unknown;  
export type IDType = unknown;  
  
type tests = [  
  Expect<Equal<StringType, string>>,  
  Expect<Equal<IntType, number>>,  
  Expect<Equal<FloatType, number>>,  
  Expect<Equal<BooleanType, boolean>>,  
  Expect<Equal<IDType, string>>,  
];
```

# Solution

```ts file:solution fold
import { Equal, Expect } from "../helpers/type-utils";  
  
export const fakeDataDefaults = {  
  String: "Default string",  
  Int: 1,  
  Float: 1.14,  
  Boolean: true,  
  ID: "id",  
};  
  
type FakeDataDefaults = typeof fakeDataDefaults;  
  
export type StringType = FakeDataDefaults["String"];  
export type IntType = FakeDataDefaults["Int"];  
export type FloatType = FakeDataDefaults["Float"];  
export type BooleanType = FakeDataDefaults["Boolean"];  
export type IDType = FakeDataDefaults["ID"];  
  
type tests = [  
  Expect<Equal<StringType, string>>,  
  Expect<Equal<IntType, number>>,  
  Expect<Equal<FloatType, number>>,  
  Expect<Equal<BooleanType, boolean>>,  
  Expect<Equal<IDType, string>>  
];
```
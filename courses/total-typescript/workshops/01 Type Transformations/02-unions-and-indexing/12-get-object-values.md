---
created: 2024-06-10T11:01
updated: 2024-06-10T11:03
---
# Problem

```ts file:12-get-object-values.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
const frontendToBackendEnumMap = {  
  singleModule: "SINGLE_MODULE",  
  multiModule: "MULTI_MODULE",  
  sharedModule: "SHARED_MODULE",  
} as const;  
  
type BackendModuleEnum = unknown;  
  
type tests = [  
  Expect<  
    Equal<BackendModuleEnum, "SINGLE_MODULE" | "MULTI_MODULE" | "SHARED_MODULE">  
  >,  
];
```

# Solution

```ts file:12-get-object-values.solution.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
const frontendToBackendEnumMap = {  
  singleModule: "SINGLE_MODULE",  
  multiModule: "MULTI_MODULE",  
  sharedModule: "SHARED_MODULE",  
} as const;  
  
type BackendModuleEnum = typeof frontendToBackendEnumMap[keyof typeof frontendToBackendEnumMap]  
  
type tests = [  
  Expect<  
    Equal<BackendModuleEnum, "SINGLE_MODULE" | "MULTI_MODULE" | "SHARED_MODULE">  
  >,  
];
```
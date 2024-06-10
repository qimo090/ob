---
created: 2024-06-10T10:36
updated: 2024-06-10T11:01
---
# Problem

```ts file:problem
import { Equal, Expect } from "../helpers/type-utils";  
  
export const programModeEnumMap = {  
  GROUP: "group",  
  ANNOUNCEMENT: "announcement",  
  ONE_ON_ONE: "1on1",  
  SELF_DIRECTED: "selfDirected",  
  PLANNED_ONE_ON_ONE: "planned1on1",  
  PLANNED_SELF_DIRECTED: "plannedSelfDirected",  
} as const;  
  
export type IndividualProgram = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      IndividualProgram,  
      "1on1" | "selfDirected" | "planned1on1" | "plannedSelfDirected"  
    >  
  >,  
];
```

# Solution

```ts file:solution1 fold
import { Equal, Expect } from "../helpers/type-utils";  
  
export const programModeEnumMap = {  
  GROUP: "group",  
  ANNOUNCEMENT: "announcement",  
  ONE_ON_ONE: "1on1",  
  SELF_DIRECTED: "selfDirected",  
  PLANNED_ONE_ON_ONE: "planned1on1",  
  PLANNED_SELF_DIRECTED: "plannedSelfDirected",  
} as const;  
  
export type IndividualProgram = typeof programModeEnumMap[  
  | "ONE_ON_ONE"  
  | "SELF_DIRECTED"  
  | "PLANNED_ONE_ON_ONE"  
  | "PLANNED_SELF_DIRECTED"];  
  
type tests = [  
  Expect<  
    Equal<  
      IndividualProgram,  
      "1on1" | "selfDirected" | "planned1on1" | "plannedSelfDirected"  
    >  
  >,  
];
```

```ts fild:solution2 fold
import { Equal, Expect } from "../helpers/type-utils";  
  
export const programModeEnumMap = {  
  GROUP: "group",  
  ANNOUNCEMENT: "announcement",  
  ONE_ON_ONE: "1on1",  
  SELF_DIRECTED: "selfDirected",  
  PLANNED_ONE_ON_ONE: "planned1on1",  
  PLANNED_SELF_DIRECTED: "plannedSelfDirected",  
} as const;  
  
export type IndividualProgram = typeof programModeEnumMap[Exclude<  
  keyof typeof programModeEnumMap,  
  "GROUP" | "ANNOUNCEMENT"  
>];  
  
type tests = [  
  Expect<  
    Equal<  
      IndividualProgram,  
      "1on1" | "selfDirected" | "planned1on1" | "plannedSelfDirected"  
    >  
  >,  
];
```


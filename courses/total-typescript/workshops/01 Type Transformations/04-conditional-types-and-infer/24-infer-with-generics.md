---
created: 2024-06-12T22:43
updated: 2024-06-12T22:49
tags:
  - TypeScript
  - TypeScript/Infer
url: https://www.typescriptlang.org/docs/handbook/2/conditional-types.html#inferring-within-conditional-types
---
# Problem

```ts file:24-infer-with-generics.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
interface MyComplexInterface<Event, Context, Name, Point> {  
  getEvent: () => Event;  
  getContext: () => Context;  
  getName: () => Name;  
  getPoint: () => Point;  
}  
  
type Example = MyComplexInterface<  
  "click",  
  "window",  
  "my-event",  
  { x: 12; y: 14 }  
>;  
  
type GetPoint<T> = unknown;  
  
type tests = [Expect<Equal<GetPoint<Example>, { x: 12; y: 14 }>>];
```

# Solution

```ts file:24-infer-with-generics.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
interface MyComplexInterface<Event, Context, Name, Point> {  
  getEvent: () => Event;  
  getContext: () => Context;  
  getName: () => Name;  
  getPoint: () => Point;  
}  
  
type Example = MyComplexInterface<  
  "click",  
  "window",  
  "my-event",  
  { x: 12; y: 14 }  
>;  
  
type GetPoint<T> = T extends MyComplexInterface<any, any, any, infer TPoint>  
  ? TPoint  
  : never;  
  
type tests = [Expect<Equal<GetPoint<Example>, { x: 12; y: 14 }>>];
```
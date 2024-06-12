---
created: 2024-06-12T22:49
updated: 2024-06-12T22:53
---
# Problem

```ts file:25-template-literal-value-extraction.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type Names = [  
  "Matt Pocock",  
  "Jimi Hendrix",  
  "Eric Clapton",  
  "John Mayer",  
  "BB King",  
];  
  
type GetSurname<T> = unknown;  
  
type tests = [  
  Expect<Equal<GetSurname<Names[0]>, "Pocock">>,  
  Expect<Equal<GetSurname<Names[1]>, "Hendrix">>,  
  Expect<Equal<GetSurname<Names[2]>, "Clapton">>,  
  Expect<Equal<GetSurname<Names[3]>, "Mayer">>,  
  Expect<Equal<GetSurname<Names[4]>, "King">>,  
];
```

# Solution

```ts file:25-template-literal-value-extraction.solution.1.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type Names = [  
  "Matt Pocock",  
  "Jimi Hendrix",  
  "Eric Clapton",  
  "John Mayer",  
  "BB King",  
];  
  
type GetSurname<T> = T extends `${infer First} ${infer Last}` ? Last : never;  
  
type tests = [  
  Expect<Equal<GetSurname<Names[0]>, "Pocock">>,  
  Expect<Equal<GetSurname<Names[1]>, "Hendrix">>,  
  Expect<Equal<GetSurname<Names[2]>, "Clapton">>,  
  Expect<Equal<GetSurname<Names[3]>, "Mayer">>,  
  Expect<Equal<GetSurname<Names[4]>, "King">>,  
];
```

```ts file:25-template-literal-value-extraction.solution.2.ts
import { S } from "ts-toolbelt";  
import { Equal, Expect } from "../helpers/type-utils";  
  
type Names = [  
  "Matt Pocock",  
  "Jimi Hendrix",  
  "Eric Clapton",  
  "John Mayer",  
  "BB King",  
];  
  
/**  
 * This is an alternative way of doing it, using S.Split 
 */
type GetSurname<T extends string> = S.Split<T, " ">[1];  
  
type tests = [  
  Expect<Equal<GetSurname<Names[0]>, "Pocock">>,  
  Expect<Equal<GetSurname<Names[1]>, "Hendrix">>,  
  Expect<Equal<GetSurname<Names[2]>, "Clapton">>,  
  Expect<Equal<GetSurname<Names[3]>, "Mayer">>,  
  Expect<Equal<GetSurname<Names[4]>, "King">>,  
];
```

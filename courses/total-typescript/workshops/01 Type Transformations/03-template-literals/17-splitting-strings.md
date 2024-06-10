---
created: 2024-06-10T12:36
updated: 2024-06-10T12:40
---
# Problem

```ts file:17-splitting-strings.problem.ts
// Might come in handy!  
// import { S } from "ts-toolbelt";  
// https://millsp.github.io/ts-toolbelt/modules/string_split.html  
  
import { Equal, Expect } from "../helpers/type-utils";  
  
type Path = "Users/John/Documents/notes.txt";  
  
type SplitPath = unknown;  
  
type tests = [  
  Expect<Equal<SplitPath, ["Users", "John", "Documents", "notes.txt"]>>,  
];
```

# Solution

```ts file:17-splitting-strings.solution.ts fold
// Might come in handy!  
import { S } from "ts-toolbelt";  
// https://millsp.github.io/ts-toolbelt/modules/string_split.html  
  
import { Equal, Expect } from "../helpers/type-utils";  
  
type Path = "Users/John/Documents/notes.txt";  
  
type SplitPath = S.Split<Path, "/">;  
  
type tests = [  
  Expect<Equal<SplitPath, ["Users", "John", "Documents", "notes.txt"]>>  
];
```
---
created: 2024-06-10T12:41
updated: 2024-06-10T13:41
tags:
  - TypeScript
  - TypeScript/TemplateLiteral
  - TypeScript/Record
---
# Problem

```ts file:18-template-literals-in-object-keys.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
type TemplateLiteralKey = `${"user" | "post" | "comment"}${"Id" | "Name"}`;  
  
type ObjectOfKeys = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      ObjectOfKeys,  
      {  
        userId: string;  
        userName: string;  
        postId: string;  
        postName: string;  
        commentId: string;  
        commentName: string;  
      }  
    >  
  >,  
];
```

# Solution

```ts file:18-template-literals-in-object-keys.solution.ts fold
import { Equal, Expect } from "../helpers/type-utils";  
  
type TemplateLiteralKey = `${"user" | "post" | "comment"}${"Id" | "Name"}`;  
  
type ObjectOfKeys = Record<TemplateLiteralKey, string>;  
  
type tests = [  
  Expect<  
    Equal<  
      ObjectOfKeys,  
      {  
        userId: string;  
        userName: string;  
        postId: string;  
        postName: string;  
        commentId: string;  
        commentName: string;  
      }  
    >  
  >,  
];
```


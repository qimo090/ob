---
created: 2024-06-09T22:40
updated: 2024-06-09T22:41
---
# Problem

```ts file:problem
import { Equal, Expect } from "../helpers/type-utils";  
  
export type Event =  
  | {  
      type: "click";  
      event: MouseEvent;  
    }  
  | {  
      type: "focus";  
      event: FocusEvent;  
    }  
  | {  
      type: "keydown";  
      event: KeyboardEvent;  
    };  
  
type EventType = unknown;  
  
type tests = [Expect<Equal<EventType, "click" | "focus" | "keydown">>];
```

# Solution

```ts file:solution fold
import { Equal, Expect } from "../helpers/type-utils";  
  
export type Event =  
  | {  
      type: "click";  
      event: MouseEvent;  
    }  
  | {  
      type: "focus";  
      event: FocusEvent;  
    }  
  | {  
      type: "keydown";  
      event: KeyboardEvent;  
    };  
  
type EventType = Event["type"];  
  
type tests = [Expect<Equal<EventType, "click" | "focus" | "keydown">>];
```
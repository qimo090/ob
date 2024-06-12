---
created: 2024-06-12T22:58
updated: 2024-06-12T22:59
---
# Problem

```ts file:26-get-result-from-async-function.problem.ts
import { Equal, Expect } from "../helpers/type-utils";  
  
const getServerSideProps = async () => {  
  const data = await fetch("https://jsonplaceholder.typicode.com/todos/1");  
  const json: { title: string } = await data.json();  
  return {  
    props: {  
      json,  
    },  
  };  
};  
  
type InferPropsFromServerSideFunction = unknown;  
  
type tests = [  
  Expect<  
    Equal<  
      InferPropsFromServerSideFunction<typeof getServerSideProps>,  
      { json: { title: string } }  
    >  
  >  
];
```

# Solution

```ts
```
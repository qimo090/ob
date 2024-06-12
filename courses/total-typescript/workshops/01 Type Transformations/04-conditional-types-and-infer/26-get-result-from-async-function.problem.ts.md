---
created: 2024-06-12T22:58
updated: 2024-06-12T23:09
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

```ts file:26-get-result-from-async-function.solution.ts fold
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
  
type InferPropsFromServerSideFunction<T> = T extends () => Promise<{  
  props: infer P;  
}>  
  ? P  
  : never;  
  
type tests = [  
  Expect<  
    Equal<  
      InferPropsFromServerSideFunction<typeof getServerSideProps>,  
      { json: { title: string } }  
    >  
  >  
];
```
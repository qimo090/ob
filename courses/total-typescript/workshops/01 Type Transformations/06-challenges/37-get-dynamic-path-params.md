---
created: 2024-06-19T00:01
updated: 2024-06-19T00:04
---
# Problem

```ts file:
import { Equal, Expect } from "../helpers/type-utils";

type UserPath = "/users/:id";

type UserOrganisationPath = "/users/:id/organisations/:organisationId";

type ExtractPathParams = unknown;

type tests = [
  Expect<Equal<ExtractPathParams<UserPath>, { id: string }>>,
  Expect<
    Equal<
      ExtractPathParams<UserOrganisationPath>,
      { id: string; organisationId: string }
    >
  >,
];
```

# Solution

```ts file:37-get-dynamic-path-params.solution.ts fold
```
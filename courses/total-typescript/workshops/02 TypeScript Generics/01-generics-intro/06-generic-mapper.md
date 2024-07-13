---
created: 2024-07-13T11:06
updated: 2024-07-13T11:07
---
# Problem

```ts file:06-generic-mapper.problem.ts
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

export const concatenateFirstNameAndLastName = (user: unknown) => {
  return {
    ...user,
    fullName: `${user.firstName} ${user.lastName}`,
  };
};

it("Should add fullName to an object which only contains firstName and lastName", () => {
  const users = [
    {
      firstName: "Matt",
      lastName: "Pocock",
    },
  ];

  const newUsers = users.map(concatenateFirstNameAndLastName);

  expect(newUsers).toEqual([
    {
      firstName: "Matt",
      lastName: "Pocock",
      fullName: "Matt Pocock",
    },
  ]);

  type tests = [
    Expect<
      Equal<
        typeof newUsers,
        Array<{ firstName: string; lastName: string } & { fullName: string }>
      >
    >,
  ];
});

it("Should retain other properties passed in", () => {
  const users = [
    {
      id: 1,
      firstName: "Matt",
      lastName: "Pocock",
    },
  ];

  const newUsers = users.map(concatenateFirstNameAndLastName);

  expect(newUsers).toEqual([
    {
      id: 1,
      firstName: "Matt",
      lastName: "Pocock",
      fullName: "Matt Pocock",
    },
  ]);

  type tests = [
    Expect<
      Equal<
        typeof newUsers,
        Array<
          { id: number; firstName: string; lastName: string } & {
            fullName: string;
          }
        >
      >
    >,
  ];
});

it("Should fail when the object passed in does not contain firstName", () => {
  const users = [
    {
      firstName: "Matt",
    },
  ];

  const newUsers = users.map(
    // @ts-expect-error
    concatenateFirstNameAndLastName,
  );
});
```

# Solution

```ts file:06-generic-mapper.solution.ts fold
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

export const concatenateFirstNameAndLastName = <
  T extends { firstName: string; lastName: string },
>(
  user: T,
) => {
  return {
    ...user,
    fullName: `${user.firstName} ${user.lastName}`,
  };
};

it("Should add fullName to an object which only contains firstName and lastName", () => {
  const users = [
    {
      firstName: "Matt",
      lastName: "Pocock",
    },
  ];

  const newUsers = users.map(concatenateFirstNameAndLastName);

  expect(newUsers).toEqual([
    {
      firstName: "Matt",
      lastName: "Pocock",
      fullName: "Matt Pocock",
    },
  ]);

  type tests = [
    Expect<
      Equal<
        typeof newUsers,
        Array<{ firstName: string; lastName: string } & { fullName: string }>
      >
    >,
  ];
});

it("Should retain other properties passed in", () => {
  const users = [
    {
      id: 1,
      firstName: "Matt",
      lastName: "Pocock",
    },
  ];

  const newUsers = users.map(concatenateFirstNameAndLastName);

  expect(newUsers).toEqual([
    {
      id: 1,
      firstName: "Matt",
      lastName: "Pocock",
      fullName: "Matt Pocock",
    },
  ]);

  type tests = [
    Expect<
      Equal<
        typeof newUsers,
        Array<
          { id: number; firstName: string; lastName: string } & {
            fullName: string;
          }
        >
      >
    >,
  ];
});

it("Should fail when the object passed in does not contain firstName", () => {
  const users = [
    {
      firstName: "Matt",
    },
  ];

  const newUsers = users.map(
    // @ts-expect-error
    concatenateFirstNameAndLastName,
  );
});
```
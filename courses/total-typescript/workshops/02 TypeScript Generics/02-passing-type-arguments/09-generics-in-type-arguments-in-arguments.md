---
created: 2024-07-13T15:08
updated: 2024-07-13T21:34
---
# Problem

```ts file:09-generics-in-type-arguments-in-arguments.problem.ts
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

export class Component<TProps> {
  private props: TProps;

  constructor(props: TProps) {
    this.props = props;
  }

  getProps = () => this.props;
}

const cloneComponent = (component: unknown) => {
  return new Component(component.getProps());
};

it("Should clone the props from a passed-in Component", () => {
  const component = new Component({ a: 1, b: 2, c: 3 });

  const clonedComponent = cloneComponent(component);

  const result = clonedComponent.getProps();

  expect(result).toEqual({ a: 1, b: 2, c: 3 });

  type tests = [
    Expect<Equal<typeof result, { a: number; b: number; c: number }>>
  ];
});
```

# Solution

```ts file:09-generics-in-type-arguments-in-arguments.solution.ts fold
import { expect, it } from "vitest";
import { Equal, Expect } from "../helpers/type-utils";

export class Component<TProps> {
  private props: TProps;

  constructor(props: TProps) {
    this.props = props;
  }

  getProps = () => this.props;
}

const cloneComponent = <TProps>(component: Component<TProps>) => {
  return new Component(component.getProps());
};

it("Should clone the props from a passed-in Component", () => {
  const component = new Component({ a: 1, b: 2, c: 3 });

  const clonedComponent = cloneComponent(component);

  const result = clonedComponent.getProps();

  expect(result).toEqual({ a: 1, b: 2, c: 3 });

  type tests = [
    Expect<Equal<typeof result, { a: number; b: number; c: number }>>,
  ];
});
```
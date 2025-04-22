# Code Style

## React & TypeScript files

### 1. Imports order

```js
// Third-party libraries
import React from "react";

// Internal libraries and modules (with absolute path)
import { Button } from "@yandex-fleet/ui";

// Files within module (with relative path)
import Component from "./Component";
// Style sheets
import styles from "./styles.module.css";
```

### 2. Naming Convention

#### Export default

Prefer naming default exports. It helps when you’re reading an error stack trace and using the React Dev Tools.

```js
// bad
export default () => <form>...</form>

// good
export default function Form() {
  return <form>...</form>
}
```

#### Function arguments

Use one-letter variables only in simple cases:

```js
return strings.map((s) => s.trim());
```

For other cases use meaningful names:

```js
cars.map((car) => {
  const vehicleNumber = car.getVehicleNumber().toLowerCase();
  return vehicleNumber;
});
```

Do not use `_` for variables that are actually used.

#### Tanker keys

Use `.` separator for entities/features and `_` separator as a spacing analog.

```
feed.title
feed.search_results.refetch
summary.events_statistics.title
summary.fetch
summary.refetch
```

### 3. Interfaces vs. Type Aliases

Prefer Type Aliases over Interfaces.

### 4. Inline types vs. Type Aliases

Prefer inlining props types rather than writing type aliases. Use type aliases in case you want to reexport them.

```js
// acceptable
type Props = {
  name: string,
};

const Component = (props: Props) => {};

// best
const Component = ({ name }: { name: string }) => {};

// best
export type TableProps<D extends Record<string, unknown>> = {
  id: string;
  columns: D[];
}
```

### 5. Destructuring

Prefer props destructuring in function signature over accessing object properties.

```js
// bad
const Component = (props: { name: string, age: number }) => {
  const { name, age } = props;
  return (
    <>
      <span>{name}</span>
      <span>{age}</span>
    </>
  );
};

// acceptable
const Component = (props: { name: string, age: number }) => {
  return (
    <>
      <span>{props.name}</span>
      <span>{props.age}</span>
    </>
  );
};

// best
const Component = ({ name, age }: { name: string, age: number }) => {
  return (
    <>
      <span>{name}</span>
      <span>{age}</span>
    </>
  );
};
```

### 6. Avoid excessive nesting

Keep structure simple and avoid nesting components inside each other and inside extra folders (like components, `EditPage`, etc.).

### 7. Don't optimize prematurely

Avoid wrapping eveything in `useMemo`, `useCallback` and `React.memo`. Consider reading this article [When to useMemo and useCallback](https://kentcdodds.com/blog/usememo-and-usecallback).

### 8. Prefer named exports

We used to opt for default exports throughout the code base, especially for React components. In new code base, named exports is the preferred way of exporting entities of any kind.

```js
// acceptable
export default function Component() {}

// best decision in new packages
export const Component = () => {};
```

### 9. Prefer kebab-case in file and directory naming

```shell
# deprecated, acceptable for existing code
EditPage.tsx
urlHandler.ts

# preferable
edit-page.tsx
handler.ts
```

### 10. Prefer naming modules as namespaces

Modules are meant to group the code and as such should be given a name reflecting the common purpose of the code within.
As an added benefit a common name is usually shorter than the specific one.

```shell
# bad
use-item-styles.ts
use-data.ts
use-match-link.ts

# good
item-styles.ts
data.ts
link.ts
```

## CSS

We are generally following [Committee requirements](https://clubs.at.yandex-team.ru/verstka/5322).

### 1. Use variables for spacings

Prefer using variables for spacings, you can find them in the `@yandex-fleet/yandex-go/src/Theme/theme-root.css` file.

### 2. Use theme colors

We care about dark theme interfaces therefore prefer using theme colors rather than palette.

### 3. Check caniuse

We support all browsers with more than 0.2% users so be aware of using new css features.

### 4. Support rtl-interfaces

Use `useDir` or rtl-related css features (ex. `direction`, `margin-inline`, etc.) to make our interfaces comfortable in rtl.

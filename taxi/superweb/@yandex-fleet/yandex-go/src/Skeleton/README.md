# Skeleton

Serves as a content placeholder when data for a component is not immediately available.

For example, `Skeleton` can be used as a `fallback` prop for `React.Suspense`:

```tsx
import React from "react";
import { Skeleton } from "@yandex-fleet/yandex-go";

import PendingTodos from "./PendingTodos";

const Pending = () => {
  return (
    <React.Suspense fallback={<Skeleton width={200} height={200} />}>
      <PendingTodos />
    </React.Suspense>
  );
};
```

## Size

Size of `Skeleton` can be configured in several ways:

- by a `className` prop, declaring `width` and `height` in the provided CSS class
- by a `style` prop, providing `width` and `height` values in a styles object
- by `width` and `height` props
- by dimensions of the provided `children` prop.

### Inferring Skeleton size from `children`

If you don't want to declare `Skeleton`'s `width` and `height` explicitly, you can pass
`children` prop and `Skeleton` will automatically inherit their dimensions.

> NOTE: `children` passed to `Skeleton` component will have `visibility: hidden` style,
> so would not be visible on the screen.

```tsx
import React from "react";
import { Skeleton } from "@yandex-fleet/yandex-go";

const SkeletonWithInferedDimensions = () => {
  return (
    <Skeleton shape="circle">
      <div style={{ width: 40, height: 40 }} />
    </Skeleton>
  );
};
```

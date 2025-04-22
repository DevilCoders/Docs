# Dropdown Component

## Usages

- [Default](#default)
- [Close when you click on an item](#close-when-you-click-on-an-item)

### Default

```typescript jsx
import React from "react";
import { Dropdown } from "@yandex-fleet/yandex-go";

const MyComponentWithDropdown = () => {
  return <Dropdown target={<button>click</button>}>something</Dropdown>;
};
```

### Close when you click on an item

theme can be: normal, action

```typescript jsx
import React from "react";
import { Dropdown } from "@yandex-fleet/yandex-go";

const MyComponentWithThemeButton = () => {
  return (
    <Dropdown target={<button>click</button>}>
      {({ hide }) => <button onClick={hide}>something</button>}
    </Dropdown>
  );
};
```

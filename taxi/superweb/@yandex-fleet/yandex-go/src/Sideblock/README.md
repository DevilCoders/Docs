# Sideblock

Taken the @yandex-int/edu-components/Sideblock component as the basis - [documentation](https://lego.yandex-team.ru/components/?storybook=%2Fdocsx%2Fedu-components-sideblock--default)

## Usages

- [Default](#default)

### Default

```typescript jsx
import React, { useState } from "react";
import { Sideblock } from "@yandex-fleet/yandex-go";

const MyComponent = () => {
  const [visible, setVisible] = useState(false);

  return (
    <Sideblock
      hasBlockingBackground
      theme="normal"
      visible={visible}
      onOutsideClick={() => setVisible(false)}
      onEscapeKeyDown={() => setVisible(false)}
    >
      <div style={{ width: 500 }}>content</div>
    </Sideblock>
  );
};

export default MyComponent;
```

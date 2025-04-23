# Button Component

Taken the @yandex-lego/components/Icon component as the basis - [documentation](https://lego-docs.s3.mds.yandex.net/story/dev/index.html?path=/docsx/lego-components-icon--playground)

## Usages

- [With Arrow](#with-arrow)
- [With Cross](#with-cross)
- [With Color](#with-color)
- [With custom image](#with-custom-image)

### With Arrow

```typescript jsx
import React from "react";
import Icon from "../Icon";

const MyComponentWithArrowIcon = () => {
  return (
    <Icon
      size="m"
      glyph="type-arrow"
      direction="bottom" // left | top | right | bottom
    />
  );
};
```

### With Cross

```typescript jsx
import React from "react";
import Icon from "../Icon";

const MyComponentWithCrossIcon = () => {
  return <Icon size="m" glyph="type-cross" />;
};
```

### With Color

```typescript jsx
import React from "react";
import Icon from "../Icon";

const MyComponentWithColorIcon = () => {
  return <Icon size="m" glyph="type-cross" color="#ffb833" />;
};
```

### With custom image

- [More about url](https://lego-docs.s3.mds.yandex.net/story/dev/index.html?path=/docsx/lego-components-icon-desktop--url#%D1%81%D0%BE%D0%B1%D1%81%D1%82%D0%B2%D0%B5%D0%BD%D0%BD%D0%B0%D1%8F-%D0%B8%D0%BA%D0%BE%D0%BD%D0%BA%D0%B0)

```typescript jsx
import React from "react";
import Icon from "./Icon";

const MyComponentWithIcon = () => {
  return (
    <Icon
      style={{ width: 20, height: 20 }}
      url="https://yastatic.net/lego/_/Kx6F6RQnQFitm0qRxX7vpvfP0K0.png"
    />
  );
};
```

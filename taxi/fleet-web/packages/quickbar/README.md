# `@yandex-fleet/quickbar`

Quickbar component

## Usage

```tsx
// MyApp.tsx
import React from "react";
import { QuickbarContextProvider } from "@yandex-fleet/quickbar-context";
import Quickbar from "@yandex-fleet/quickbar";

export const MyApp = () => {
  return (
    <QuickbarContextProvider>
      <Quickbar />
      <Section />
    </QuickbarContextProvider>
  );
};
```

```tsx
// Section.tsx
import React, { useContext } from "react";
import { QuickbarContext } from "@yandex-fleet/quickbar-context";

export const Section = () => {
  const { openQuickbar } = useContext(QuickbarContext);

  const onClick = () => {
    openQuickbar({
      content: {
        type: "predefined",
        content: "newIssue",
      },
    });
  };

  return (
    <div>
      <button type="button" onClick={onClick}>
        Create New Issue
      </button>
    </div>
  );
};
```

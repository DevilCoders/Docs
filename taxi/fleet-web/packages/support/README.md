# @yandex-fleet/support

Support section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const Support = lazy(() => import("@yandex-fleet/support"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Support />} />
      </Routes>
    </Router>
  );
};
```

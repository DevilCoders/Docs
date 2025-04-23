# @yandex-fleet/api-keys

API Keys section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const ApiKeys = lazy(() => import("@yandex-fleet/api-keys"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<ApiKeys />} />
      </Routes>
    </Router>
  );
};
```

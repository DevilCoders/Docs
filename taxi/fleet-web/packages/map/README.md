# @yandex-fleet/map

Map section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const Map = lazy(() => import("@yandex-fleet/map"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Map />} />
      </Routes>
    </Router>
  );
};
```

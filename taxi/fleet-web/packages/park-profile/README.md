# @yandex-fleet/park-profile

Park profile section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const ParkProfile = lazy(() => import("@yandex-fleet/park-profile"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<ParkProfile />} />
      </Routes>
    </Router>
  );
};
```

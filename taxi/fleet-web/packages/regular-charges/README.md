# @yandex-fleet/regular-charges

Regular charges section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const RegularCharges = lazy(() => import("@yandex-fleet/regular-charges"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<RegularCharges />} />
      </Routes>
    </Router>
  );
};
```

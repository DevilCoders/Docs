# @yandex-fleet/payouts

payouts section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const Payouts = lazy(() => import("@yandex-fleet/payouts"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Payouts />} />
      </Routes>
    </Router>
  );
};
```

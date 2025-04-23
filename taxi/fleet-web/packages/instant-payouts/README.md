# @yandex-fleet/instant-payouts

Instant payouts section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const InstantPayouts = lazy(() => import("@yandex-fleet/instant-payouts"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<InstantPayouts />} />
      </Routes>
    </Router>
  );
};
```

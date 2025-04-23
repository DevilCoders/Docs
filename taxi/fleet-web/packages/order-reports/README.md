# @yandex-fleet/order-reports

Order reports section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const OrderReports = lazy(() => import("@yandex-fleet/order-reports"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<OrderReports />} />
      </Routes>
    </Router>
  );
};
```

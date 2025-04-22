# @yandex-fleet/transaction-reports

Transaction reports section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const TransactionReports = lazy(
  () => import("@yandex-fleet/transaction-reports")
);

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<TransactionReports />} />
      </Routes>
    </Router>
  );
};
```

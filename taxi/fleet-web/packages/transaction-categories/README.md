# @yandex-fleet/transaction-categories

Transaction categories section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const TransactionCategories = lazy(
  () => import("@yandex-fleet/transaction-categories")
);

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<TransactionCategories />} />
      </Routes>
    </Router>
  );
};
```

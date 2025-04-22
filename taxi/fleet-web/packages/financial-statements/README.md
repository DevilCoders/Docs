# @yandex-fleet/financial-statements

Financial statements section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const FinancialStatements = lazy(
  () => import("@yandex-fleet/financial-statements")
);

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<FinancialStatements />} />
      </Routes>
    </Router>
  );
};
```

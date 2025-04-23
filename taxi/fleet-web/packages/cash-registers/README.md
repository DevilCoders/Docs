# @yandex-fleet/cash-registers

Online cash registers integration section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const CashRegisters = lazy(() => import("@yandex-fleet/cash-registers"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<CashRegisters />} />
      </Routes>
    </Router>
  );
};
```

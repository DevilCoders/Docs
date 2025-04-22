# @yandex-fleet/quality-reports

Quality reports section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const QualityReports = lazy(() => import("@yandex-fleet/quality-reports"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<QualityReports />} />
      </Routes>
    </Router>
  );
};
```

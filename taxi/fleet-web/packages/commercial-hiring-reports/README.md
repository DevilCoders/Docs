# @yandex-fleet/commercial-hiring-reports

Commercial hiring reports section

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const CommercialHiringReports = lazy(
  () => import("@yandex-fleet/commercial-hiring-reports")
);

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<CommercialHiringReports />} />
      </Routes>
    </Router>
  );
};
```

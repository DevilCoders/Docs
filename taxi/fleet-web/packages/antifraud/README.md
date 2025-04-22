# @yandex-fleet/antifraud

Antifraud settings section
https://st.yandex-team.ru/FLEETWEB-2032

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const AntiFraud = lazy(() => import("@yandex-fleet/antifraud"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<AntiFraud />} />
      </Routes>
    </Router>
  );
};
```

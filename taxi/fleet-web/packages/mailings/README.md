# @yandex-fleet/mailings

Mailings section

## Usage

```tsx
import React, { lazy } from "react";
import { Router, Routes, Route } from "@yandex-fleet/router";
const Mailings = lazy(() => import("@yandex-fleet/mailings"));
const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<Mailings />} />
      </Routes>
    </Router>
  );
};
```

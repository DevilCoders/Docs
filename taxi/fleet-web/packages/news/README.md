# @yandex-fleet/news

News section

You can create and and edit news at https://tariff-editor.taxi.tst.yandex-team.ru/news-dispa

## Usage

```tsx
import React, { lazy } from "react";

import { Router, Routes, Route } from "@yandex-fleet/router";

const News = lazy(() => import("@yandex-fleet/news"));

const App = () => {
  return (
    <Router>
      <Routes>
        <Route path="/" element={<News />} />
      </Routes>
    </Router>
  );
};
```

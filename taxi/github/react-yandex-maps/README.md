# @yandex-fleet/react-yandex-maps

Yet another React wrapper for the Yandex.Maps API

## Features

- React [Suspense](https://reactjs.org/docs/concurrent-mode-suspense.html) support
- Yandex Maps API loading is controlled by the library, no need for manual `<script>` injection
- language, mode and other Yandex.Maps API parameters are controlled via `YandexMaps` component props
- Interaction with Yandex.Maps API via React hooks

## Usage

```tsx
import React from 'react';
import { YandexMaps, Language, Map, Version, useMap } from 'react-yandex-maps';

function MyMap() {
  return (
    // Every prop except `apikey` reloads the Yandex Maps API
    // and re-renders the subtree of YandexMaps component
    <YandexMaps
      apikey='your API key'
      lang='en_US'
      version={Version.Dev}
      mode='release'
    >
      <Map
        state={{
          center: [55.7158, 37.5692],
          zoom: 10,
          type: 'yandex#map',
        }}
      >
        some map-related or arbitrary content here
      </Map>
    </YandexMaps>
  );
}
```

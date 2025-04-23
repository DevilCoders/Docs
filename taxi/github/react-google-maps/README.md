# @yandex-fleet/react-google-maps

Yet another React bindings for the Google Maps API

## Usage

Install the package with NPM

```bash
npm i --registry http://npm.yandex-team.ru --save @yandex-fleet/react-google-maps
```

or Yarn

```bash
yarn add @yandex-fleet/react-google-maps
```

Add Google map to your app

```tsx
import React from 'react';
import {
  GoogleMaps,
  Map,
  Marker,
  OverlayView,
} from '@yandex-fleet/react-google-maps';

export default function App() {
  return (
    <React.Suspense fallback={<span>Loading Google Maps...</span>}>
      <GoogleMaps apikey='YOUR_API_KEY' suspense>
        <Map
          center={{ lat: 55.7522, lng: 37.6156 }}
          zoom={10}
          style={{ width: '100vw', height: '100vh' }}
        >
          <Marker position={{ lat: 55.7, lng: 37.6 }} />
          <OverlayView
            mapPaneName='markerLayer'
            position={{ lat: 55.7, lng: 37.5 }}
          >
            <div>Custom DOM node</div>
          </OverlayView>
        </Map>
      </GoogleMaps>
    </React.Suspense>
  );
}
```

## Development

Clone and install dependencies

```
git clone git@github.yandex-team.ru:taxi/react-google-maps.git
cd react-google-maps
npm i
```

Create `.env` with Google Maps API Key

```
APIKEY=<Your API Key>
```

Run Storybook and open <http://localhost:9009/>

```
npm run start-storybook
```

## Publishing

To publish the package, create `.env` file in the root of the repo with `GH_TOKEN` and `NPM_TOKEN` variables declared.
These variables will allow `semantic-release` to authorize to your GitHub and NPM accounts while publishing.

To publish a new version, just run

```bash
npm run publish
```

The package will then be published to NPM and new release will be added to GitHub.

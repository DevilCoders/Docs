> Note: Maps provider is defined based on TLD (top level domain).
> You can force the usage Yandex Maps by editing `getComponents()` in the [src/lib/getMapComponents.tsx](https://github.yandex-team.ru/B2BGeo/frontend/blob/master/projects/mvrp-map/src/lib/getMapComponents.tsx) file or `getTld()` in the [src/lib/tld.ts](https://github.yandex-team.ru/B2BGeo/frontend/blob/master/projects/mvrp-map/src/lib/tld.ts) file.

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Quick start
1. `npm install`
This install all packages and create SSL_CRT_FILE and SSL_KEY_FILE from magicdev
2. `npm run start:ru` (or `npm run start:com`)
3. The app is running on https://localhost.msup.yandex.ru:8082/courier/mvrp-map (https://localhost.msup.yandex.com:8082/courier/mvrp-map)

## Tests
This project uses e2e tests via [cypress](https://docs.cypress.io). See additional information about test [here](https://a.yandex-team.ru/arc_vcs/maps/b2bgeo/frontend/projects/mvrp-map/e2e-tests/readme.md).

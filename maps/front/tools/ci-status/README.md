# CI status for commit in trunk

Chrome extension to view CI statuses new commits on "History" tab of Arcanum.

This extension load last 50 task for `trunk` on `/maps/front/`.

## How to install

1. Download latest [packed extension](https://sandbox.yandex-team.ru/resources?any_attr=false&owner=MAPS_FRONT&state=READY&limit=20&offset=0&attrs=%7B%22ext%22%3A%22ci-status%22%2C%22project%22%3A%22maps-front-maps%22%7D): `ya download --output ci-status.crx sbr:<ID>`.
2. Open `chrome://extensions`.
3. Drag and drop file `ci-status.crx`.

## Developing

1. `nvm use`.
1. `npm run build -- --watch`.
1. Open `chrome://extensions` and load folder `./extension` via "Load unpacked extension".

## Release new version

1. `npm version patch` (or `minor`/`major`)
1. `npm run release`

# express-http-geobase

[![](https://drone.yandex-team.ru/api/badges/toolbox/express-http-geobase/status.svg)](https://drone.yandex-team.ru/toolbox/express-http-geobase)
![](https://badger.yandex-team.ru/npm/express-http-geobase/version.svg)
![](https://badger.yandex-team.ru/npm/express-http-geobase/owner.svg)
[![OKO health](https://oko.yandex-team.ru/badges/repo.svg?repoName=frontend/packages/express-http-geobase&vcs=arc)](https://oko.yandex-team.ru/repo/toolbox/express-http-geobase)

Express middleware for node-http-geobase

## Install
```
npm install -S express-http-geobase
```

## Usage
```
app.use(require('express-http-geobase')(opts));

app.get('/', function (req, res) {
    console.log(req.geolocation.region_id);
    console.log(req.geolocation.parents);
});
```
Since `yandex_gid` cookie is used, please ensure use of cookie-parser.

`req.geolocation` object is provided by this middleware. Basically it is the result of `HttpGeobase.prototype.pinpointGeolocation` method call
with the following additional fields:

- `parents` - result of `HttpGeobase.prototype.parents` method call
- `traits` - result of `HttpGeobase.prototype.traitsByIp` method call (requires `traits: true` option)

and optional fields (if an error occurred)
- `isError` - boolean
- `errors` - an object with error details

If geolocation request has failed, host-based fallback values are provided (see `fallback.js` for details).

## Notes
WARNING: `is_trusted` parameter of `pinpoint_geolocation` geobase method is set to `true`. This was made intentionally to support old nodejs
binding `region` method behaviour. This allows to provide compatibility and seamless migration.

## Supported options
- `server` - http-geobase server hostname or IP address (default: geobase.qloud.yandex.ru)
- `traits` - if `true`, adds information about user ip (see [traitsByIp](https://github.yandex-team.ru/toolbox/node-http-geobase#geobasetraitsbyipip-opts))
- `clientOptions` - http-geobase options. See [node-http-geobase documentation](https://github.yandex-team.ru/floatdrop/node-http-geobase) for details.

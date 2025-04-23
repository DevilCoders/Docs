## Local development

```bash
make deps       # install dependencies
make dev.setup  # setup local development (`rm -rf .dev` or it subdirs at any time)
make dev        # start dev server

make dev.tunneler
```

## Test

```bash
make test

make test filter=src/traffic    # filter testfiles by prefix
make test log=1                 # print browser console to stdout
make test debug='mocks:*'       # grep util.debug in *.test.js or look at console output in /tests/index.html
```

Each testfile is being ran in it's own isolated phantom.js process.

For faster development run `make dev` and open `/tests/index.html?filter=src/traffic/*&debug=*` in your browser.

## Release

**NOTE**: jsapi is not using semver, because it's older than semver. Debian-like versioning scheme is used instead.
```
  2  .  1  . 79  -  42
epoch.major.minor-patch
```

```bash
# Create branch to bump version
arc checkout -b jsapi-version-bump
# Bump version, commit and tag (`make version.minor` will bump 2.1.79->2.1.80 and you'll need to create feature branch)
make version.patch

arc pr create --push --publish
# Ship & merge
arc checkout trunk


# Release testing
npx qtools release testing -- --build-arg STATIC_CLIENT_KEY --build-arg QTOOLS_TOKEN
# Release production
npx qtools deploy production

# Manually build, push and deploy
npx qtools build -- --build-arg STATIC_CLIENT_KEY --build-arg QTOOLS_TOKEN
npx qtools push
npx qtools deploy testing
```

## AWACS

- [front-jsapi.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-jsapi.slb.maps.yandex.net/upstreams/list?filter=%7B%22idRegexp%22:%22v2-1%22%7D)
- [front-jsapi.tst.slb.maps.yandex.net](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/front-jsapi.tst.slb.maps.yandex.net/upstreams/list?filter=%7B%22idRegexp%22:%22v2-1%22%7D)

#### In manual mode

##### Prerequisites

Install docker [https://www.docker.com/get-started](https://www.docker.com/get-started).

Get qtools token. Use this [instruction](https://github.yandex-team.ru/mapsapi/jsapi-v2/blob/2.1.69/CONTRIBUTION.md#actual-version) as a guidance.

Login into docker registry using this [instruction](https://wiki.yandex-team.ru/qloud/docker-registry/#cli).

##### Build & push

If you want to build and push image to the registry by hand (which is highly discouraged) you can do it by executing following steps:

1. Perform all steps from [Build and push docker image to the registry](./CONTRIBUTION.md#build-and-push-docker-image-to-the-registry).

2. Execute command:

```bash
make docker-build-push
```
Note: During docker-build we are pushing static files to MDS S3 storage. `podrick-int` endpoint is used for that.
This endpoint require authorization via secret key, which could be found at https://yav.yandex-team.ru/secret/sec-01cjz2vkw9hqhf3c7skw5g4zxt/, and should be provided via env variable `STATIC_CLIENT_KEY`.

##### Troubleshooting

If you see errors like this one:
```
Err http://dist.yandex.ru stable/all/ Release.gpg
  Could not resolve 'dist.yandex.ru'
```

it might mean that container does not have network. You can try fix this by adding --network host to docker build options:
```
$(npm bin)/qtools build -- --network host
```

### Using local API on external websites with `mitmproxy`

Prerequisites (once)
1. Install and setup [mitmproxy](https://mitmproxy.org/).
2. Install certificate via http://mitm.it/.
3. Setup proxy in your browser (use FoxyProxy)

Run
```sh
mitmproxy --ssl-insecure -s tools/mitmproxy/spoof.py --set jsapi="https://$USER.api-maps.dev.yandex.net:8080/"
```

## Frontend

### Images

Images are located in `images/` directory.
All paths in ym.modules.importImages and styl/css files are considered to be relative to it.
E.g.:

```css
background-image: url('traffic/green.svg'); // Means images/traffic/green.svg
```

In `js` module:
```
var images = ym.modules.importImages({
    'green.svg': {
        src: 'traffic/green.svg' // Means images/traffic/green.svg
    }
});
```

### Distribution
There are 2 phases in api startup process:
1. `init.js`

    User The first script that user gets when requesting js api is `init.js`.
    Server takes `build/(release|debug)/init.js` file, and modifies it's code so that the function `ymapsInit` is called with set of server-side generated parameters.
    `init.js` contains module system, promise polyfills, initialization logic. See `builder/init.js`.

2. `init.js` fetches static bundle
    There are prebuild bundles, that contains set of modules + list of modules that are missing in this bundle. `full` bundle contains all existing modules. Bundles are stored in `build/(debug|release)`. There is `build/(debug|release)/bundles.json` which contains each bundle's url. It allows to change bundle location (e.g. to some static file storage).

    1. Module system loads initial bundle, that is provided in `load` query parameter as `package.<bundle_name>`. If no bundle is provided. `full` bundle is loaded. Technically bundle name is extracted on server side, and passed to `ymapsInit`.
    2. If requested module is missing in initial bundle, then full bundle is loaded.

    If you want to add bundle you should:
      1. Create <bundle_name>.json in builder/bundles folder with list of all modules (and all dependencies). If some dependency is missing, full.js will be loaded instantly after your bundle.
      2. [Optional] Make package.<bundle_name> module, which defines what shall be exposed on namespace, after bundle loading.
      3. Adjust server code, to correctly recognize your bundle and set `env.preload.bundle` parameter correctly.

## Oldie how to
If you want to change 2.1.oldie code then you need to follow these steps:
1. `arc checkout releases/maps-front/jsapi-v2-1/2.1.oldie`
2. `cd path_to_arcadia/maps/front/quarantine/jsapi-v2.1`
3. Create new branch, add files, commits as usual.
4. `arc pr create --push --no-edit --to releases/maps-front/jsapi-v2-1/2.1.oldie`

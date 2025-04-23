# Tickenator's backend

## Building from sources
```bash
export ARCADIA_ROOT=%SOME_VALID_PATH%

cd "${ARCADIA_ROOT}"

ya make -j0 --checkout search/mon/tickenator

cd search/mon/tickenator && ya tool horadric && ya make -r
```

### Run serval

[DEV SERVAL DOCS](https://a.yandex-team.ru/arc/trunk/arcadia/search/horadric2/doc/local-dev.md)

```bash
export ARCADIA_ROOT=%SOME_VALID_PATH%

cd "${ARCADIA_ROOT}"

ya make balancer/serval 

"${ARCADIA_ROOT}"/balancer/serval/serval -c "${ARCADIA_ROOT}/search/mon/tickenator/serval_configs/serval_config.yaml"

export OAUTH_TOKEN=<your_token>  # (access to ST, SPI-queue)

"${ARCADIA_ROOT}"/search/mon/tickenator/bin/tickenator
```

Application started on the localhost:8888


## Development

1. After edit: `ya tool horadric`

2. cd generated/tickenator_ts/tickenator_ts/ && vim package.json (bump version!)

3. npm publish --registry=https://npm.yandex-team.ru

4. Build: `ya make`

5. Commit: `svn ci -m "REVIEW:NEW commit message"`

## Start with UI

1. [Checkout](https://github.yandex-team.ru/Marty/tickenator-ui)
2. `npm install`
3. `npm run build`
TODO: Describe starting horadric2 tickenator with local static

## Doc

1. API: https://nda.ya.ru/3UY36f

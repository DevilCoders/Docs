# Contributing

## Getting Started

1. Clone repository on development server

  ```
  cd mobmaps-proxy-api
  ```

2. Install dependencies

  ```
  make deps
  ```

3. Run service:

  ```
  make dev
  ```

By default http-service starts on the port `8080`.

The application can also listen on a port:

```
MAPS_NODEJS_PORT=8080 make dev
```

## Testing

To run all tests use the command:

```
make validate
```

## Stress testing

1. Get requests to service from YQL in JSON [format](https://yql.yandex-team.ru/Operations/XhncVglcTrV_kRypEuh-LBEeffVDh7KlEVEigVcSuuo=)

```sql
PRAGMA yt.Pool = "MAPSAPI";

SELECT
    request,
    ip
FROM hahn.`home/logfeller/logs/maps-front-production-log/1d/2020-01-10`
WHERE tskv_format = 'front-mobmaps-proxy-api_app'
    AND request NOT LIKE '/ping'
    AND status LIKE '200'
LIMIT 1000000;
```

2. Build project

```sh
make build
```

3. Generate ammo:

```
node ./out/tools/gen-stress-ammo.js < ${path_to_yql_data} > /tmp/ammo.txt
```

4. Upload resulting ammo to MDS and update URLs in shooting configurations in .qtools.json.

## Deploying

This project uses [ymaps-qloud-tools](https://github.yandex-team.ru/maps/ymaps-qloud-tools)
(`qtools` for short) to interface with docker, the docker registry and the cloud platform Qloud.

Every commit to trunk will trigger a CI (Trendbox) build which:

1. Run tests.
2. Builds a docker image.
3. Pushes it to registry.
4. Deploys it to testing.
5. Run stress testing.

This is the preferred way to deploy.

### Manual release to testing

If CI is down, use the following command:

```
npx qtools release testing --force
```

### Manual release to external-testing

If CI is down, use the following command:

```
npx qtools release external-testing --force
```

### Deploy the current version to production

```
npx qtools deploy production --force
```

## Troubleshooting

If the tests contain "500/undefined/path not found", just update "inthosts" version from [here](https://sandbox.yandex-team.ru/resources?type=MAPS_CONFIG_INTHOSTS).

If the applicaion throws an error "self signed certificate in certificate chain", you have a problem with the internal SSL-certificate. Read more: https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vnode.js.

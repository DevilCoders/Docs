# http-api-stub

A project stub for http-services developed in Yandex Maps API.

## Forking

We provide an fork script with a simple wizard:

1. Switch to trunk in your local arcadia working copy:
```sh
arc checkout trunk
arc pull
arc checkout -b init-<your-new-service>
```

2. Go to `/maps/front`.

3. Start the interactive fork script:
```sh
make new-http-api-service-directory
```

4. Go to the new service directory:
```sh
cd services/<your-new-service>
```

5. Install dependencies:
```sh
npm install
```

6. Create a new branch, commit changes and create a PR:
```sh
arc add services/<your-new-service>
arc commit -m "Initial commit"
arc pr create
```

You can find more info on how to use the development scaffolding in [CONTRIBUTING.md](CONTRIBUTING.md)

## Maps HTTP API Service Naming Rules

There are 3 rules:

1. If service is available from *intranet* only: `${serviceName}-int` (example: `constructor-int`)
2. If service is available from *internet* or *intranet* and its API is *private* (for internal usage only): `${serviceName}-service` (example: `coverage-service`)
3. If service is available from *internet* and its API is *public*: `${serviceName}-api` (example: `preloader-api`)

See also [discussion](https://github.yandex-team.ru/maps/http-api-stub/issues/92) about naming rules.

## Dependencies

For maximum stability we enforce exact versions for all dependencies in [package.json](package.json)
(this rule is set in the [.npmrc](.npmrc) provided with your project) and use [package-lock.json](https://docs.npmjs.com/files/package-lock.json).

## Application Configuration

A project created from this stub stores configurations by environment.
The name of the current configuration is determined by the name of the current Yandex.Deploy environment
(using `MAPS_STAGE` env variable).

A good practise is to use configuration options instead of the value of current environment:

```js
// good
if (config.needDoSomething) {
    doSomething();
}

// bad
if (env === 'development') {
    doSomething();
}
```

In this case the application doesn't depend on the environment, but rather on the configuration options.

## Proxy

If you need to get a real IP address or the original URL of the request, check the documentation of your balancer.
For instance, you can read about load balancing in `Yandex Deploy`
[here (Qloud -> Y.Deploy: Migration guide)](https://wiki.yandex-team.ru/maps/dev/ui/deploy/yd/migration/#awacs-rewrite) and
[here (Y.Deploy: Balancing quick guide)](https://wiki.yandex-team.ru/deploy/docs/quick-start-in-deploy/balancing-quick-start/).
To get more information about headers modification during load balancing - please read an
[appropriate chapter](https://wiki.yandex-team.ru/cplb/awacs/cookbook/#kakmodificirovatzagolovkizaprosa) of the `AWACS cookbook`.

It's **not** recommended to enable [`trust proxy`](http://expressjs.com/en/guide/behind-proxies.html)
configuration setting of `express` framework, because balancer (at least `Y.Deploy`) doesn't override
`X-Forwarded-For` header from a client.

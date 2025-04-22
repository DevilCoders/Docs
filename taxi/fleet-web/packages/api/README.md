# @yandex-fleet/api

- [@yandex-fleet/api](#yandex-fleetapi)
  - [ApiProvider](#apiprovider)

## ApiProvider

If you need some global configuration to be used across the application,
the right place to add it is `queryConfig` object, which can be found in
[ApiProvider.tsx](src/ApiProvider.tsx) module.

The whole application is wrapped within the `ApiProvider` component, so
each query hook will use configuration from the `queryConfig` by default.

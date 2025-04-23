## Requirements

* [Node.js](http://nodejs.org/) `8`
* [npm](http://npmjs.org) `3`

## Add new proxy
Add new backend to config.
```(yaml)
  - environment: <abc service slug without maps->
    backends: <backend balancer or qloud component id>

  # with routing
  - environment: <abc service slug without maps->
    backends:
      - location: /
        upstream: <backend balancer or qloud component id>
      - location: /another/path
        upstream: <another backend balancer or qloud component id>

  # if your service uses internal (yandex-team.tld) cookies and is not compatible with yandex.tld
  - environment: <abc service slug without maps->
    backends: <backend balancer or qloud component id>
    internalOnly: true
```

[Build qtools config](#build-qtools-config) and [deploy new proxy](#release)

Wait from 30 mins to 1 hour and add access via IDM ([example](https://idm.yandex-team.ru/#rf-role=shB1xbti#group:42082@webauth-qloud/qloud-ext/maps/front-crowdtesting-proxy/envs/nmaps/user(fields:();params:(with_external:true)),rf-role=shB1xbti#group:144157@webauth-qloud/qloud-ext/maps/front-crowdtesting-proxy/envs/nmaps/user(fields:();params:(with_external:true)),rf-expanded=shB1xbti,rf=1)) for the groups depending on your project:
  * [Infrastructure team](https://abc.yandex-team.ru/services/maps-front-infra/)
  * Service
    * with postfix `-qa-users` in **Maps team** (for example, [Web maps QA](https://abc.yandex-team.ru/services/maps-front-maps-qa-users/))
    * or services in [Geoplatform testing Teams](https://abc.yandex-team.ru/services/mapsplatformtestingteam/services/)

New access is become available during 1 hour. Check that the new proxy works fine and close ticket.

### Add assessors
For adding access to assessors team  follow instructions at [maps-front-assessors-sync scheduler](../../schedulers/maps-front-assessors-sync)

## Build qtools config
```sh
$ make deps
$ make build
```

## Release
Deploy all proxies.
```sh
$ make deploy
```

or deploy only the specific one.
```
$ npx qtools deploy <environment>
```

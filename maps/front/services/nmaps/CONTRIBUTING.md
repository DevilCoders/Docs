# Contributing

  * [Local development](#local-development)
  * [Workflow](#workflow)
  * [Deployment](#deployment)

## Local development

  ### General

  1. Install [Arc](https://docs.yandex-team.ru/devtools/intro/quick-start-guide).

  2. Join [abc group](https://abc.yandex-team.ru/services/31094).

  3. Add local domain to hosts:
        ```
        127.0.0.1 nmaps.local.maps.yandex.ru
        127.0.0.1 nmaps.local.maps.yandex.com
        127.0.0.1 nmaps.local.maps.yandex.com.tr
        ```

  4. Go to the project work directory (assuming Arcadia is mounted into ~/arcadia)
        ```bash
        cd ~/arcadia/maps/front/services/nmaps
        ```

  Then there are two options: without and with docker. For both ways you should pass [TANKER_OAUTH_TOKEN](#tanker-oauth-token) to commands.

  ### Without docker (Linux, MacOS)

  1. Get certificate via [CRT](https://crt.yandex-team.ru):
      * Specify params:

            CA name:
            Internal CA

            Тип сертификата:
            Для web-сервера

            Хосты:
            *.local.maps.yandex.com.tr, *.local.maps.yandex.com, *.local.maps.yandex.ru

            ABC-сервис:
            Народная карта (фронтенд)
      * Save it into `~/.ssl/local.maps.yandex.tld.pem`.

  2. Install [NVM](https://github.com/nvm-sh/nvm)

  3. Type in console (being in the project working directory):
        ```bash
        make dev
        ```
  4. Point your browser at:
        https://nmaps.local.maps.yandex.ru:8080

  #### Backend instances

  By default `unstable` version of backend servants is used.
  If you need specific backend servants, you should specify it via `BACKEND_ENV` environment variable:
  ```bash
  BACKEND_ENV=@euclid make dev
  ```

  #### Translations

  By default application is built with russian translations only. If you need another translations, for example `en`, run:
  ```bash
  LANGS=en make dev
  ```

  #### Privacy

  By default application is built with internal privacy level (npro). If you need external, run:
  ```bash
  PRIVACIES=external make dev
  ```

  ### With docker

  1. Install [Docker](https://www.docker.com) for your OS.

  2. Log into [registry.yandex.net](https://wiki.yandex-team.ru/docker-registry/#authorization).

  3. Type in console (being in the project working directory):
        ```bash
        docker-compose up
        ```

  4. Point your browser at:
        https://nmaps.local.maps.yandex.ru:3000

  #### Backend instances

  By default `unstable` version of backend servants is used.
  If you need specific backend servants, you should specify it via `BACKEND_ENV` environment variable:
  ```bash
  BACKEND_ENV=@euclid docker-compose up
  ```

  #### Connecting to a running container

  Get container id:
  ```bash
  docker ps
  ```

  Connect:
  ```bash
  docker exec -it {CONTAINER_ID} bash
  ```

  #### Translations

  By default application is built with russian translations only. If you need another translations, for example `en`, run:
  ```bash
  LANGS=en docker-compose up
  ```

  #### Privacy

  By default application is built with internal privacy level (npro). If you need external, run:
  ```bash
  PRIVACIES=external docker-compose up
  ```

## Workflow

### Versioning

Build versions have the format of `major.minor.patch`.

* `major` is always 3.
* Increment `minor` when starting a new release iteration.
* Increment `patch` when building a new version for testing.

For example, `3.172.4` is the fifth version built and tested in release 172.

### Branches

#### Trunk branch

All changes scheduled for the next release iteration are merged into `trunk` branch.

Each change starts as a new pull request. Usually the "head" branch
is forked off `trunk` and has a `NMAPS-` prefix. For example, `NMAPS-1234`.

#### Release branch

When a new release iteration number `N = major.minor` starts, a new branch
`releases/maps-front/nmaps/N` is forked off `trunk`. All changes scheduled for the current release
iteration are merged here.

First commit has version `major.minor.0`.

Each change starts as a new pull request to `trunk` branch. After pull request has been merged to `trunk`,
its changes are cherry-picked to release branch `releases/maps-front/nmaps/N`.

When the last build in the current release is deployed in production,
a new branch `NMAPS-merge-release-N` is forked off `releases/maps-front/nmaps/N`
and merged into `trunk` branch via pull request.

### Commits

Commit message must be written in english and should be prefixed, in most cases, with corresponding task from issue tracker, for example:
```
NMAPS-10063: Add ability to filter moderation tasks by moderator
```

## Deployment

Make sure you are in release (`releases/maps-front/nmaps/N`) branch. When deploy is within common release flow, stable tanker branch is created. To create stable tanker branch you should pass [TANKER_OAUTH_TOKEN](#tanker-oauth-token) in `make deploy-production` command. If hotfix is deployed, `already-exists` error is expected for create stable tanker branch step.

### Testing

```bash
# Increment version, create a tag and deploy it to testing
make patch # or make minor
```

### Production
```bash
# Deploy latest tag to production environment
make deploy-production
```

### Hotfix

To patch a release in production without waiting for the next release, you should checkout release branch with current production version, cherry-pick fixing commit and run:
```bash
make hotfix
```
When the last build of the hotfix is deployed in production, its changes are cherry-picked to `trunk` branch via pull request.

## Tanker oauth token
Can be issued [here](https://nda.ya.ru/3SjQY7).

## Secrets

| Name                             | Link                                                             |
| -------------------------------- | ---------------------------------------------------------------- |
| maps-front-nmaps.production.app       | https://yav.yandex-team.ru/secret/sec-01ejxajmzmdepq47d0c6ezef22 |
| maps-front-nmaps.testing.app          | https://yav.yandex-team.ru/secret/sec-01ejxapab6n40wftemj2cgseeq |

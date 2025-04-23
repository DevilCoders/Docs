# Contribution Guide

This document describes some points about contribution process for altay.

## Codestyle

See [Yandex Maps](https://github.com/ymaps/codestyle).

## Install

Before start installation you have to make sure that there is `yatool` on your local machine.
Read more about this tool [here](https://wiki.yandex-team.ru/yatool/).
To install it please follow [the guides](https://wiki.yandex-team.ru/yatool/distrib/).
Export [TANKER_OAUTH_TOKEN](#tanker-oauth-token) secret to your $HOME/.bashrc or $HOME/.bash_profile file.

### Go to the project work directory

```bash
cd <arcadia-path>/maps/front/services/altay
# Local machine setup.
make local
# Install i18n
make i18n
# Run dev stand.
make dev
```

The local stand will be available at `https://altay.dev.yandex-team.ru:8080`.

### Solve any problems

#### i18n

If you need to update translations from tanker, run
```bash
make i18n
```

## Deploy

The project has at least two environments: `testing` and `production`.
To release `testing` environment run the following command:

```bash
make release-testing
```

The `production` environment usually never gets released before `testing`, so assuming the current version of `testing`
is already released, the `production` environment can be deployed via:

```bash
make deploy-production
```

## Tanker oauth token
Can be issued [here](https://nda.ya.ru/3SjQY7).

## Secrets

| Name                             | Link                                                             |
| -------------------------------- | ---------------------------------------------------------------- |
| maps-front-altay.production.app       | https://yav.yandex-team.ru/secret/sec-01g7vnkvtns39rq60xwye750am |
| maps-front-altay.testing.app          | https://yav.yandex-team.ru/secret/sec-01g7vnme76rrtcpm0f1xc2qmmk |
| maps-front-altay.development          | https://yav.yandex-team.ru/secret/sec-01g8827p81a9422p42he20tfhg |

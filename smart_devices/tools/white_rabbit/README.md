# White Rabbit

A hassle-free rabbit hole penetrator.

## Building

```sh
$ ya make smart_devices/tools/white_rabbit
```

## Usage

```sh
$ white_rabbit yandexstation_2
RH challenge: CD0396D69D771A8C065D0DF0012889F4
RH response:
P9TOiPLZ4JGjiRFLUjV4mOIz9Pvqi0nIBNVSHPtqB+lAYagaSqSNVL+TY5q1rxRK4lavLQrkLp6KyQ2L0AONdWBbhPsdljG4U8TTr2xSCY/8wgSb+qDvFSh/XHaFNaxSjwb6dNu7WrIoEV26DMToYlPjJYW/951XKultPe7cJzox1vS2+/GMuPWvvLCbD6jo6e+DRZgv2FaP6tPbuvcgf0nVC0H0rZGjEyaazkkzirZDjZMRA+jPmCHtkqR1cJSFM3n97BKNfpvr6MRH/bOrEz9s63cS/G88jCWssGBfbncZ4PeUvRarpzPd6meXgjSiu84fQ/joHy2lOBxX7AJcFQ==
```

By default tool will try to obtain OAuth token using your SSH key. If that doesn't work for you, get the token [manually](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=f2aac093416e4a949d727bd547207944) and put it in `SIGNER_TOKEN` environment variable:
```sh
$ export SIGNER_TOKEN=AQAD-qJSJ...
```

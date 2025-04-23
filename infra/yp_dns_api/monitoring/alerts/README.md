# Alerts generation for YP DNS API

Run after commit
```sh
$ ya make -r
$ ./update_alerts --juggler-token $JUGGLER_TOKEN
```

## Tokens
[Solomon](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa)

[Juggler](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0)

## Solomon project
[yp_dns_api](https://solomon.yandex-team.ru/admin/projects/yp_dns_api)

## Juggler alerts
[namespace=yp.dns.api](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dyp.dns.api)

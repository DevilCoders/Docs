# Alerts generation for YP DNS

Run after commit
```sh
$ ya make -r
$ ./update_alerts --solomon-token $SOLOMON_TOKEN --juggler-token $JUGGLER_TOKEN
```

## Tokens
[Solomon](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1c0c37b3488143ff8ce570adb66b9dfa)

[Juggler](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=cd178dcdc31a4ed79f42467f2d89b0d0)

## Solomon project
[yp_dns](https://solomon.yandex-team.ru/admin/projects/yp_dns)

## Juggler alerts
[namespace=yp.dns](https://juggler.yandex-team.ru/aggregate_checks/?query=namespace%3Dyp.dns)

# Сборка пакета

1. Поправить версию в pkg.json.
2. Выгрузить в dist:

```
ya package --debian --key=<YOUR_GPG_KEY> ./pkg.json
dupload --to market-common zookeeper_3.6.1yandex4_amd64.changes
```

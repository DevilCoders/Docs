# api для доступа к флагам из админки

## Deploy
https://deploy.yandex-team.ru/projects/avia-feature-flag-api

## Документация по ручкам

- [Получение функциональных флагов](./internal/controllers/featureFlag.md)
- [Определение живости сервиса](./internal/controllers/ping.md)

## Разработка

```
$ cp ./tools/samples/environments.sh ./tools/environments.sh
$ vi ./tools/environments.sh
$ ./tools/run-dev-api.sh
```

### Ручная сборка докер-образа

```
$ ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/feature_flag_api/pkg.json
```

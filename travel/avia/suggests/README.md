# Авиа Саджесты

## Запуск в dev

```
$ cp ./tools/samples/environments.sh ./tools/environments.sh
$ vi ./tools/environments.sh
$ ./tools/run-dev-api.sh
```

### Ручная сборка докер-образа

```
$ ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/suggests/pkg.json
```

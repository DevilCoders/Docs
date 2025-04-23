# flight-status-fetcher

## Разработка

```
$ cp ./tools/samples/environments.sh ./tools/environments.sh
$ vi ./tools/environments.sh
$ ./tools/run-dev-api.sh
$ ./tools/run-dev-update-from-airport.sh
$ ./tools/run-dev-celery.sh  worker -A travel.avia.flight_status_fetcher.worker -c 1
```

### Сборка докер образа локально

```
$ ./ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/flight_status_fetcher/pkg.json
```

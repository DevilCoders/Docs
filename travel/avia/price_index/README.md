# Сервис хранения авиа-цен

## Что умеет
1) индексировать цены
2) доставать цены

## Как запустить на dev машинке:

### Запуск api

```
$ cp tools/samples/environments.sh tools/environments.sh
$ vi tools/environments.sh
$ ./tools/run-dev-alembic.sh upgrade head
$ ./tools/run-dev.sh
```

### Изменение структуры БД

```
$ ./tools/run-dev-alembic.sh upgrade head
$ vi ./models/*
$ ./tools/run-dev-alembic.sh revision --autogenerate -m '<name>'
$ ./tools/run-dev-alembic.sh upgrade head
```

### Сборка образа руками

```
$ ya package --docker --docker-registry registry.yandex.net --docker-repository avia travel/avia/price_index/pkg.json
```

## Sentry
- production: https://sentry.production.avia.yandex.net/sentry/price-index/
- testing: https://sentry.testing.avia.yandex.net/sentry/price-index/

## Мониторинги
Не настроены

## Графики
- search-api
  - не настроены, но данные отправляются в solomon и можно смотреть, например, так https://nda.ya.ru/t/YeBTp0u84FQZ2m
- indexer
  - дашборд в solomon https://solomon.yandex-team.ru/?project=avia&dashboard=price_index&ConsumerPath=avia/production/price-index/search-results-consumer
  - состояние очереди в logbrocker https://lb.yandex-team.ru/logbroker/accounts/avia/production/search-results-queue?page=statistics&type=topic&tab=partitions&shownTopics=all%20topics&consumer=avia%2Fproduction%2Fprice-index%2Fsearch-results-consumer&metricsFrom=1631612529742&metricsTo=1631698929742&sortOrder=%22default%22
 
## Логи:
1) access.log - сюда пишется нечто подобное access.log, но с телом
2) info.log - сюда пишутся все сообщения с уровнем не ниже info
3) error.log - сюда пишутся все сообщени с уровнем не ниже ERROR
4) gunicorn.log - сюда пишутся gunicorn логи
5) sql.log - сюда пишутся sql запросы если попросили их писать

## Документация:
- [Поиск по диапазону дат](views/search.md)
- [Поиск множества направлений](views/min_price_batch_search_view.md)
- [Поиск минимальных цен в окне](views/top_direction_prices_by_date_window.md)


## TVM
* Testing: 2002806
* Production: 2002808

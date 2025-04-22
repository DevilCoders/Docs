## Что это такое

Тыква - это наш запасной продакшн. Если запрос не может быть обслужен ни одним бекендом (ошибки или что-то иное), тогда запрос отправляется в тыкву.

## Как выглядит

[РЦ тыквы](https://l7test.yandex.ru/morda-pumpi-rc/)

[Продакшн тыквы](https://l7test.yandex.ru/morda-pumpi/)

## Исходный код

[В Аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/portal/pumpi)

## Инфраструктура

### Генератор кеша

[Cache_generator](https://nanny.yandex-team.ru/ui/#/services/catalog/cache_generator/) - здесь просто запущен вызов скрипта, который делает запросы в специальный сервис offload
[Offload](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/offload.morda.yandex-team.ru/show/) - это балансер сервиса offload, который сделан специально для сбора кеша тыквы

### Тестинг

[testing-pumpi-yp](https://nanny.yandex-team.ru/ui/#/services/catalog/testing-pumpi-yp/)

### Продакшн

[production-pumpi-yp](https://nanny.yandex-team.ru/ui/#/services/catalog/production-pumpi-yp/)

## Настройки балансера

Сейчас список хранится в виде [yp-pod-set](https://a.yandex-team.ru/arc/trunk/arcadia/gencfg/custom_generators/balancer_gencfg/configs/l7heavy/globaldata.py?rev=7625768#L56)
[Тут](https://a.yandex-team.ru/arc/trunk/arcadia/gencfg/custom_generators/balancer_gencfg/configs/l7heavy/globaldata.py?rev=7594034#L823) задаются "бекенды" для разных видов нашего трафик.

Настройки l7test редактируются [тут](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/knoss_fast_testing/show/)

## Как поднять себе окружение

Разработка тыквы собрана в docker.
Нужно счекаутить репозиторий и выполнить ``make up`` (установив предварительно docker, конечно же)

## Логи и графики

Логи в [Кибане](https://portal-kibana.n.yandex-team.ru/goto/8ff50c009e97e134bc8909ffeb68325e)
Логи в [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/pumpi-nginx-access-log)
Сигналы в [yasm](https://nda.ya.ru/t/d27CkzYx3bbX2P)

## Запас тыквы
По итогам [встречи](https://calendar.yandex-team.ru/event/58536201?applyToFuture=0&event_date=2021-09-09T13%3A00%3A00&layerId=27427) договорились, что:
- тыква морды держит 100Крпс (пролива от Антиробота)
- весь заявленный трафик тыква + балансер должны держать в каждом ДЦ (на случай прихода локального ддоса в один ДЦ)

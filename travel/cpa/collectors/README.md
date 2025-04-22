# Коллекторы

Коллектор периодически считывает данные партнёра о заказах и записывает в logbroker.
Основная функция коллектора – преобразовать данные из формата партнёра в общий формат, пригодный для дальнейшей
обработки

Снэпшот - информация о состоянии заказа в момент очередного обращения к партнёру.
Набор снэпшотов определённого заказа формирует его историю

### Код коллектора

* добавить снэпшот в [order_snapshot.py](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/lib/order_snapshot.py) (создать наследника от `AviaOrderSnapshot` или `HotelsOrderSnapshot` или другого и добавить в `PROVIDERS`)
* коллектор должен быть унаследован от [Collector](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/collectors/lib/collector.py)
* в классе-наследнике нужно переопределить метод `_get_snapshots`, который представляет собой генератор, возвращающий снэпшоты (наследники `OrderSnapshot`).
* код коллектора расположить в виде python-модуля в `travel/cpa/collectors/{avia, hotels, ...}/{partner_name}`
* если запрос к партнёру требует повторов, функцию, выполняющую запрос, нужно обернуть в хелпер

```python
    self.get_raw_snapshots = with_retries(
        self.get_raw_snapshots_once,
        counter=self.metrics,
        key='collector.events.invalid_response',
    )
```

* вместо `requests.get` использовать `Collector.request_get`
* аргументы командной строки, специфичные для партнёра, задаются в методе `configure`

```python
    @classmethod
    def configure(cls, parser):
        parser.add_argument('--api-key', required=True)
```

* все коллекторы собираются в один исполняемый файл [collector_exec](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/collectors_exec/__main__.py), выбирается коллектор из списка `COLLECTORS` аргументом командной строки `--partner-name`

### Отладка коллектора

Для отладки коллектора можно или не отправлять данные в logbroker или использовать топик `travel-cpa@dev--collectors-result`.
Для него настроена поставка данных в [//logs/travel-cpa-dev-collectors-result](https://yt.yandex-team.ru/arnold/navigation?path=//logs/travel-cpa-dev-collectors-result)

### IPv4 proxy

Коллекторы ходят к партнёрам через прокси. Вся логика работы через прокси реализованоа в общем коде коллектора.
Хостнейм из `BASE_URL` автоматически заменяется на хостнейм прокси.

Для изменения адреса прокси можно использовать `--proxy-url`.
Для хождения напрямую нужно добавить `--no-proxy`

После добавления коллектора нужно обновить конфигурацию nginx в docker-образе прокси:
* запустить `tools` с параметром `proxy_config`
* локально собрать docker-образ из `devops/ipv4-proxy`
* опубликовать новую версию образа в docker registry в `registry.yandex.net/travel/cpa/ipv4-proxy`
* выкатить новую версию в [qloud](https://qloud-ext.yandex-team.ru/projects/avia/partners-proxy/production)

Подробнее про IPv4 proxy [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/travel/cpa/devops/ipv4-proxy)

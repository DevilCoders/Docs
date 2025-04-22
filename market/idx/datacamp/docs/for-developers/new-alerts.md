# Создание мониторингов
Мониторинги можно разделить на следующие типы:
* мониторинги контейнеров
  - проверка, что в контейнерах есть свободное место на диске, работают logrotat
  - проверка, что сервис успешно запустился в контейнере
  - количество крешей/ООМов бинарников в контейнерах
* мониторинги на logbroker
  - проверка, что сервис читает и коммитит сообщения
  - проврерка квоты на запись в топик либо же на весь аккаунт
* 4XX/5XX ручек
  - ручки строллера начали пятисотить
* работоспособность различных пайплайнов обработки данных
  - системные офферы
  - статус работы асинхронных задач в sandbox
* мониторинги на основе графиков в yasm/solomon

В большинстве случаев для создания мониторинга требуется совершить три действия: реализовать отправку сырых событий в juggler, настроить их агрегацию и написать инструкцию к мониторингу. 

## Мониторинги на основе графиков в solomon {#solomon-based-alerts}
[Основная статья по алертам в solomon](https://solomon.yandex-team.ru/docs/concepts/alerting/).

TLDR:
1. Создаем алерт в [админке](https://solomon.yandex-team.ru/admin/projects/market.datacamp/alerts/new?aType=custom)
   - Ко всем основным полям есть описание, смысла их дублировать здесь нет
   - В annotations указываем два обязательных элемента `juggler_host` и `juggler_service`, и желательно в аннотацию добавить `description`
   - В качестве канала указываем [juggler-default](https://solomon.yandex-team.ru/admin/projects/market.datacamp/channels/juggler-default). Это универсальный канал для отправки сигналов в juggler.
2. Добавляем агрегацию в [малек](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs/configs)
{% cut "Пример конфига в малек %}

```bash
cat arcadia/market/sre/conf/market-alerts-configurator/my-new-solomon-based-alert.yaml
juggler:
  meta:
    urls:
      - title: Траблшутинг
        url: <ссылка на инструкцию, что делать при горящем мониторинге>
  checks:
    - service: <название сервиса из алерта в соломоне>
  default:
    aggregator: logic_or
    aggregator_kwargs:
      nodata_mode: force_crit
    check_options: {}
    host: <название хоста из алерта в соломоне>
    namespace: market.datacamp
    notifications: []
    tags:
      - market_indexer_datacamp
      - market_production
      - production
      - market
      - _market_
    ttl: 900
```

{% endcut %}

## Мониторинги на входящие топики в логброкер
Частный случай мониторингов на основе графиков в solomon. На каждый топик принято заводить три основных мониторинга [CreateTimeLagMsByCommitted](https://logbroker.yandex-team.ru/docs/reference/metrics#CreateTimeLagMsByCommitted),
[MessageLagByCommitted](https://logbroker.yandex-team.ru/docs/reference/metrics#MessageLagByCommitted), [ReadTimeLagMs](https://logbroker.yandex-team.ru/docs/reference/metrics#ReadTimeLagMs), для заведения всех мониторингов рекомендуется
использовать тулзу [create_solomon_alerts](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/dev/create_solomon_alerts). Тулза по названию топика генерирует алерты в solomon, который будут отправлять сигналы через дефолтный канал.
**Не забываем добавить агрегацию через малек.**

## Мониторинги всея хранилища {#active-alerts}
Примеры мониторингов: мониторинг на свежесть таблички в YT, проверка свежести системного оффера. Не подходит для мониторинга, который
считается по всему офферному стейту либо время выполнения измеряется в минутах.

В таком случае нам подходит механизм [активныв проверок](https://docs.yandex-team.ru/juggler/aggregates/actives#http) в juggler.
Основная идея заключается в том, что за статусом мониторинга juggler будет ходить в админку рутин через балансер. Таким
образом мы не считаем один и тот же мониторинг на всех контейнерах рутин, а будет считать на одном* контейнере.

Как написать такой мониторинг:
1. Добавить код проверки в ручку рутин `/monitoring`, [вот сюда](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/lib/monitorings/common.py?rev=r9146249#L41)
2. Настроить агрегат в мальке, [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs/configs/mi-datacamp-united.yaml?rev=r9299568#L335-347)
3. Готово, вы прекрасны

* *На самом деле juggler ходит не один раз, а несколько, чтобы исключить флапы

## Мониторинги по офферному стейту {#offer-state-alerts}
Примеры мониторингов: количество офферов с цветом Y, количество офферов без картинок, количество оффером с чем угодно

1. Начинаем считать нужную метрику в [stats-calc](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/tasks/statistics)
2. Накликиваем алерт в solomon по [инструкции](#solomon-based-alerts) и конфиг в мальке
3. Готово, вы восхительны

## Тяжелые мониторинги не по офферному стейту {#heavy-monitorings}
Примеры мониторингов: check_sender_to_miner_state

Тяжелые мониторинги не по офферному стейту мы считаем в sandbox, и явно пушим статус проверки в juggler.

1. Добавляем свою проверку в таску [CheckStateMonitorings](https://a.yandex-team.ru/arc_vcs/market/idx/datacamp/routines/lib/tasks/check_state_monitorings.py?rev=r9289303#L20)
2. Настраиваем агрегат в мальке, [пример](https://a.yandex-team.ru/arc/trunk/arcadia/market/sre/conf/market-alerts-configs/configs/mi-datacamp-united.yaml?rev=r9299568#L273-279)
3. Готовы, вы бесподобны

## Ссылки
* [Документация по Juggler](https://docs.yandex-team.ru/juggler/)
* [Малек aka market-alerts-configurator](https://wiki.yandex-team.ru/market/sre/fordev/howto-market-alerts-configurator/)

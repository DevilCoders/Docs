## Что это?
TL;DR: сервис управляемого "троттлинга" операций над объектами.

Мотивация и логика описаны в [RFC](docs/draft.md). Inspired by [Google Srsly talk](https://www.youtube.com/watch?v=BOP3z7uCW4w).

## Доступ
* UI - [orly.yandex-team.ru/ui/](https://orly.yandex-team.ru/ui/)
* API - [orly.yandex-team.ru/rest/](https://orly.yandex-team.ru/rest/)

## CLI
* Доступен простой CLI для orly: [infra/orly/ctl](https://a.yandex-team.ru/arc/trunk/arcadia/infra/orly/ctl).
* Предлагается все правила хранить в репозитории в качестве reference: [infra/orly/rules](https://a.yandex-team.ru/arc/trunk/arcadia/infra/orly/rules).
  И вносить изменения через `orlyctl apply-rule -f rules/salt-state-apply.yaml`.

## Модель
В модель входят два объекта:

* `Rule` - правило того, как нужно "размазывать" (троттлить) операции.
  Например, "выкладки новых конфигураций l3mngr" или "применени конфигурации солта на хостах".
* `Operation` - именованное действие над чем-то в рамках правила.
   Например, "выкладка новой конфигурации балансера nanny в рамках правила awacs-balancer-updates" или "примение изменения в солте на хосте sas1-5166". Для этого этого служит поле `op_id`, которое должно уникально идентифицировать объект, многожество одновременных которое мы ограничиваем:
  * `sas1-5166.search.yandex.net` - имя хоста, если мы хотим ограничить количество одновременно обрабатываемых хостов
  * `production-balancer-morda-sas` - имя сервиса, если мы хотим ограничить количество одновременно обрабатываемых сервисов

## Use case
Давайте возьмём примеры:
    У нас есть огромное количество хостов, на которых работает netconfig-fix, настраивающий маршруты на хосте. Если он обнаружил проблему в настройках, он хочет наложить "fix". В случае программной или конфигурационной ошибки мы можем на большом количестве хостов флота RTC выполнить ошибочные действия в единицы минут и "уложить" кластер.
    Нам нужна оркестрация таких действий.
Решение с orly:

* Создаём правило `netconfig-fixall` c настройкой максимального количество операций и, потенциально, расписанием - например в выходные запретить такие действия вообще.
* Обучаем netconfig-fixall "ходить" в orly и запрашивать разрешение на операцию, идентификатором назначаем hostname.

В результате все действия будут оркестрированы и их можно централизовано ускорять/отключать.

## Правила
Описывают органичения и расписание того, какие операции разрешать. Модель такая:

* в конкретный момент времени согласно настройкам одновременно выполняться может только `maxAllowed` количество операций.
  Это значение может быть задано глобально на операцию, либо для любого временного интервала её можно переопределить
* операция должна в какой-то момент закончиться, освободив место для следующей
  Т.к. система рассчитана был максимально простой (и надёжной), то пользователь (например, netconfig на хостах) **освобождена** от необходимости самостоятельно (через вызов API) завершать операцию. Это производит сам сервис, удаляя операцию (считая её успешной) после `duration` секунд с момента её старта.

### Расписание
Правила могут иметь расписание, например:

```
    "spec": {
        "duration": "120s",
        "maxAllowed": 400,
        "schedule": {
            "enableDays": [
                {
                    "day": "MON",
                    "begin": "00:00",
                    "end": "09:59"
                    "maxAllowed": 10
                },
                {
                    "day": "MON",
                    "begin": "10:00",
                    "end": "19:00"
                },
                {
                    "day": "MON",
                    "begin": "19:01",
                    "end": "22:00",
                    "maxAllowed": 10
                },
                // ...
            ]
        }
    }
```
Такое расписание для понедельника (`MON`) означает (время всегда московское):

* с 00:00 до 09:59  максимально можно 10 операций
* с 10:00 до 19:00 - 400 операций (взято с top level) настройки
* с 19:01 до 22:00 - 10 операций
* с 22:01 до 23:59 - 0 операций, т.к. этот период вообще не указан

**Ограничения**:
* Максимальное количество правил на день недели - 10.

### Селектор лейблов
Правила могут иметь фильтр (*seleсtor*) по допустимым лейблам операций:

```yaml
meta:
  id: 'hostman-kernel-production'
spec:
  duration: '1200s'
  maxAllowed: 2
  selector:
    matchIn:
      - key: "geo"
        values: ["sas", "msk"]
      - key: "prj"
        values: ["yabs-rtc-mtn"]
```
Семантика **whitelist'а** и логического **AND**:

* разрешить правило только, если у операции label "geo" совпадает с одним из указанных
* и prj label равен "yabs-rtc-mtn"

## Примеры API
**Создание/изменение правила**:

```
cat > rule.json
{
    "rule":
    {
        "meta": {
            "id": "netconfig-apply-routes"
        },
        "spec": {
            "max_allowed": 10,
            "duration": "300s"
        }
    }
}
---
curl --data @rule.json https://orly.nanny.yandex-team.ru/rest/CreateRule/
```
**Старт операции**:

```
cat > op.json
{
    "rule": "netconfig_apply_routes",
    "id": "sas1-0219.search.yandex.net"
}
---
curl --data @op.json http://orly.nanny.yandex-team.ru/rest/StartOperation/
```
## Метрики
Экспортируются следующие метрики:

* `handle_operation_request_{ok,fail}_dhhh`
* `handle_create_rule_{ok,fail}_dhhh`
* `handle_get_rule_{ok,fail}_dhhh`

Пример: [handle_operation_request_ok_dhhh](https://yasm.yandex-team.ru/chart/itype=rtcsmall;prj=orly;geo=sas;hosts=ASEARCH;signals=hsum(unistat-handle_operation_request_ok_dhhh)/)

Так же экспортируются отдельные метрики по статусам операций для каждого правила. Правило записывается в tier тэг. Например:

* [netconfig-apply-routes](https://yasm.yandex-team.ru/chart/itype=rtcsmall;prj=orly;tier=netconfig-apply-routes;hosts=ASEARCH;signals=%7Bhsum(unistat-handle_operation_request_forbidden_dhhh),hsum(unistat-handle_operation_request_allow_dhhh)%7D/)
* [salt-state-apply](https://yasm.yandex-team.ru/chart/itype=rtcsmall;prj=orly;tier=salt-state-apply;hosts=ASEARCH;signals=%7Bhsum(unistat-handle_operation_request_forbidden_dhhh),hsum(unistat-handle_operation_request_allow_dhhh)%7D/)

## Сервис
* Выделен в YP.lite - [production_orly](https://nanny.yandex-team.ru/ui/#/services/catalog/production_orly/).
* Кластер etcd настроен [скриптом в hardcode mode](https://a.yandex-team.ru/arc/trunk/arcadia/infra/orly/exec_etcd.py).

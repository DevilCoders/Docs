# Транспорты "Начислятора"

Топики для LB описаны в 2-х файлах-конфигах (подробнее в [конфигурации](configs.md)):

- в [приложении](https://a.yandex-team.ru/arc_vcs/billing/hot/accrualer/config/prod/accrualer.yaml) описаны общие топики
  для работы приложения (входящие потоки, топики для ошибок, неизвестных событий и событий для будущего)
- в [логике](https://a.yandex-team.ru/arc_vcs/billing/hot/accrualer/config/prod/logic.yaml) описаны конкретные топики
  для актов и начислений для разных namespace, так же есть указание на директорию, где лежат расписанные события для
  формирования начислений по удержаниям

## Входящие

### Logbroker

Сервис читает три потока событий:

- поток исходных событий из системы счетов - это основной поток входящих данных:
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing/{{env}}/accounts-events
- поток ручных событий - можно использовать для переотправки потерянных событий или иных ручных вмешательств:
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing/{{env}}/manual-events
- поток событий взаимозачетов - специальная очередь для обработки взаимозачетов ([подробнее](nettings.md)):
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-accrualer/{{env}}/netting-events

В каждом окружении потоки читаются через одного consumer-а:

- https://logbroker.yandex-team.ru/lbkx/accounts/billing/{{env}}/events-accrual-consumer

### YT

На YT лежат расписанные события (marked events) для формирования начислений по взаимозачетам. У каждого namespace своя
директория, которая указывается в логическом конфиге в
секции `marked_event` ([пример](https://a.yandex-team.ru/arc_vcs/billing/hot/accrualer/config/prod/logic.yaml?rev=r9493931#L80))

## Исходящие

Топики для поставки начислений и актов описываются в логическом конфиге, актуальную конфигурацию топиков смотреть в нем.
Для dry-run топиков и поставок используется суффикс `-dry` в названии.

### Доходные/агентские начисления

- Такси:
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-accrualer/{{env}}/accruals/new-accrual
- Коммунальный топик:
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-accrualer/{{env}}/accruals/new-accrual-common

### Расходные начисления

- Пустой:
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-accrualer/{{env}}/accruals/spendable-accruals
- Коммунальный топик:
    - https://logbroker.yandex-team.ru/lbkx/accounts/billing-accrualer/{{env}}/accruals/spendable-common

### Выгрузка начислений в YT

Актуальные трансферы смотреть [тут](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfers).

**Важно:** Все выгрузки из одного окружения настроены в одну директорию. Название таблицы в директории с выгрузкой
соответствует названию топика, из которого происходит выгрузка.

Готовые начисления выгружаются в дин.таблицы на YT через механизм репликации DT.

Директории:

- начисления:
    - https://yt.yandex-team.ru/{{cluter}}/navigation?offsetMode=key&path=//home/balance/{{env}}/new_billing/accrualer/new_accruals
- акты:
    - https://yt.yandex-team.ru/{{cluster}}/navigation?path=//home/logfeller/logs/billing/hot/accrualer/{{env}}/agent-acts
- ошибки:
    - https://yt.yandex-team.ru/{{cluster}}/navigation?path=//home/logfeller/logs/billing/hot/accrualer/{{env}}/errors
- неизвестные события:
    - https://yt.yandex-team.ru/{{cluster}}/navigation?path=//home/logfeller/logs/billing/hot/accrualer/{{env}}/unknown-event

#### Выгрузки

- тест:
    - агентские начисления:
        - [на Хан](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dttocefckmvt4jbs60c6/view)
          , [на Арнольд](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dtt5qcbv2rknl4la95q2/view)
    - расходные:
        - [на Хан](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dtt1hsknulj029n3u3a0/view)
          , [на Арнольд](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dttj0bhaeehtg9bukavb/view)
- прод:
    - агентские начисления:
        - [на Хан](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dtt3i5q8mhs3seit3t8m/view)
          , [на Арнольд](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dtt1vanu87h3ugv6slbf/view)
    - расходные:
        - [на Хан](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dttirvsfrlp45s03q8qi/view)
          , [на Арнольд](https://yc.yandex-team.ru/folders/akujj8ktnsm7bo3k98pl/data-transfer/transfer/dttgct64l8lp92ag9fvs/view)

# Руководство по сценарию "noc-hard"

Сценарий предназначен для выполнения долгих работ со свитчём.
Долгие работы — это работы, которые могут занять больше получаса времени и/или несут изменения в коммутации/ip-адрессации подключенных к свитчу серверов.
Если работы быстрые (просто ребут свича), то вам нужен другой сценарий - простой NOC сценарий ([noc-soft](https://docs.yandex-team.ru/wall-e/scenario/noc-soft)).

Доступ к сценарию осуществляется через [IDM](https://idm.yandex-team.ru/#rf=1,rf-role=cTYH9Vus#walle/scenario/noc-hard(fields:()),f-status=all,sort-by=-updated,rf-expanded=cTYH9Vus)

## Ограничения
- в рамках одного сценария возможно запросить сервера, принадлежащие только одному свичу;
- сценарии внедрены еще не на всех владельцев серверов. Текущий список подключенных к сценариям команд/владельцев: RTC, MDB, MDS, Sandbox MTN, Метрика.

{% note warning %}

На текущий момент для этого сценария осуществляется валидация - Wall-e проверяет, что все хосты из стойки/списка имеют хотя бы один из whitelist тегов или наличие сконфигурированного Maintenance Plot на проекте, к которому принадлежит хост.

Текущий список whitelist тегов: `"rtc"`

Если на вход попал хотя бы один хост, не проходящий валидацию, то Wall-e отдаст 400-ку и сообщение вида `"Host '<inv>' does not have any whitelist tags on it, whitelist tags: <current whitelist tags>"`

{% endnote %}

## Создание сценария
Создать сценарий можно на странице [Scenarios](https://wall-e.yandex-team.ru/scenarios). Нажимаем кнопку "Create", в появившейся форме в выпадающем списке "Scenario type" выбираем тип "noc-hard".
Заполняем форму:
- В поле "Ticket" указывает тикет в StarTrek'е, по которому проводятся работы. У робота [robot-walle@](https://staff.yandex-team.ru/robot-walle) должен быть доступ на чтение и создание комментариев в очереди StarTrek'а, или в этом конкретном тикете.
- В поле "Name" вводим произвольное имя сценария.
- Переключатель "Resources" позволяет ввести список конкретных хостов ("Hosts"), или указать имя свитча ("Switch").
- В поле "Scheduled maintenance" следует указать планируемую дату и время начала работ.
- Установка галочки "Autostart" позволяет сразу же стартовать сценарий.

{% note warning %}

Настоятельно просим заполнять поле **"Scheduled maintenance"**.

Эта информация потребуется владельцам серверов для согласования работ, а также позволит автоматике Wall-E корректно спланировать снятие нагрузку серверов к назначенному времени.

{% endnote %}

Список хостов можно задать в одном из трех форматов: "имя (fqdn)", "инвентарный номер (inv)" или "uuid", по одному на строке или через пробел.

Также можно создать сценарий из основного интерфейса Wall-e: выбираем галочкой нужные хосты, в появившемся меню операций с выбранными хостами выбираем "Create scenario".

## Ход работы сценария
Разбиение хостов на группы, согласование и ход работы происходит полностью аналогично [itdc-maintenance](https://docs.yandex-team.ru/wall-e/scenario/itdc-maintenance) сценарию за некоторыми исключениями:
* хосты не выключаются в процессе подготовки к работам
* хосты не перезагружаются и не переналиваются
* после выполнения работ на стороне NOC надо нажать кнопку `Finish` на странице сценария в UI Wall-E


## Работа через API
Список всех ручек API доступен по адресу https://api.wall-e.yandex-team.ru/

Немного примеров для создания и управления сценарием:
* создание с указанием свитча:
  ```
  curl -X POST https://api.wall-e.yandex-team.ru/v1/scenarios \
    -d '{"name": "noc hard test", "scenario_type": "noc-hard", "ticket_key": "TICKET-66", "script_args": {"switch": "vla1-1s84", "maintenance_start_time": 1629897530}}' \
    -H 'Content-Type: application/json' -H 'Authorization: OAuth <token>'
  ```
* создание с указанием списка хостов:
  ```
  curl -X POST https://api.wall-e.yandex-team.ru/v1/scenarios \
    -d '{"name": "noc hard test", "scenario_type": "noc-hard", "ticket_key": "TICKET-66", "hosts": ["host1.yandex-team.ru", "host2.yandex-team.ru"], "script_args": {"maintenance_start_time": 1629897530}}' \
    -H 'Content-Type: application/json' -H 'Authorization: OAuth <token>'
  ```
* сигнал окончания работ со стороны NOC и начало возврата хостов в работу после работ:
   ```
   curl -X PATCH https://api.wall-e.yandex-team.ru/v1/scenarios/<id> \
     -d '{"labels": {"WORK_COMPLETED": "true"}}' \
     -H 'Content-Type: application/json' -H 'Authorization: OAuth <token>'
   ```


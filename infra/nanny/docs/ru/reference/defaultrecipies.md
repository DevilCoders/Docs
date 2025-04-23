# Как настроить стандартные рецепты в сервисе

Сервис в Nanny по умолчанию использует стандартные рецепты для подготовки и активации. Ниже приведено краткое описание этих рецептов и рекомендации по настройке.

## Полезные ссылки

Код рецептов можно посмотреть в [Аркадии](https://arc.yandex-team.ru/wsvn/robots/trunk/genconf/recepies) или в [Nanny](https://nanny.yandex-team.ru/ui/#/alemate/recipes/).

## Конечный автомат состояний сервиса

![img](https://jing.yandex-team.ru/files/sshipkov/Screenshot%202021-07-12%20at%2022.48.26.96df873.png)

* **prepare** – подготовка ресурсов конфигурации сервиса на хостах
* **activate** – активация конфигурации сервиса на хостах
* **deactivate** – деактивация конфигурации сервиса на хостах
* **destroy** – удаление ресурсов конфигурации сервиса с хостов

### Структура рецепта и типы задач

Все доступные типы задач и их поля в [Nanny](http://nanny.yandex-team.ru/ui/#/alemate/tasktypes_help/).

### Входные параметры для любого рецепта
На вход рецепту будут переданы обязательные параметры:

* `conf_id` – идентификатор конфигурации, которую необходимо подготовить и активировать
* `service_id` – идентификатор сервиса
* `snapshot_id` – идентификатор snapshot'а, которому соответствует активируемая конфигурация
* `ticket_id` – идентификатор тикета (если сервис привязан к очереди), иначе `None`
* `transport` – в зависимости от выбора Engine в настройках сервиса, либо `cqudp` (BSCONFIG), либо `iss` (ISS)

### _prepare_service_configuration.yaml
Подготавливает конфигурацию `conf_id`

1. Выполняет `prepare`.
1. После успешного выполнения предыдущего пункта выполняет `global prepare`.

код рецепта

```code
# Prepare *only* recipe: allows to specify degrade levels and degrade speed
{%- set stop_degrade_level = stop_degrade_level|default(0.1) %}
{%- set transport = transport|default('cqudp') %}
{%- set prepare_operating_degrade_level = prepare_operating_degrade_level|default(1.0) %}
{%- set prepare_max_degrade_speed = prepare_max_degrade_speed|default(1.0) %}
description: Deploy {{ conf_id }}, snapshot {{ snapshot_id }}

nanny_service_id: {{ service_id }}
nanny_ticket_id: {{ ticket_id }}
tasks:
    prepare:
        type: configuration_prepare
        configuration: {{ conf_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }}

        max_degrade_speed: {{ prepare_max_degrade_speed }}
        operating_degrade_level: {{ prepare_operating_degrade_level }}
        stop_degrade_level: {{ stop_degrade_level }}
        description: 'Prepare {{ conf_id }}'
    global_prepare:
        type: global_configuration_prepare
        configuration: {{ conf_id }}
        transport: {{ transport }}
        description: 'Global prepare {{ conf_id }}'
        dependencies:
          - prepare

```

#### Параметры {#prepare-service-options}

`prepare_operating_degrade_level`:
* Какую долю можно брать для обновления, насколько мы можем деградировать сервис. 
`operation_degrade_level == 0.1` означает, что во время выкладки активным будет оставаться  `1 - 0.1 = 0.9`, то есть 90 всех инстансов. Оставшиеся 10% будут распределены между обрабатываемыми и мертвыми инстансами. Например, есть 100 инстансов, из них 5 лежит, `operating_degrade_level == 0.1` – будем брать по 5 машин для выкладки.
* По умолчанию - **1.0**
* Зачем менять - Пусть есть io-intensive сервис и для него на хосты выезжает большой файл. Тогда, если сразу везде дёрнут `sky get`, диск окажется перегружен, просядет время ответа.

`stop_degrade_level`:
* Максимальная допустимая доля ошибок, после которых мы будем считать, что задача все равно выполнена успешно
Например, всего есть 1000 инстансов, а `stop_degrade_level == 0.1`, то даже если на 100 из них задача завершилась неудачей, мы все равно будем считать, что в целом задача выполнилась успешно. Важная деталь: запуск задачи с `stop_degrade_level > operating_degrade_level` приведет к тому же результату, как и запуск с `stop_degrade_level == operating_degrade_level`. Поскольку мы не можем погасить долю инстансов, большую, чем `operating_degrade_level`, то и число неудач, равное `stop_degrade_level` никогда не будет достигнуто, и задача успешно завершится только если число ошибок будет не больше, чем `operating_degrade_level`.
*Замечание:* выкладка инстанса может завершиться неудачей:
    * из-за проблем с хостом. Когда хост очнется, инстанс будет погашен в первую очередь.
    * из-за проблем с iss. На инстансе останется старая версия, исправлять нужно будет вручную.
* По умолчанию - **0.1**
* Зачем менять - При выкладке должно выполняться условие
`int([кол-во инстансов] * stop_degrade_level) >= [кол-во неудачно подготовленных инстансов]`. Исходя из нижней оценки правой части, можно принимать решение об увеличении `stop_degrade_level`

`prepare_max_degrade_speed`:
* Описание - Максимальная доля инстансов, которую можно деградировать в секунду, лимитирует скорость деградации
* По умолчанию - **1.0**
* Зачем менять - Требуется уменьшить, если сервис высоконагруженный


### _activate_only_service_configuration.yaml
Активирует конфигурацию `conf_id`

1. Выполняет `new_configuration_activate`, если `duration == 0` и `timed_configuration_activate` в обратном случае.
1. После успешного выполнения предыдущего пункта выполняет `global_configuration_activate`.

код рецепта

```code
# Activate *only* recipe: assumes that service configuration is prepared
{%- set operating_degrade_level = operating_degrade_level|default(0.1) %}
{%- set stop_degrade_level = stop_degrade_level|default(0.1) %}
{%- set check_port = check_port|default(False) %}
{%- set check_status_script = check_status_script|default(False) %}
{%- set transport = transport|default('cqudp') %}
{%- set duration = duration|default(0) %}
description: Activate {{ conf_id }}, snapshot {{ snapshot_id[:11] }}

nanny_service_id: {{ service_id }}
nanny_ticket_id: {{ ticket_id }}
tasks:
    activate:
        type: {{ 'new' if duration == 0 else 'timed' }}_configuration_activate
        configuration: {{ conf_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }}
        activate_timeout: 60
        operating_degrade_level: {{ operating_degrade_level }}
        stop_degrade_level: {{ stop_degrade_level }}
        check_port: {{ 'true' if check_port else 'false' }}
        check_status_script: {{ 'true' if check_status_script else 'false' }}
        description: 'Activate {{ conf_id }}'
        {%- if duration != 0 %}
        duration: {{ duration }}
        {%- endif %}
    global_activate:
        type: global_configuration_activate
        configuration: {{ conf_id }}
        transport: {{ transport }}
        description: 'Global activate {{ conf_id }}'
        dependencies:
            - activate
```


В рецепте есть один неизменяемый параметр
`activate_timeout: 60`
Он выполняет роль ограничения сверху на время старта каждого инстанса.

**Актуален только для `bsconfig`.**

#### Параметры {#activate-service-options}
`operating_degrade_level`:
* см `prepare_operating_degrade_level`
* По умолчанию - **0.1**
* Зачем менять - Изменяется в зависимости от того, сколько инстансов требуется поддерживать в активном состоянии

`stop_degrade_level`:
* см `stop_degrade_level`

`max_degrade_speed`:
* см `max_degrade_speed`

`check_port`:
* Описание - Требуется ли `TCP-check` порта инстанса (используется в проверке живости инстанса в `bsconfig`, где считается нормальным для демона открыть порт только на `localhost`, пока демон не будет готов к работе)
 **актуально только для транспорта `cqudp`**
* По умолчанию - **False**
* Зачем менять - Если сервис на `bsconfig` и вы понимаете, что делаете

`check_status_script`:
* Описание - Требуются ли проверка существования скрипта `loop-httpsearch` и запуск `status` у этого скрипта
**актуально только для транспорта `cqudp`**
* По умолчанию - **False**
* Зачем менять - Если сервис на `bsconfig` и вы понимаете, что делаете

`duration`:
* Описание - Минимальная длительность операции в секундах. Задаёт минимальное время, на которое нужно растянуть переключение, увеличивая интервалы между переключениями инстансов.
* По умолчанию - **0**
* Зачем менять - Сценарии, когда стоит выставить большой интервал времени:
    * выкладка сносит кэш – ставим, например, 6 часов
    * небезопасная выкладка – возможность вовремя заметить неполадки и остановить выкладку

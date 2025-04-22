# Рецепты выкладки Alemate/Nanny

## Что это? {#intro}

Для выкладки сервисов Nanny используется специальный формат **рецептов выкладки**, который позволяет:

* задавать в виде графа порядок выкладки инстансов сервиса по датацентрам/геолокациям/произвольным группам инстансов;
* управлять допустимым на время выкладки уровнем деградации сервиса;
* устанавливать критерий успеха выкладки в зависимости от доли успешно обработанных инстансов;
* выполнять ряд прочих действий в процессе выкладки: уводить пользовательский трафик из локации на время её переключения, отправлять нотификации в switter.

Рецепты описываются в виде [yaml-документов](http://ru.wikipedia.org/wiki/YAML). Рецепт содержит описание задач (и взаимосвязей между ними), которые нужно выполнить для выкладки релиза. Рецепт может принимать конкретные параметры, с которыми он будет запущен, которые внедряются в него с помощью шаблонизатора [Jinja2](http://jinja.pocoo.org/).

## Где хранятся рецепты? {#where}

Рецепты хранятся в Аркадии: `ssh://arcadia.yandex.ru/robots/trunk/genconf/recepies` ([https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/alemate/recipes)](https://a.yandex-team.ru/arc/trunk/arcadia/infra/nanny/alemate/recipes).


## Как получить доступ к рецептам на запись {#access}

Доступ есть у всех.

## Простейший пример {#example}

Простейший рецепт активации (запуска новой ревизии) сервиса выглядит так:

Граф рецепта:
![img](https://jing.yandex-team.ru/files/sshipkov/2017-07-0617-39-39.161fa01.png)


{% cut "Рецепт" %}

```
description: Activate {{ conf_id }}, snapshot {{ snapshot_id[:11] }}

nanny_service_id: {{ service_id }}
nanny_ticket_id: {{ ticket_id }}
tasks:
    activate:
        type: new_configuration_activate
        configuration: {{ conf_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }}
        operating_degrade_level: {{ operating_degrade_level }}
        stop_degrade_level: {{ stop_degrade_level }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        instance_selector: '{{ instance_selector }}'
        max_degrade_speed: {{ max_degrade_speed }}
    global_activate:
        type: global_configuration_activate
        configuration: {{ conf_id }}
        transport: {{ transport }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        dependencies:
            - activate
```

{% endcut %}

В этом рецепте две задачи:

* Плавная активации инстансов сервиса (тип задачи `new_configuration_activate`);
* Одновременная активация всех инстансов сервиса (тип задачи `global_configuration_activate`).

Более сложный рецепт активации сервиса выглядит так:

![img](https://jing.yandex-team.ru/files/sshipkov/2017-07-0617-38-39.77ab1cb.png)


{% cut "Рецепт" %}

```
{%- set operating_degrade_level = operating_degrade_level|default(0.1) -%}
{%- set operating_degrade_man = operating_degrade_man|default(False) -%}
{%- set operating_degrade_sas = operating_degrade_sas|default(False) -%}
{%- set operating_degrade_vla = operating_degrade_vla|default(False) -%}
{%- set stop_degrade_level = stop_degrade_level|default(0.1) -%}
{%- set stop_degrade_man = stop_degrade_man|default(False) -%}
{%- set stop_degrade_sas = stop_degrade_sas|default(False) -%}
{%- set stop_degrade_vla = stop_degrade_vla|default(False) -%}
{%- set check_port = check_port|default(False) -%}
{%- set transport = transport|default('cqudp') %}
{%- set max_degrade_speed = max_degrade_speed|default(None) -%}
{%- set manual = manual|default(False) -%}
{%- set serial_activation = serial_activation|default(False) -%}
{%- set sas_down = sas_down|default(False) -%}
{%- set man_down = man_down|default(False) -%}
{%- set vla_down = vla_down|default(False) -%}
{%- set gprepare = grepare|default(False) -%}
{%- set prepare_timeout = prepare_timeout|default(False) -%}
description: Deploy {{ conf_id }}, snapshot {{ snapshot_id }}
queue: {{ service_id }}_deploy
nanny_service_id: {{ service_id }}
tasks:
    prepare_sas:
        type: configuration_prepare
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }} . I@a_geo_sas
        prepare_shards: true
        operating_degrade_level: 1
    {%- if stop_degrade_sas %}
        stop_degrade_level: {{ stop_degrade_sas }}
    {%- else %}
        stop_degrade_level: {{ stop_degrade_level }}
    {%- endif %}
    {%- if sas_down %}
        max_fails_count: 1
        max_fails_status: DONE
    {%- endif %}
    {%- if prepare_timeout %}
        prepare_timeout: {{ prepare_timeout }}
    {%- endif %}
    prepare_man:
        type: configuration_prepare
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }} . I@a_geo_man
        prepare_shards: true
        operating_degrade_level: 1
    {%- if stop_degrade_man %}
        stop_degrade_level: {{ stop_degrade_man }}
    {%- else %}
        stop_degrade_level: {{ stop_degrade_level }}
    {%- endif %}
    {%- if man_down %}
        max_fails_count: 1
        max_fails_status: DONE
    {%- endif %}
    {%- if prepare_timeout %}
        prepare_timeout: {{ prepare_timeout }}
    {%- endif %}
    prepare_vla:
        type: configuration_prepare
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }} . I@a_geo_vla
        prepare_shards: true
        operating_degrade_level: 1
    {%- if stop_degrade_vla %}
        stop_degrade_level: {{ stop_degrade_vla }}
    {%- else %}
        stop_degrade_level: {{ stop_degrade_level }}
    {%- endif %}
    {%- if vla_down %}
        max_fails_count: 1
        max_fails_status: DONE
    {%- endif %}
    {%- if prepare_timeout %}
        prepare_timeout: {{ prepare_timeout }}
    {%- endif %}
    {%- if gprepare %}
    global_prepare:
        type: global_configuration_prepare
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        dependencies:
          - prepare_sas
          - prepare_man
          - prepare_vla
    {%- endif %}
    activate_sas:
        type: new_configuration_activate
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }} . I@a_geo_sas
        activate_timeout: 60
        {%- if operating_degrade_sas %}
        operating_degrade_level: {{ operating_degrade_sas }}
        {%- else %}
        operating_degrade_level: {{ operating_degrade_level }}
        {%- endif %}
        {% if stop_degrade_sas %}
        stop_degrade_level: {{ stop_degrade_sas }}
        {%- else %}
        stop_degrade_level: {{ stop_degrade_level }}
        {%- endif %}
        manual_confirm: {{ manual }}
        {%- if max_degrade_speed %}
        max_degrade_speed: {{ max_degrade_speed }}
        {%- endif %}
        {%- if sas_down %}
        max_fails_count: 1
        max_fails_status: DONE
        {%- endif %}
        check_port: {{ 'true' if check_port else 'false' }}
        dependencies:
            - prepare_sas
    activate_man:
        type: new_configuration_activate
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }} . I@a_geo_man
        activate_timeout: 60
        {%- if operating_degrade_man %}
        operating_degrade_level: {{ operating_degrade_man }}
        {%- else %}
        operating_degrade_level: {{ operating_degrade_level }}
        {%- endif %}
        {% if stop_degrade_man %}
        stop_degrade_level: {{ stop_degrade_man }}
        {%- else %}
        stop_degrade_level: {{ stop_degrade_level }}
        {%- endif %}
        manual_confirm: {{ manual }}
        {%- if max_degrade_speed %}
        max_degrade_speed: {{ max_degrade_speed }}
        {%- endif %}
        {%- if man_down %}
        max_fails_count: 1
        max_fails_status: DONE
        {%- endif %}
        check_port: {{ 'true' if check_port else 'false' }}
        dependencies:
            - prepare_man
            {%- if serial_activation %}
            - activate_sas
            {%- endif %}
    activate_vla:
        type: new_configuration_activate
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        filter: C@{{ conf_id }} . I@a_geo_vla
        activate_timeout: 60
        {%- if operating_degrade_vla %}
        operating_degrade_level: {{ operating_degrade_vla }}
        {%- else %}
        operating_degrade_level: {{ operating_degrade_level }}
        {%- endif %}
        {% if stop_degrade_vla %}
        stop_degrade_level: {{ stop_degrade_vla }}
        {%- else %}
        stop_degrade_level: {{ stop_degrade_level }}
        {%- endif %}
        manual_confirm: {{ manual }}
        {%- if max_degrade_speed %}
        max_degrade_speed: {{ max_degrade_speed }}
        {%- endif %}
        {%- if vla_down %}
        max_fails_count: 1
        max_fails_status: DONE
        {%- endif %}
        check_port: {{ 'true' if check_port else 'false' }}
        dependencies:
            - prepare_vla
            {%- if serial_activation %}
            - activate_man
            {%- endif %}
    global_activate:
        type: global_configuration_activate
        configuration: {{ conf_id }}
        service_id: {{ service_id }}
        snapshot_id: {{ snapshot_id }}
        transport: {{ transport }}
        dependencies:
            {%- if gprepare %}
            - global_prepare
            {%- endif %}
            - activate_man
            - activate_sas
            - activate_vla
```

{% endcut %}

В нём выкладка сервиса выполняется по локациям:

* Сначала происходит переключение сервиса в SAS (Сасово);
* Рецепт ждёт ручного подтверждения;
* Происходит переключение сервиса в MAN (Финляндия);
* Рецепт ждёт ручного подтверждения;
* Происходит переключение сервиса во VLA (Владимир).

## Рецепты сервиса {#service-recipes}

Для выкладки сервиса необходимо указать в нём два рецепта:

* Рецепт подготовки конфигурации — задаёт сценарий принесения файловых ресурсов инстанса;
* Рецепт активации конфигурации — задаёт сценарий рестарта инстансов сервиса на кластере для запуска новой ревизии сервиса.

В большинстве случае вам не должно быть нужно использовать кастомные рецепты или писать свои рецепты. Обычно должно быть достаточно стандартных рецептов сервиса.

## Структура рецепта {#recipe-structure}

Рецепт описывается следующими полями yaml-документа:

* `description` — человекочитаемое описание рецепта (необязательный параметр).
* `tasks` — список задач рецепта (обязательный параметр).

Каждая задача описывается набором общих параметров и параметров специфичных для её типа. 

Общий набор параметров:
* `type` — тип задачи 
* `dependencies` — список задач, которые должны быть завершены до выполнения данной; этот параметр задаёт структуру графа задач 
* `manual_confirm` — если `true`, задача будет выполнена только после ручного подтверждения (необязательный параметр, по умолчанию `false`); для ручного подтверждения необходимо будет нажать кнопку **Confirm** на странице задачи 
* [другие поля](http://nanny.yandex-team.ru/ui/#/alemate/tasktypes_help/) — специфичны для отдельных типов задачи

## Доступные типы задач и их поля {#task-types}

Полный список задач можно посмотреть в [Nanny](http://nanny.yandex-team.ru/ui/#/alemate/tasktypes_help/). Среди них присутствует большое число узкоспецифичных задач. А ниже приведены основные типы задач, которые используются почти во всех рецептах.

### Плавная подготовка и активация сервиса {#configuration-action}

Для плавной подготовки ресурсов сервиса используется тип задачи `configuration_prepare`.
Для плавной активации (старта новой ревизии инстансов) сервиса используется тип задачи `new_configuration_activate`.
Список поддерживаемых на текущий момент параметров этих задач одинаков. Значения параметров по умолчанию можно посмотреть [тут](https://nanny.yandex-team.ru/ui/#/alemate/tasktypes_help/):

Параметр | Значение | Описание 
:--- | :--- | :---
`filter` | настраивается вручную | параметр задаёт подмножество инстансов сервиса, которые нужно подготовить, с помощью [фильтра Блинова](https://doc.yandex-team.ru/Search/skynet-dg/concepts/syntax.html#new-syntax) 
`instance_selector` | настраивается вручную | [параметр задаёт порядок перебора инстансов](#selectors) 
`operating_degrade_level` | настраивается вручную | [допустимая доля инстансов, на которые можно одновременно доставлять ресурсы](#operating-degrade-level-desc) 
`stop_degrade_level` | настраивается вручную | [задаёт критерий успешности выполнения задачи](#stop-degrade-level-desc) 
`max_degrade_speed` | настраивается вручную | [максимальная скорость обработки инстансов](#max-degrade-speed-desc) 
`service_id` | должен быть равен `{{service_id}}` | название сервиса, конкретное значение подставляется автоматически из Nanny 
`snapshot_id` | должен быть равен `{{snapshot_id}}` | id ревизии сервиса, конкретное значение подставляется автоматически из Nanny 
`configuration` | должен быть равен `{{conf_id}}` | название конфигурации в терминах системы деплоя (ISS), конкретное значение подставляется автоматически из Nanny 
`transport` | должен быть равен `{{transport}}`  | ID инсталляции ISS, в которой нужно обрабатывать инстансы, конкретное значение подставляется автоматически из Nanny 


##### Примеры фильтров Блинова {#blinov-filter-examples}

Для понимания синтаксиса необходимо знакомство с [ документацией 1](https://doc.yandex-team.ru/Search/skynet-dg/concepts/syntax.html#new-syntax), [документацией 2](https://doc.yandex-team.ru/generated/skynet/sky/blinovcalc.html).
Для разметки инстансов используются тэги инстансов.
`C@{{ conf_id }}` — соответствует всему множеству инстансов сервиса;
`C@{{ conf_id }} . I@a_geo_sas` — соответствует подмножеству инстансов сервиса, находящихся в датацентре Сасово; (то же для `a_geo_man`, `a_geo_vla`).
`C@{{ conf_id }} . I@a_itype_backend` — соответствует множеству инстансов сервиса типа `backend`. Тип инстансов задаётся тэгом `itype` в gencfg-группе.

### Одновременная подготовка/активация сервиса {#global-configuration-action}

Для запуска одновременной подготовки ресурсов сервиса используется тип задачи `global_configuration_prepare`.
Для запуска одновременной активации (старта новой ревизии инстансов) сервиса используется тип задачи `global_configuration_activate`.

#### Для чего нужен этот тип задач? {#why-global}

В штатных условиях этот тип задачи не требуется для корректной выкладки сервиса. Однако рекомендуется всегда выставлять его последней стадией в своих рецептах. Причины для этого следующие:

1. В случае глобальных проблем может быть нужно срочно выполнить активацию новой ревизии на всех инстансах на кластере. Это можно сделать поправив рецепт или поправив пороги деградации в задаче активации сервиса, однако это может занять время. Быстрее будет вручную перевести задачу плавной активации в статус `DONE` с помощью соответствующей кнопки на странице задачи, после чего `global_configuration_activate` одновременно отправит команду активации на все инстансы сервиса;
1. В задачах плавной активации могут быть заданы множества инстансов сервиса, объединение которых не охватывает все инстансы сервиса (из-за человеческой ошибки в рецепте). В этом случае активация забытых инстансов также будет выполнена на стадии `global_configuration_activate`.
Те же самые причины относятся к типу задач `global_configuration_prepare`.

Список поддерживаемых на текущий момент параметров этих задач одинаков:

Параметр | Значение | Описание 
:--- | :--- | :---
`service_id` | должен быть равен `{{service_id}}` | название сервиса, конкретное значение подставляется автоматически из Nanny   
`snapshot_id` | должен быть равен `{{snapshot_id}}` | id ревизии сервиса, конкретное значение подставляется автоматически из Nanny   
`configuration` | должен быть равен `{{conf_id}}` | название конфигурации в терминах системы деплоя (ISS), конкретное значение подставляется  автоматически из Nanny   
`transport` | должен быть равен `{{transport}}`  | ID инсталляции ISS, в которой нужно обрабатывать инстансы, конкретное значение подставляется автоматически из Nanny  

## Управление порогами деградации {#operating-degrade-level}

#### Почему зависают выкладки? {#why-deployment-is-failed}

В процессе выкладки Alemate/Nanny запускает рестарт инстансов сервиса. В рестарт отправляется небольшая доля инстансов, которая задаётся параметром рецепта выкладки. Если инстансы, отправленные в рестарт, не поднимутся, выкладка не пойдёт дальше, и **зависнет**. Зачем нужно это ограничение, можно посмотреть [ниже](#why-control-degradation).

Причины того, что инстанс не поднимается, могут быть разные:

* Ошибка в коде выкатываемого релиза. В этом случае не следует продолжать выкатку, а правильно наоборот откатиться на предыдущий релиз;
* Проблемы с железом, на котором стартует инстанс. В этом случае может быть полезно увеличить долю инстансов для отправки в рестарт, если оставшиеся мощности позволяют это сделать;
* Проблемы с инфраструктурными сервисами, на машинах, где стартуют инстансы. Например, сломано porto или ISS-агент. В этом случае может быть полезно увеличить долю инстансов для отправки в рестарт, если оставшиеся мощности позволяют это сделать.

Обычно исправить зависание выкладки можно подняв разрешённое число инстансов, которые можно одновременно отправить в рестарт. Делать это нужно аккуратно, чтобы не отправить в рестарт одновременно слишком много инстансов и не увести сервис в downtime. Как это сделать, описано [ниже](#how-to-update).

#### Зачем это нужно? {#why-control-degradation}

**Пример 1.** При выкатке новой версии бинарника инстанса происходит его рестарт. Инстанс на хосте не может обрабатывать входящие запросы с момента завершения процесса старой версии бинарника до момента готовности новой версии. На протяжении этого промежутка времени инстанс называется деградировавшим. Если запустить рестарт одновременно на всех инстансах сервиса, то сервис в целом не сможет обрабатывать запросы, что приведёт к даунтайму. Для избежания этой проблемы alemate имеет параметры для управления долей инстансов, которые можно одновременно привести в деградировавшее состояние.

**Пример 2.** Сервис состоит из большого числа инстансов, которые требуют принесения очень тяжёлых ресурсов (не менее десятков GB). В такой ситуации может возникать ситуация, что одновременная доставка этих ресурсов на все инстансы сервиса перегружает сеть. Эта проблема является не частой и свойственна в основном сложным сервисам (web-поиск, поиск по картинкам, видео etc), для её решения также следует использовать описанные ниже параметры.

#### Параметры управления деградацией {#degradation-params}

##### operating_degrade_level {#operating-degrade-level-desc}

`operating_degrade_level` — максимальная доля инстансов, которую можно одновременно отправить рестарт (одновременно запустить доставку данных в случае с задачей `configuration_prepare`). Задаётся в долях единицы, например, `0.1`, `0.15`, etc.

**Пример.**

1. Пусть всего в сервисе `100` инстансов;
1. Пусть в задаче `new_configuration_activate` задан `operating_degrade_level = 0.1`;
1. В этом случае одновременно в рестарт будет отправлено не более, чем `100 * 0.1 = 10` инстансов;
1. Как только один из инстансов из обрабатываемой десятки готов, в рестарт отправляется ещё один, и так далее.

**Замечание**

1. Число машин, отправляемых в обработку, округляется вниз. Например, если в сервисе `25` инстансов и `operating_degrade_level = 0.1`, то в обработку будет отправлено не более чем 2 инстанса (`floor(25 * 0.1) = 2`);
1. Если `operating_degrade_level` слишком мал для того, чтобы взять в обработку хотя бы один инстанс (например, инстансов 5, `operating_degrade_level = 0.1`), то число инстансов, которые берутся в обработку, будет увеличено. Значение, до которого будет поднят `operating_degrade_level` зависит от используемого [селектора инстансов](#selectors). При похостовом переключении (`instance_selector: host_selector`), округление вверх будет произведено до максимального числа инстансов, находящихся на одном хосте. При поинстансном переключении (`instance_selector: instance_selector`) округление вверх будет сделано до одного инстанса.

##### stop_degrade_level {#stop-degrade-level-desc}

`stop_degrade_level` — максимальная допустимая доля ошибок, после которых мы будем считать, что задача все равно выполнена успешно.
Например, если у нас всего 1000 инстансов, а `stop_degrade_level` == 0.1, то даже если на 100 из них задача завершилась неудачей, мы все равно будем считать что в целом задача выполнилась успешно.

##### max_degrade_speed {#max-degrade-speed-desc}

`max_degrade_speed` — доля инстансов в секунду, которую можно отправить в рестарт. Этот параметр используется для растяжки выкатки сервиса по времени. Параметр ограничивает скорость, с которой запускается в рестарт максимально допустимое число инстансов. Этот параметр работает **вместе** с параметром `operating_degrade_level` и не исключает, а дополняет его. Параметр гарантирует, что общая длительность выкладки составит не менее `1.0 / max_degrade_speed` секунд.

**Пример 1**

1. Пусть в сервисе `100` инстансов;
2. Пусть в задаче `new_configuration_activate` задан `operating_degrade_level = 0.1`;
3. Пусть в задаче задан `max_degrade_speed = 1.0`. Это означает, что в секунду в рестарт можно отправить максимально допустимое количество инстансов;
4. Тогда в первую же секунду в рестарт будут отправлены `100 * 0.1 = 10` инстансов;
5. Как только один из инстансов из обрабатываемой десятки готов, в рестарт отправляется ещё один, и так далее.

**Пример 2**

1. Пусть в сервисе `100` инстансов;
1. Пусть в задаче `new_configuration_activate` задан `operating_degrade_level = 0.1`;
1. Пусть в задаче задан `max_degrade_speed = 0.001`. Это означает, что инстансы можно отправлять в рестарт со скоростью не более, чем `100 * 0.001 = 0.1` в секунду;
1. Тогда в первую же секунду в рестарт будут отправлен один инстанс;
1. Через десять секунд в рестарт будет отправлен второй инстанс;
1. ...
1. Через 100 секунд в рестарт уйдут 10 инстансов;
1. Следующий (11-ый) инстанс будет отправлен в рестарт сразу же, как только будет готов один из инстансов, но не раньше, чем ещё через 10 секунд (т.е. через 110 секунд после запуска всей задачи).

#### Как поднять пороги деградации? {#how-to-update}

##### Поднять пороги только у запущенной выкладки {#update-existing-deployment}

Иногда бывает необходимо разово поднять пороги деградации запущенной выкладки так, чтобы не затронуть при этом все последующие выкладки. Например, если прямо сейчас сервис в разломанном состоянии и нужно срочно рестартнуть все инстансы одновременно, но при дальнейших выкладках делать этого не хочется.

Для этого нужно использовать кнопку `Degrade levels` на странице задачи активации инстансов.

![img](https://jing.yandex-team.ru/files/sshipkov/2017-02-2017-08-55.450991f.png)

В поле `operating_degrade_level` нужно указать долю инстансов, которые можно одновременно отправить в рестарт. Например, пусть всего в сервисе 10 инстансов, при этом 4 из них можно рестартить одновременно. `operating_degrade_level = 4 / 10 = 0.4`. Подробнее параметр описан [выше](#operating-degrade-level-desc).

В поле `stop_degrade_level` нужно указать долю неподнявшихся инстансов, после которой можно считать активацию успешной. Например, пусть всего в сервисе 10 инстансов, при этом достаточно, если живы из них будут тольо 8. Тогда `stop_degrade_level = (10 - 8) / 10 = 2 / 10 = 0.2`. Подробнее параметр описан [выше](#stop-degrade-level-desc).

![img](https://jing.yandex-team.ru/files/sshipkov/2017-02-2017-13-09.00c0584.png)

##### Поднять пороги только у последующих выкладок {#update-existing-and-new-deployments}

Чтобы поднять пороги деградации у всех последующих выкладок сервиса, необходимо поправить настройки рецептов сервиса. Для этого нужно открыть `Service -> Recipes` и внести в рецепт подготовки/активации новые значения параметров деградации. При этом **текущая выкладка не будет затронута**. Как поменять пороги деградации у текущей выкладки см. [выше](#update-existing-deployment).


## Порядок перебора инстансов {#selectors}

Для выкладки сервиса его инстансы отправляются в рестарт в некотором порядке. Этот порядок фиксирован и не меняется при выкладках разных релизов одного и того же сервиса, **если при этом список его инстансов остаётся постоянным (т.е. остаются постоянными его gencfg-группы)**. Порядок перебора инстансов задаётся параметром  `instance_selector`.

#### Перебор инстансов по хостам {#host-selector}

Используется при выборе параметра задачи активации/подготовки конфигурации `instance_selector: host_selector`.

1. Инстансы упорядочиваются фиксированным случайным образом (с постоянным `seed`);
1. Если максимальное число инстансов, живущих на одном хосте превосходит `operating_degrade_level`, то он будет неявно поднят до максимального числа инстансов, живущих на одном хосте. Пример: `operating_degrade_level: 0.1`, всего в конфигурации 4 хоста, на каждом живёт по 2 инстанса. Тогда `operating_degrade_level` будет поднят до `0.25`, т.к. иначе нет возможности отправить в рестарт ни одного хоста.
1. Далее при выкладке инстансы отправляются в рестарт **похостово**;

**Пример.**

1. Пусть сервис имеет по 2 инстанса на каждом из 4 хостов. Общее количество инстансов 8;
1. Пусть `operating_degrade_level = 0.375`. `8 * 0.375 = 3`, т.е. одновременно в даунтайме может находиться не больше трёх инстансов;
1. При этом `operating_degrade_level` не позволяет отправить в рестарт инстансы сразу двух хостов. Выкладка сервиса будет происходить так:
* В рестарт отправляются оба инстанса первого хоста;
* Как только поднялся первый инстанс из двух, в рестарт отправляются оба инстанса второго хоста;
* Общее число инстансов в даунтайме при этом становится равным `3`.
* После того, как поднимется ещё один инстанс (общее количество инстансов в даунтайме станет равно `2`), третий хост **не будет** отправлен в рестарт;
* После того, как поднимется ещё один инстанс (общее количество инстансов в даунтайме станет равно `1`), третий хост **будет** отправлен в рестарт.
* ...

Это поведение сейчас используется **по умолчанию**.


####  Перебор инстансов без учёта хостов {#instance-selector}

Используется при выборе параметра задачи активации/подготовки конфигурации `instance_selector: instance_selector`.

1. Инстансы упорядочиваются фиксированным случайным образом (с постоянным `seed`);
1. Далее при выкладке инстансы отправляются в рестарт без учёта хостов.
Если на хосте живёт несколько инстансов сервиса, то какая-то их часть может быть отправлена в рестарт в самом начале выкладки, а оставшаяся часть — в самом конце.

#### Шардированное переключение {#sharded-selectors}

Используется при выборе одного из двух значений параметра:

* `instance_selector: sharded_host_selector`;
* `instance_selector: sharded_instance_selector`.
Подробнее описано на соответствующей [странице документации](../../how-to/yp-lite-shards.md).

## Параметры рецепта {#parameters}

Перед выполнением рецепта будет произведен его рендеринг с помощью Jinja2, yaml-рецепты поддерживают все языковые конструкции этого движка.

Самый простой вариант использования параметров: вставка значения по имени, для этого в теле рецепта нужно вставить `{{ parameter }}`, при рендеринге эта строка будет заменена значением переданного параметра по имени `parameter`.

## Больше примеров {#more-samples}

Ознакомиться с примерами рецептов, которые уже есть в репозитории, можно удобно через [Nanny](http://nanny.yandex-team.ru/ui/#/alemate/recipes/).

## Как запустить рецепт? {#how-to-apply}

Через [ReST API Nanny](alemate-api.md).

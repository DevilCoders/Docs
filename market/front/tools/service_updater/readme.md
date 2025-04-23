Скрипты массового обновления сервисов Маркета
========================================

Установка (SVN)
--------

```bash
ya make --checkout market/front/tools/service_updater/repl
```

После этого repl-интерфейс будет доступен как `market/front/tools/service_updater/repl/repl`

Установка (ARC)
---------

```shell
cd arc/arcadia/market/front/tools/service_updater/repl
ya make
```

После этого в данной директории будет доступен исполняемый файл `./repl`

Что это и для чего
----------------

Это набор скриптов для быстрого и удобного деплоя изменений в RTC-сервисах + repl для простого управления этим процессом.

Зачастую возникают ситуации, в которых требуется изменять описание сервисов (обновление секретов, обновление ресурсов, смена настроек в instanceSpec и т.д.). Проделывать подобные изменения через веб-интерфейс достаточно сложно, неудобно, долго и ненадёжно. С другой стороны использовать низкоуровневые клиенты для того, чтобы делать это из консоли - ещё менее надёжно и зачастую горздо более неудобно. Данная библиотка призвана решить подобный недостаток.

Состав:

  - `lib/runner.py` - тут происходит магия. Это скрипт осуществляющий выкатку и взаимодействие с пользователем (вывод логов, запрос подверждения и т.д.)
  - `lib/deployment.py` - описание цели деплоя - некое окружение некого дашборда + фильтры специальных сервисов типа kraken, sample, content-preview, canary
  - `lib/service.py` - описание отдельного сервиса
  - `lib/clients.py` - более низкоуровневые клиенты используемы под капотом
  - `lib/abc.py` - различные словари (названия окружений, дашбордов, специальных типов сервисов и т.д.)
  - `helpers/instance_spec.py` - готовые скрипты для типичных операций по изменению instanceSpec'а
  - `helpers/resources.py` - готовые скрипты для типичных операций по изменению ресурсов
  - `helpers/layers.py` - готовые скрипты для типичных операций по изменению базовых слоёв
  - `helpers/tickets.py` - готовые скрипты для типичных операций по изменению tickets integration
  - `scenarios/*` - готовые сложные сценарии обновлений см. [scenarios/readme.md](scenarios/readme.md)

Примеры использования
-------------------

```python
runner = updater.Runner()

runner.deploy(
    'Deploy like-a-boss',
    lambda service: helpers.update_or_create_file_resource(service, 'readme.txt', 'deployed like-a-boss')
)

runner.deploy(
    'Deploy like-a-boss next resource',
    lambda service: helpers.update_or_create_file_resource(service, 'deleteme.txt', 'deployed like-a-boss again')
)
```

Или более прицельно:

```python
runner = updater.Runner(envs=[
    updater.DashboardEnv.testing,
    updater.DashboardEnv.prestable,
    updater.DashboardEnv.production,
], dashboards=[
    updater.Dashboard.white_desktop,
    updater.Dashboard.white_touch,
    updater.Dashboard.white_fapi
], special_types=[
    updater.SpecialServiceType.canary,
], only_special=False)

runner.deploy(
    'Deploy like-a-boss',
    lambda service: helpers.update_or_create_file_resource(service, 'readme.txt', 'deployed like-a-boss')
)
```

Или используя сокращённый синтаксис:

```python
updater.Runner.deploy_all(
    'Deploy like-a-boss',
    lambda service: helpers.update_or_create_file_resource(service, 'readme.txt', 'deployed like-a-boss'),
    envs=[
        updater.DashboardEnv.testing,
        updater.DashboardEnv.prestable,
        updater.DashboardEnv.production,
    ],
    dashboards=[
        updater.Dashboard.white_desktop,
        updater.Dashboard.white_touch,
        updater.Dashboard.white_fapi
    ],
    special_types=[
        updater.SpecialServiceType.canary,
    ],
    only_special=False
)
```

Или совсем прицельно:
```python
updater.Runner.deploy_single(
    'Deploy like-a-boss',
    lambda service: helpers.update_or_create_file_resource(service, 'readme.txt', 'deployed like-a-boss'),
    updater.ListDeployment(['first_service_id', 'second_service_id'])
)
```


Спецификация
-----------

**mutator**

Встречается в качестве аргумента во многих местах. Это функция которая принимает в качестве единственного аргумента сервис (объект класса `market.sre.tools.rtc.nanny.models.service.Service`) и производит над ним изменения. Данный скрипт обязан производить идемпотентные изменения иначе будет брошено исключение.

staticmethod **Runner.deploy_single(description, mutator, deployment)**

Деплой одной цели. Процесс выкатки состоит из 3х этапов:
  - ожидание готовности сервисов (не деплоим когда что-то другое уже деплоится)
  - подготовка изменений и запуск изменений
  - ожидание завершения деплоя (мониторим что всё успешно завершилось и не требуется ручного вмешательства)

staticmethod **Runner.deploy_all(description, mutator, envs, dashboards, special_types, only_special)**

Массовый деплой. По-умолчанию включает все сервисы во всех окружениях. Выкатывает сначала тестинг, затем престейбл и после этого прод.

Параметры envs, dashboars, special_types принимают на вход массивы и являются необязательными (по умолчанию содержат максимальный набор)

Параметр only_special опциональный и позволяет отключать деплой не на специальные окружения (т.е. например с помощью этого параметра можно выкатить что-то только на канарейку, указав её в списке special_types)

**Runner(envs, dashboards, special_types, only_special)**

Конструктор для многоразового использования.

**Runner#deploy(description, mutator)**

Аналогично вызову `Runner.deploy_all` с параметрами переданными в конструктор данного инстанса.

staticmethod **Deployment.get_services_list(dash_id, envs, special_types, only_special)**

Получение списка сервисов по названию дашборда, окружениям и специальным типам. Возвращет массив объектов `lib.Service`

**Deployment(services_list)**

Конструктор класса (базовый класс). Принимает список сервисов в виде OrderedList, где ключ - имя сервиса, а значение - сервис

**ListDeployment(services_list)**

Конструктор класса. Принимает список сервисов в виде списка айдишников

**DashDeployment(dash_id, envs, special_types, only_special)**

Конструктор класса. Принимает те же параметры что и `Deployment.get_services_list`

**DashDeployment#link**

Ссылка на дашборд в няне (к сожалению нет детализации по окружению и специальным типам - няня так не умеет)

**DashDeployment#description**

Ссылка на дашборд с доп-описанием какое окружение используется

**Deployment#services**

Список сервисов

**Deployment#pending**

Список выкатывающихся сервисов. Словарь, ключи - название сервиса, значения - `lib.Service`.

**Deployment#hostnames**

Список хостов с разбивкой по сервисам (словарь, ключи - название сервисов, значения - массивы названий хостов)

**Deployment#prepare(mutator)**

Подготовка сервисов (применение изменений без выкатки куда-либо)

**Deployment#deploy(description)**

Выкатка изменений (перед этим требуется сделать `Deployment#prepare`). Возвращает результат `Deployment#wait_for_release()`

**Deployment#status(pending)**

Получение списка статусов сервисов. По-умолчанию отображатеся только статус сервисов которые изменены и выкатываются. Если передать `pending=False`, будет отображаться статус всех сервисов

**Deployment#wait_for_ready()**

Ожидание готовности сервисов к выкатке. В случае если происходит таймаут ожидания возвращает массив сервисов в которых произошёл таймаут.

**Deployment#wait_for_release()**

Ожидание завершения выкатки. Является генератором. Возвращает объект `lib.Service`, когда тот переходит в состояние ONLINE. Если происходит таймаут, бросает исключение.

staticmethod **Service.special_type(service_id)**

Возвращает специальный тип сервиса, если такой есть (kraken, canary, sample, content-preview)

staticmethod **Service.is_banned(service_id)**

Проверка, что сервис должен быть безусловно исключен из списка деплоя (сейчас применяется к xscript-сервисам)

**Service(service_id)**

Конструктор.

**Service#special_type**

Специальный тип сервиса.

**Service#status**

Возвращает текущий статус сервиса

**Service#prepared**

Объект `market.sre.tools.rtc.nanny.models.service.Service` - появляется после вызова `Service#prepare()`.

**Service#updated**

Объект `market.sre.tools.rtc.nanny.models.service.Service` - появляется после вызова `Service#update()`. Наличие данного поля означает, что создан снепшот в няне.

**Service#activated**

Объект `market.sre.tools.rtc.nanny.models.service.Service` - появляется после вызова `Service#activate()`. Наличие данного поля означает, что запущена активация снепшота в няне (не означает что он успешно завершился).

**Service#prepare(mutator)**

Подготовка изменений в сервисе.

**Service#update(description)**

Создание снепшота с изменениями в няне

**Service#activate()**

Запуск выкатки снепшота в няне.

**helpers.***

Хелперы для стандартных действий над сервисами. Все названия достаточно точно описывают, что хеплеры делают. Праметры тоже достаточно очевидны, кроме matcher'а и ti_matcher. matcher - это функция, в которую передаётся name и command и она должна возвращать True/False. ti_matcher - это фукнция, в которую передаётся тип таски и тип ресурса, должна возвращать True/False, используется в Tickets Integration

  - `find_prepare_script(service, matcher)` - поиск prepare секции в instanceSpec
  - `update_or_create_prepare_script(service, matcher, name, script)`
  - `update_prepare_script(service, matcher, name, script)`
  - `remove_prepare_script(service, matcher)`
  - `find_container_script(service, matcher)` - поиск основной секции в instanceSpec
  - `update_container_script(service, matcher, name, script)`
  - `remove_container_script(service, matcher)`
  - `get_dynamic_resource_script(service)` - возвращает скрипт обновления динамических ресурсов
  - `update_dynamic_resource_script(service, command)`
  - `update_layer(service, resource)`
  - `find_sandbox_resource(service, resource)` - ищет сендбокс ресурс по resource_type
  - `get_resource_by_filename(service, filename)` - ищет ресурс по названию файла
  - `update_or_create_file_resource(service, filename, contents)`
  - `remove_file_resource(service, filename)`
  - `update_or_create_sandbox_resource(service, filename, resource, is_dynamic, is_juggler_bundle)`
  - `remove_sandbox_resource(service, filename)`
  - `find_tickets_integration(service, ti_matcher)`
  - `update_or_create_tickets_integration(service, ti_matcher, task_type, resource_type, description, evn_filter, queue)`
  - `update_tickets_integration(service, ti_matcher, task_type, resource_type, description, evn_filter, queue)`
  - `remove_ticket_integration(service, ti_matcher)`
  - `env_filter_by_service(service)` - хелпер для env_filter. По id сервиса возвращает testing/prestable/stable

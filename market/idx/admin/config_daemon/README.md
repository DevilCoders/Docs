## Конфиг-демон

Микросервис-дополнение для быстрых конфигов индексатора

Корневой тикет [MARKETTECH-873](https://st.yandex-team.ru/MARKETTECH-873)

#### Как воспользоваться:

Для работы с ZooKeeper у IDXAPI есть специальная ручка `override_config` , которая позволяет изменить быстрый конфиг (значение доезжает мгновенно):

#### Веб-интерфейс с удобным управлением

Можно зайти на хосты idxapi, например, по следующим адресам:

Для управления конфигами прода:

http://idxapi.market.yandex.net:29334/v1/override_config

http://ps01h.market.yandex.net:29334/v1/override_config 

Для управления конфигами тестинга:

http://ps01ht.market.yandex.net:29334/v1/override_config

#### Проставление значения конфига

Структура запроса:

`[/<version>]/override_config/set?zk-path=<zk_path>&user=<user>&reason=<reason>&section=<section>&option=<option>&value=<value>[&section=<section>&option=<option>&value=<value>&...]`

- `zk-path` - путь в ZooKeeper, по которому будет сохранен конкретный конфиг
- `user` и `reason` - поля для идентификации пользователя, который изменяет конфиг и причины изменения
- `section`, `option` и `value` - секция, параметр и новое значение конфига соответственно (можно указать произвольное число значений)

Особенности:

- Для каждого параметра нужно указывать его секцию (для корректной связи секция - параметр)
- Если по переданному пути в ZooKeeper'е нет данных, то там создается новый конфиг
- Нельзя проставлять один и тот же параметр (внутри одной секции) несколько раз
- В curl нужно передать `--request POST/PUT`

#### Удаление параметра конфигов

Структура запроса:

`[/<version>]/override_config/remove?zk-path=<zk_path>&user=<user>&reason=<reason>&section=<section>&option=<option>[&section=<section>&option=<option>&...]`

- `zk-path`, `user`, `reason`, `section`, `option` - аналогично

Особенности:

- Для каждого параметра нужно указывать его секцию (для корректной связи секция - параметр)
- Нельзя удалять один и тот же параметр (внутри одной секции) несколько раз
- Если не указать параметры конфига, то конфиг (если существует) будет удален полностью по переданному пути
- В curl нужно передать `--request DELETE` и указать `--user`

#### Рекурсивное удаление параметра конфига

```[/<version>]/override_config/remove_recursive?zk-path=<zk-path>&user=<user>&reason=<reason>&section=<section>&option=<option>```

- `zk-path`, `user`, `reason`, `section`, `option` - аналогично

Особенности:

- Удаление параметра конфига по всем дочерним путям в структуре хранения конфигов ZooKeeper-а
- В curl нужно передать `--request DELETE` и указать `--user`

#### Вывод параметров конфига

Структура запроса:

`[/<version>]/override_config/show?zk-path=<zk-path>`

- `zk-path` - путь в ZooKeeper, по которому лежит конфиг

Особенности:

- Вывод в формате json

#### Вывод структуры хранения конфигов

Структура запроса:

```[/<version>]/override_config/show_structure?zk-path=<zk-path>```

- `zk-path` - путь конфига в ZooKeeper

Особенности: 

- Древовидный вывод дочерних путей относительно пути из запроса

#### Вывод более глубоких путей, по которым указанный конфиг переопределяется

Структура запроса:

``` [/<version>]/override_config/check_option_override?zk-path=<zk-path>&section=<section>&option=<option>```

- `zk-path` - путь конфига в ZooKeeper
- `section` - секция параметра
- `option` - название параметра

Особенности:

- Вывод путей полных путей построчно

#### Как выбрать zk-path?

Пути имеют следующий формат: `/fast_config/name/env/mitype[/dc]`, где:

- `name` - название потребителя быстрых конфигов, например, idxapi
- `env` - testing или production
- `mitype` - в привычном понимании, например stratocaster/gibson/yellow.stratocaster
- `dc` - датацентр (пока никак не используется)

**Особенность** - при движении от корня параметры конфига затираются новыми при их повторении

Записать конфиг можно в любую вершину пути. Например, если потребуется проставить значение параметра конфига для IDXAPI-а во всем проде, то его нужно записать по пути `/fast_config/idxapi/production`.

При этом в вершинах уровня `mitype` или `dc` это значение можно будет переопределить.

#### Что происходит дальше?

Только что проставленное значение будет считано **конфиг-демоном** и записано в файл `local.ini.override` в директорию с остальными конфигами. Каждый интегрированный сервис считывает конфиги в порядке `common.ini` -> `local.ini` -> `local.ini.override`, поэтому быстрые конфиги будут иметь наивысший приоритет.

Поскольку быстрые конфиги разрабатывались для экстренных ситуаций, когда требуется изменить конфиг уже во время работы сервиса, то в новом релизе **лучше добавить новое значение в локальный конфиг**, тогда его будет сложнее потерять (хотя уже сейчас в лог IDXAPI попадает информация о причине изменения конфига)

#### Примеры использования:

При работе с быстрыми конфигами нужно руководствоваться тем, что по мере удаления от корня конфиги в путях могут затирать друг друга при необходимости. Представим, что изначально по пути `/fast_config/idxapi/production/` лежит значение параметра `blue_market.log_path`. Оно будет общим для всех **mitype**-ов. Но если для **gibson** потребуется переопределить это значение, то это можно прописать по пути `/fast_config/idxapi/production/gibson`, не удаляя при этом параметр из `/fast_config/idxapi/production/`.

Также стоит учитывать, что сервера ZooKeeper-а для тестинга и продакшена разные, т.е. все изменения через ps01ht будут работать только в тестинге.

1. **Узнаем структуру быстрых конфигов в ZooKeeper**

   Пример:

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request GET "http://ps01ht.market.yandex.net:29334/v1/override_config/show_structure?zk-path=/fast_config/"
   |-- idxapi
   |   |-- production
   |   |   |-- gibson
   |   |-- testing
   |       |-- planeshift.balalaika-ps02ht
   |       |-- stratocaster
   |-- offers-robot2
       |-- testing
           |-- yellow.stratocaster
   ```

   Пусть нам нужно проставить значение параметра "**testing_section.testing_option**" для всего сервиса **IDXAPI**.

2. **Проверим, что значение параметра не переопределяется на более глубоких уровнях**

   Для этого воспользуемся ручкой **check_option_override**, пример:

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request GET "http://ps01ht.market.yandex.net:29334/v1/override_config/check_option_override?zk-path=/fast_config/idxapi&section=testing_section&option=testing_option"
   List of deeper ZooKeeper paths where "testing_section.testing_option" is overwritten:
   /fast_config/idxapi/production
   /fast_config/idxapi/production/gibson
   /fast_config/idxapi/testing
   /fast_config/idxapi/testing/stratocaster
   ```

   Далее нужно решить: а нужны ли переопределенные значения на более глубоких уровнях? Для принятия решения может пригодиться сходить по этим путям и посмотреть, какими именно значениями параметр там переопределяется.

3. **Посмотрим на значения параметра по интересующим нас путям**

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request GET "http://ps01ht.market.yandex.net:29334/v1/override_config/show?zk-path=/fast_config/idxapi/testing"
   {
       "testing_section": {
           "testing_option": "testing_value"
       }, 
       "testing_section1": {
           "testing_option1": "testing_value0"
       }, 
       "testing_section2": {
           "testing_option2": "testing_value2"
       }
   }
   ```

4. **Рекурсивно удалим переопределения конфига на более глубоких путях**

   Пусть мы решили удалить все более глубокие переопределения параметра для тестинга. Тогда воспользуемся ручкой **remove_recursive**:

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request DELETE --user evgenabramov "http://ps01ht.market.yandex.net:29334/v1/override_config/remove_recursive?user=evgenabramov&reason=testing&zk-path=/fast_config/idxapi/testing&section=testing_section&option=testing_option"
   Enter host password for user 'evgenabramov':
   ok
   ```

   Теперь если мы посмотрим переопределения конфига, как во 2 пункте, то увидим, что указаные пути пропали:

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request GET "http://ps01ht.market.yandex.net:29334/v1/override_config/check_option_override?zk-path=/fast_config/idxapi&section=testing_section&option=testing_option"
   List of deeper ZooKeeper paths where "testing_section.testing_option" is overwritten:
   /fast_config/idxapi/production
   /fast_config/idxapi/production/gibson
   ```

5. **Запишем значение параметра по выбранному пути:**

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request POST "http://ps01ht.market.yandex.net:29334/v1/override_config/set?zk-path=/fast_config/idxapi&user=evgenabramov&reason=testing&section=testing_section&option=testing_option&value=new_testing_value"
   ```

   Теперь по пути лежит новое значение, проверим это:

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request GET "http://ps01ht.market.yandex.net:29334/v1/override_config/show?zk-path=/fast_config/idxapi"
   {
       "idxapi_section1": {
           "idxapi_option1": "idxapi_value1", 
           "idxapi_option2": "idxapi_value2"
       }, 
       "idxapi_section2": {
           "idxapi_option2": "idxapi_value2"
       }, 
       "testing_section": {
           "testing_option": "new_testing_value"
       }
   }
   ```

6. **Если нужно удалить сразу несколько параметров по конкретному пути:**

   ``` 
   evgenabramov-x:idxapi evgenabramov$ curl --request DELETE --user evgenabramov "http://ps01ht.market.yandex.net:29334/v1/override_config/remove?zk-path=/fast_config/idxapi&user=evgenabramov&reason=testing&section=idxapi_section1&option=idxapi_option2&section=idxapi_section2&option=idxapi_option2"
   Enter host password for user 'evgenabramov':
   ok
   ```

   Проверим, что получилось:

   ```
   evgenabramov-x:idxapi evgenabramov$ curl --request GET "http://ps01ht.market.yandex.net:29334/v1/override_config/show?zk-path=/fast_config/idxapi"
   {
       "idxapi_section1": {
           "idxapi_option1": "idxapi_value1"
       }, 
       "testing_section": {
           "testing_option": "new_testing_value"
       }
   }
   ```

При этом можно быть уверенным, что прописанный конфиг будет записан в файл `local.ini.override`, а сервис сразу узнает об обновлении конфига и перезапустится. Интервал оповещения можно задать в `etc/common.ini` в параметре `fast_config.refresh_interval` (подробности ниже). 

Кроме того, конфиг не перезатрется следующим релизом, поскольку конфиги ZooKeeper имеют наивысший приоритет.

#### Особенности конфиг-демона:

1. Запускается вместе с основным сервисом (бинарник приходит с debian-пакетом или как отдельная секция в RTC)

2. В реальном времени ходит в междатацентровый ZooKeeper и проверяет наличие быстрых конфигов по путям со следующим форматом (см. [обсуждение формата](https://st.yandex-team.ru/MARKETINDEXER-30149)): 

   `/fast_config/name/env/mitype[/dc]`, где:

   - `name` - название потребителя быстрых конфигов, например, idxapi

   - `env` - testing или production

   - `mitype` - в привычном понимании, например stratocaster/gibson/yellow.stratocaster

   - `dc` - датацентр (пока никак не используется)

   **Особенность** - при движении от корня параметры конфига затираются новыми при их повторении

3. Если конфиг поменялся после последней проверки, записывает его в файл `local.ini.override` в папку с конфигами и посылает `SIGHUP` основному сервису, у которого есть обработка с обновлением конфига и последующим перезапуском
4. Умеет работать c разными форматами конфигов:
   - `ConfigParser` - форматом (как, например, в Offers-robot2) 
   - `yaconf` (как в IDXAPI)
5. Работает на железных машинах и в RTC
6. Для своей работы обязательно требует уточнения следующих параметров в секции `fast_config` ini-конфига:
   - `zk-path` - шаблонизированный путь в ZooKeeper (например, `/fast_config/idxapi/{env}/{mitype}`)
   - `refresh_interval` - время в секундах между чтением конфига в ZooKeeper
   - `setup_time` - время в секундах, необходимое для запуска основного сервиса. (Важный параметр, поскольку если сервис запустился не до конца и обработка сигнала не была настроена, то по сигналу `HUP` он может сразу упасть)
7. Решает проблему с необходимостью ожидания нового релизного пайплайна для обновления конфигов, поскольку есть возможность быстро записать данные в ZooKeeper (см. ниже)
8. Имеет [yatf-тесты](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/admin/config_daemon/yatf) со всеми необходимыми ресурсами, подключением к серверам ZooKeeper-а и сигнальным взаимодействием с потребителем 

Для взаимодействия с ZooKeeper удобно использовать специальные ручки IDXAPI ([код](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/api/backend/blueprints/override_config.py))

Код можно посмотреть [здесь](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/admin/config_daemon).

Уже реализовано в:

- [IDXAPI](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/api/backend/idxapi.py?rev=5509962#L152)
- [Offers-robot2](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/feeds/robot/offersrobot/robot.py?coverage=true&rev=5558811#L146)
- [Datacamp (Parser)](https://a.yandex-team.ru/arc/trunk/arcadia/market/idx/datacamp/parser/lib/service.py?rev=5640012#L93)

В планах интеграция с:

- DataCamp (Stroller, Routines, Piper, Miner)
- MarketIndexer
- YellowIndexer
- Picrobot

Дальнейшее развитие:

1. Валидация значений, устанавливаемых в **user** и **reason**
2. Мониторинги работы конфиг-демона в Juggler'е
3. Нотификация в telegram при установке быстрых конфигов
4. Интеграция с интерфейсом ЦУМа


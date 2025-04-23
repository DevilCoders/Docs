# Solomon-pusher переехал в аркадию, sandbox и реактор
## Migration guide
Порядок работы стал следующим:
1. Коммитим новый SQL в [аркадию](https://a.yandex-team.ru/arc/trunk/arcadia/market/solomon-pusher/)
2. В [реакторе](https://reactor.yandex-team.ru/browse?rootId=596061&selected=596061), в нужном сервисе создаем соответствующую реакцию. Помимо необходимых полей, нужно заполнить уведломления в __Notifications__: фейл и крит по длительности. Канал - `Telegram chat`, имя чата - `SolomonPusherNotifications`. Если имя чатега не подсказывается, нужно присоединиьться к https://t.me/joinchat/DHuS-UZzQ8zSV_iK_F6tOA и попробовать еще разок
3. Profit

При изменении sql никаких действий кроме коммита не требуется. Сразу после мержа таски будут использовать обновленный

### Маппинг на пушер из браавоса
#### PUSH_SOLOMON_SENSORS
Бывший `[push-sensor-value.py]`
__Inputs:__
* `path_to_sql` - открыть в sql в аркадии и скопировать путь целиком
* `is_testing` - если проставить галочку сенсоры будут отправляться в кластер `testing` соломона (если новый сервис - необходимо его предварительно в соломоне создать в тестовом кластере)
* `use_date_range` - в sql в первыйе 2 $ подставятся время и дата предыдущего запуска и сейчас, работает как `load_date_sh`
* `additional_sql_args` - почему то в реакторе не отбражается параметр, ищу другие пути. В идеальном мире - параметры, которые можно передать в sql, если стоит галочка про даты, то пойдут с третьего $, иначе с первого

#### Остальные
`CREATE_ST_TICKETS_FROM_SENSORS` - StarTrek
`POST_SENSORS_VIA_HTTP` - HTTP
`SEND_SENSORS_TO_EMAIL` - SMTP
те же параметры что и у таски выше для формирования sql + прибавился дополнительный
`Alert channel name` - соответствует описанию канала уведомлений в описании скрипта `sql-monitor.py]`. Отличе заключается в том, что вместо `type` в конфиге, нужно выбрать соответствующий тип таски.
Если проставить галочку is_testing:
`CREATE_ST_TICKETS_FROM_SENSORS` - нарисует тикетов в очередь [SOLOMONTEST](https://st.yandex-team.ru/SOLOMONTEST/)
`SEND_SENSORS_TO_EMAIL` - отправит емейлов в рассылку solomonpushertest@yandex-team.ru
Если на что-то нет прав, стучитесь к Тане Васильевой `@tanya_vasya`

### Изменения в конфигах
Поменялась секция с подключением к базе, должна быть такой:
```
[Database]
driver=psycopg
user=market_checkouter_ro
host=man-f1bdw1kwmzo3lkqo.db.yandex.net
port=6432
database=market_checkouter_prod
vaultName=solomon_pusher_checkouter_postgres_pass
```
и смотрите другие примеры конфигов.
Все поля обязательные, `vaultName` - алиас по которому ищется секрет. Предпочтительным является заведение секретов в [Яндекс.Секретнице](https://yav.yandex-team.ru/). После создания секрета надо предоставить доступ на чтение роботу [robot-shlomo](https://staff.yandex-team.ru/robot-shlomo) и [проделегировать доступ](https://wiki.yandex-team.ru/sandbox/yav/#permissions) (можно от имени своего пользователя, то есть с использованием своего OAuth-токена, у которого в `scopes` есть `sandbox:api` и `vault:use`). При этом в конфиге имя секрета надо указывать в формате, описанном [тут](https://wiki.yandex-team.ru/sandbox/yav/#migration). Можно также завести секрет в [sandbox vault](https://sandbox.yandex-team.ru/admin/vault), но этот способ является [устаревшим](https://wiki.yandex-team.ru/sandbox/vault/).

## Доработка тасок или создание новых
Кратко:
1. Поднимаем дев сэндбокс в наверное [ЫПЕ](qyp.yandex-team.ru)
2. Настраиваем remote deploy в ide
3. Дорабатываем/создаем таску
4. Проверяем как работает в дев сандбоксе
5. Прогоняем тесты на дев сандбоксе `./sandbox test_tasks --clean`
6. Коммитим в аркадию
7. Profit

Про как писать заадачи довольно подробно написано на [вики sandbox](https://wiki.yandex-team.ru/Sandbox/), можно постучаться в `@anclav123`, попробую помочь. Или на рассылку sandbox

## Вводная про solomon-pusher
### Что такое solomon-pusher
По сути это набор python- и sql-скриптов для выполнения ряда задач по мониторингу различных данных.

### Что умеет solomon-pusher
Все основные функции так или иначе связаны с выполнением произвольного sql-запроса в произвольной реляционной БД и последующей обработкой результатов.

Что можно сделать с результатами выполнения sql:
1. Запушить данные в [Solomon](https://wiki.yandex-team.ru/solomon/) в качестве значения сенсора. Далее возможности расширяются до стандартных плюшек Соломона: можно настроить графики по значениям сенсора в Графане, можно настроить алерты, можно настроить нотификацию об алертах через e-mail, juggler, TG и др.
2. Отправить данные по e-mail в виде CSV-файла
3. Создавать/изменять/закрывать тикеты в StarTrek по данным из sql. Например, можно реализовать постановку тикета на исправление проблемы, которую обнаружил sql-запрос. Можно настроить, чтобы тикет автоматически обновлялся при изменении характера проблемы, или закрывался, если проблема "рассосалась".

Перечисленный функционал настраивается для регулярной работы с нужным расписанием (по крону).

## Структура проекта
### Сервисы
Все источники данных в проекте разбиты по т.н. сервисам (services). Например, sql-скрипты для получения данных из БД чекаутера принадлежат сервису checkouter, а для БД Аксапты - сервис erp. Поэтому все sql-скрипт и настройки источников данных лежат в папках **[services](services)/{название_сервиса}**

Для каждого сервиса обязательно присутствует конфигурационный файл **services/{название_сервиса}/{название_сервиса}.cfg**, содержащий настройки сервиса. Настройки сервиса определяют поведение скрипта, работающего в контексте этого сервиса.

В каждом сервисе как правило введена дополнительная иерархия подпапок, в которых хранятся уже непосредственно sql-скрипты. Это нужно для лучшей организации sql-кода. Обычно иерархия подпапок соответствует некой функциональной классификации внутри сервиса. Например, в сервисе [checkouter](services/checkouter) есть подпапки ff (функционал фулфиллмента), payments (платежи), delivery (доставка). Рекомендуется следовать этому принципу.

### crontab
В корне проекта расположен файл [crontab](crontab), в котором настраиваются все запуски скриптов solomon-pusher под конкретные нужды по обработке данных. Это стандартный файл для [unix-планировщика cron](https://ru.wikipedia.org/wiki/Cron). В каждой строчке содержится расписание запуска и команда для запуска.

## Конфиг
Для каждого сервиса обязательно присутствует конфигурационный файл **services/{название_сервиса}/{название_сервиса}.cfg**, в котором описываются настройки подключения к БД, Соломону, StarTrek и др. Дополнительно можно использовать локальный конфигурационный файл **services/{название_сервиса}/local-{название_сервиса}.cfg**, который оверрайдит настройки из основного конфига. Локальный конфиг не хранится в репозитории. Он полезен для дополнения или переопределения настроек на локальной машине (другие настройки подключения к БД, хранение секретных токенов и паролей).

Конфигурационный файл имеет структуру:

```
[Имя_раздела_1]
key1=value1
key2=value2
...

[Имя_раздела_2]
key1=value1
key2=value2
...
```
Пример конфига: [services/checkouter/checkouter.cfg](services/checkouter/checkouter.cfg)

### Раздел Datasource
Раздел определяет настройки соединения с БД для выполнения SQL-запроса
```
[Database]
driver=psycopg2
connectURL=postgresql://user:pwd@host:port/db_name?ssl=true&sslmode=require
```
  * `driver` определяет драйвер БД:
    - `psycopg2` - Postgres
    - `pymssql` - MS SQL Server
  * `connectURL` определяет коннекшн-строку с указанием хоста, порта, имени БД, логина и пароля для соединения с БД; формат коннекшн-строки зависит типа БД

### Раздел Solomon
Раздел определяет настройки проекта в Соломоне, куда будут пушиться значения сенсоров
```
[Solomon]
project=marketplace
cluster=production
service=checkouter
```
  * `project` - название проекта в Соломоне; для Беру/Bringly используется проект `marketplace`
  * `cluster` - название кластера в Соломоне; сейчас заведен только один `production`
  * `service` - название сервиса в Соломоне

## Скрипты
### [push-sensor-value.py](push-sensor-value.py)
Выполняет sql-запрос и пушит результаты в Соломон в виде числового значения сенсора. Результат sql-запроса определяет набор сенсоров и их значений во времени, которые нужно запушить в Соломон.

Для упрощения вызова скрипта есть shell-скрипт-напарник [push-service-sensor.sh](push-service-sensor.sh), принимающий следующие параметры:
  1. `-l` - опциональный параметр-флаг, включающий логирование скрипта в файл лога, находящийся в папке logs на машине выполнения
  2. <название_сервиса> - определяет конфиг и папку, в которой хранится sql-запрос
  3. <название_сенсора> - определяет путь к файлу sql-запроса относительно папки сервиса (без расширения .sql)

**Пример вызова скрипта:**
```
./push-service-sensor.sh -l checkouter /order-status/order-statuses
```
Такой вызов возьмет sql-скрипт [services/checkouter/order-status/order-statuses.sql](services/checkouter/order-status/order-statuses.sql) (запрос считает количество заказов в разрезе статусов и цвета), выполнит его в БД, указанной в конфиге сервиса checkouter [services/checkouter/checkouter.cfg](services/checkouter/checkouter.cfg), и запушит результаты запроса в Соломон.

SQL-запрос должен возвращать такие обязательные столбцы:
  * `sensor` - название сенсора в Соломоне; по соглашению название сенсора должно совпадать с путем к SQL-файлу (без расширения .sql), относительно папки сервиса
  * `ts` - unix-таймстамп для значения сенсора
  * `value` - числовое значение сенсора

Кроме обязательных столбцов можно дополнительно указать столбцы для разрезов (лейблов) значения сенсора. В примере с [services/checkouter/order-status/order-statuses.sql](services/checkouter/order-status/order-statuses.sql) разрезами являются статус, подстатус и цвет заказа. Соответственно для каждого разреза (лейбла) нужно возвращать отдельный столбец, указав ему название, которое будет запушено в Соломон в виде лейбла.

Таким образом каждая строка результатов SQL-запроса содержит данные для сенсора, который нужно запушить: имя сенсора, таймстамп значение, само значение сенсора и конкретные значения разрезов (лейблов).

### [sql-monitor.py](sql-monitor.py)
Выполняет SQL-запрос и отправляет данные по указанному каналу уведомлений. Есть различные типы каналы уведомлений, которые различаются форматом данных, способом из передачи и т.д. Подробнее про каналы написано [ниже](#каналы-уведомлений).

Для упрощения вызова скрипта есть shell-скрипт-напарник [service-sql-monitor.sh](service-sql-monitor.sh), принимающий следующие параметры:
  1. `-l` - опциональный параметр-флаг, включающий логирование скрипта в файл лога, находящийся в папке logs на машине выполнения
  2. <название_сервиса> - определяет конфиг и папку, в которой хранится sql-запрос
  3. <название_канала> - определяет канал, через который нужно отправить данные; канал должен быть определен в конфиге сервиса
  4. <путь_к_sql> - определяет путь к файлу sql-запроса относительно папки сервиса (без расширения .sql)

**Пример вызова скрипта:**
```
./service-sql-monitor.sh -l checkouter smtp-ff-packaging-team /ff/delayed-packaging-monitor
```
При этом в конфиге сервиса [services/checkouter/checkouter.cfg](services/checkouter/checkouter.cfg) канал `smtp-ff-packaging-team` настроен так:
```
[smtp-ff-packaging-team]
type=SMTP
sendTo=rkikot@yandex-team.ru, lna05@yandex-team.ru, gayane@yandex-team.ru, agorbatenko@yandex-team.ru
```

Такой вызов возьмет sql-скрипт [services/checkouter/ff/delayed-packaging-monitor.sql](services/checkouter/ff/delayed-packaging-monitor.sql) (запрос ищет заказы, которые задержались на этапе сборки на складе), выполнит его в БД, указанной в конфиге сервиса checkouter [services/checkouter/checkouter.cfg](services/checkouter/checkouter.cfg), сериализует данные в csv и отправит по e-mail указанным выше адресатам.

## Каналы уведомлений
Канал уведомлений определяет, куда и каким образом будут переданы результирующие данные выполнения sql-запроса.

Сейчас реализованы такие типы каналов:
  * `SMTP` - результаты sql-запроса сериализуются в CSV-файл и отправляются по e-mail указанным в канале адресатам
  * `StarTrek` - по результатам sql-запроса создается один или несколько тикетов в СтарТреке; есть возможность обновлять ранее созданные тикеты, чтобы не дублировать их при повторном выполнении скрипта для одних и тех же результатов sql-запроса
  * `HTTP` - результаты sql-запроса сериализуются в CSV-файл и отправляются HTTP POST-запросом по указанному в канале URL'у

Каналы настраиваются в конфиге сервиса, каждый канал - в отдельном разделе конфига. Название канала - название раздела в конфиге. Обязательное поле - `type` - определяет тип канала. Пример настройки канала `smtp-delivery-team` в конфиге:

```
[smtp-delivery-team]
type=SMTP
sendTo=muslimaleksander@yandex-team.ru, wuddy@yandex-team.ru, evgenynikulin@yandex-team.ru
```

У каждого типа канала свое поведение и свои дополнительные настройки в конфиге.

### Тип канала SMTP
Результаты выполнения SQL-запроса отправляются по e-mail в виде приаттаченного CSV-файла. В CSV **не** сериализуются столбцы с названием, начинающимся с двух символов подчеркивания `__`. Если SQL-запрос не возвращает никаких данных, то письмо не отправляется.

Настройки канала определяются в конфиге в секции с названием канала:
  * `type=SMTP` - тип канала SMTP
  * `sendTo` - список адресатов через запятую
  * `subject` - тема письма; это необязательное поле - если не указано, то тема письма должна быть указана в самом SQL-запросе в столбце `__smtp_subject`

Общие настройки для всех каналов типа SMTP находятся в разделе `SMTP` конфига:
  * `sendFrom` - From-адресат письма

### Тип канала StarTrek
По результатам выполнения SQL-запроса создаются новые или обновляются существующие тикеты в СтарТреке. Значения для полей тикетов определяются в самом SQL-запросе. Там же определяется логика группировки результирующих строчек запроса в тикеты.

Название тикета, определенное в SQL-запросе, является ключом, по которому скрипт идентифицирует тикеты. Перед тем, как создать новый тикет, скрипт проверяет, не существует ли уже в очереди тикет с таким названием. Если его нет, то создается новый, а если уже есть, то тикет-дубль создаваться не будет: при необходимости существующий тикет будет обновлен (если в канале включена настройка `updateTickets`).

При этом если в канале включена настройка `closeDuplicateTickets`, скрипт дополнительно может следить за наличием тикетов-дублей, возникших каким-либо образом, и закрывать их, оставляя открытым только один (самый ранний открытый).

Дополнительно скрипт может закрывать те тикеты в очереди, которым уже не соответствует ни одна строка из SQL-запроса (если в канале включена настройка `closeTickets`).

Для всех результирующих строк запроса с одинаковым названием тикета будет создан один тикет в СтарТреке. Если тикету соответствует более одной строки запроса, то все такие строки будут сериализованы в CSV-файл, который приаттачивается к тикету. В CSV **не** сериализуются столбцы с названием, начинающимся с двух символов подчеркивания `__`.

Столбцы SQL-запроса, определяющие поля тикета:
  * `__st_queue` - название очереди
  * `__st_summary` - название тикета
  * `__st_description` - описание тикета
  * `__st_tags` - теги тикета, список через запятую (нельзя использовать пробелы в тегах)
  * `__st_components` - числовые ид. компонентов тикета, список через запятую
  * `__st_weight` - вес тикета
  * `__st_customer_order_number` - поле "Номер заказа Беру" (блок полей "Беру.ру")
  * `__st_return_reason` - поле "Основание возврата" (блок полей "Беру.ру")
  * `__st_payment_method` - поле "Способ оплаты" (блок полей "Беру.ру")
  * `__st_customer_email` - поле "Email покупателя" (блок полей "Беру.ру")
  * `__st_cost_adv` - поле "Стоимость" (блок полей "Оценка задачи")

Настройки канала определяются в конфиге в секции с названием канала:
  * `type=StarTrek` - тип канала StarTrek
  * `updateTickets` - флаг (`true`/`false`), включающий обновление тикетов; если выключено, то существующие тикеты обновляться не будут; по умолчанию включено
  * `closeTickets` - флаг (`true`/`false`), включающий закрытие тикетов; если выключено, то существующие тикеты закрываться не будут; по умолчанию включено
  * `closeDuplicateTickets` - флаг (`true`/`false`), включающий дедубликацию тикетов; если выключено, то тикеты-дубликаты закрываться не будут; по умолчанию включено

Общие настройки для всех каналов типа StarTrek находятся в разделе `StarTrek` конфига:
  * `url` - URL АПИ СтарТрека
  * `login` - логин, под которым производятся действия в СтарТреке
  * `userAgent` - как скрипт представляется API СтарТрека

### Тип канала HTTP
Результаты выполнения SQL-запроса сериализуется в CSV и отправляется в теле HTTP POST-запроса с заголовком `Content-Type: text/csv`. В CSV **не** сериализуются столбцы с названием, начинающимся с двух символов подчеркивания `__`.

Настройки канала определяются в конфиге в секции с названием канала:
  * `type=HTTP` - тип канала HTTP
  * `url` - URL, по которому выполняется POST-запрос

## SQL-шаблонизатор
### Переиспользование SQL-кода
Основная кодовая база в solomon-pusher - это SQL-запросы. Их много и регулярно возникает потребность частично переиспользовать SQL-код из соседних запросов. Чтобы не дублировать код, в solomon-pusher есть возможность "включения" (include) кусков SQL-кода (включаемый код) внутрь другого SQL-запроса (включающий код).

Синтаксис "вызова" SQL-кода:
```$<имя_sql>[(<аргумент_1>[, <аргумент_2>[, ...])]```

 * `имя_sql` - путь к sql-файлу (без расширения .sql), код которого нужно подставить вместо конструкции вызова
 * `аргумент_N` - "аргументы" "вызова" SQL-кода, которые позволяют в определенной степени параметризировать вставляемый SQL-код

В качестве `имя_sql` может быть как просто название SQL-файла, так и относительный путь к SQL-файлу (в обоих случаях - без расширения .sql). В первом случае включаемый SQL-файл должен находится в той же папке, что и включающий SQL-файл, либо в специальной папке `util`, находящейся в непосредственно в папке сервиса, в котором находится включающий файл. В случае же указания в конструкции "вызова" относительного пути, включаемый файл ищется по этому пути относительно корневой папки сервиса, где находится включающий файл.

<details>
<summary><i>Пример 1 (простое включение)</i></summary>

Включающий SQL-файл [services/checkouter/delivery/delivery-orders.sql](services/checkouter/delivery/delivery-orders.sql):
```
...
where o.rgb <> 0 and not o.fake and o.user_id != $stress_test_uid AND NOT (o.user_id BETWEEN 2190550858753437195 AND 2190550859753437194)
...
```

Включаемый SQL-файл [services/checkouter/util/stress_test_uid.sql](services/checkouter/util/stress_test_uid.sql):
```
2308324861409815965
```

После выполнения шаблонизации результирующий SQL-код будет выглядить так:
```
...
where o.rgb <> 0 and not o.fake and o.user_id != 2308324861409815965 and not (o.user_id between 2190550858753437195 AND 2190550859753437194)
...
```
</details>

Включаемый SQL-файл может быть параметризован. При "вызове" в него могут быть "переданы" аргументы, значения которых заменят исходные параметры-шаблоны. Для этого внутри включаемого SQL-файла используются специальные переменные `$1`, `$2` и т.д., обозначающие параметры в порядке их "передачи" при включении.

<details>
<summary><i>Пример 2 (включение с аргументами)</i></summary>

Включающий SQL-файл [services/checkouter/order-status/order-statuses.sql](services/checkouter/order-status/order-statuses.sql):
```
SELECT '/order-status/order-statuses' as sensor,
       round(extract(epoch from now())) as ts,
       $rgb_name(o.rgb) as rgb,
       $status_name(o.status) as status,
       coalesce($substatus_name(o.substatus), 'NONE') as substatus,
       count (*) as value
from orders o
WHERE o.rgb <> 0 and not o.fake and o.user_id != $stress_test_uid AND NOT (o.user_id BETWEEN 2190550858753437195 AND 2190550859753437194)
    and o.context = 0 and (o.rgb <> 2 or o.created_at > '2018-11-12')
    and (o.status not in (7,6) or o.status_updated_at >= current_date)
group by o.rgb, o.status, o.substatus
order by o.rgb, o.status, o.substatus
```

Включаемый SQL-файл [services/checkouter/util/rgb_name.sql](services/checkouter/util/rgb_name.sql):
```
case $1
  when 0 then 'WHITE'
  when 1 then 'BLUE'
  when 2 then 'RED'
  else $1::text
end
```

Включаемый SQL-файл [services/checkouter/util/status_name.sql](services/checkouter/util/status_name.sql):
```
case $1
  when 0 then 'PLACING'
  when 1 then 'RESERVED'
  when 2 then 'UNPAID'
  when 3 then 'PROCESSING'
  when 4 then 'DELIVERY'
  when 5 then 'PICKUP'
  when 6 then 'DELIVERED'
  when 7 then 'CANCELLED'
  when 8 then 'PENDING'
  else $1::text
end
```

После выполнения шаблонизации результирующий SQL-код будет выглядить так:
```
SELECT '/order-status/order-statuses' as sensor,
       round(extract(epoch from now())) as ts,
       case o.rgb
         when 0 then 'WHITE'
         when 1 then 'BLUE'
         when 2 then 'RED'
         else o.rgb::text
           end
    as rgb,
       case o.status
         when 0 then 'PLACING'
         when 1 then 'RESERVED'
         when 2 then 'UNPAID'
         when 3 then 'PROCESSING'
         when 4 then 'DELIVERY'
         when 5 then 'PICKUP'
         when 6 then 'DELIVERED'
         when 7 then 'CANCELLED'
         when 8 then 'PENDING'
         else o.status::text
           end
    as status,
       coalesce(case o.substatus
                  when 0 then 'RESERVATION_EXPIRED'
                  when 1 then 'USER_NOT_PAID'
                  when 2 then 'USER_UNREACHABLE'
                  when 3 then 'USER_CHANGED_MIND'
                  when 4 then 'USER_REFUSED_DELIVERY'
                  when 5 then 'USER_REFUSED_PRODUCT'
                  when 6 then 'SHOP_FAILED'
                  when 7 then 'USER_REFUSED_QUALITY'
                  when 8 then 'REPLACING_ORDER'
                  when 9 then 'PROCESSING_EXPIRED'
                  when 10 then 'PENDING_EXPIRED'
                  when 11 then 'SHOP_PENDING_CANCELLED'
                  when 12 then 'PENDING_CANCELLED'
                  when 13 then 'USER_FRAUD'
                  when 14 then 'RESERVATION_FAILED'
                  when 15 then 'USER_PLACED_OTHER_ORDER'
                  when 16 then 'USER_BOUGHT_CHEAPER'
                  when 17 then 'MISSING_ITEM'
                  when 18 then 'BROKEN_ITEM'
                  when 19 then 'WRONG_ITEM'
                  when 20 then 'PICKUP_EXPIRED'
                  when 21 then 'DELIVERY_PROBLEMS'
                  when 22 then 'LATE_CONTACT'
                  when 23 then 'CUSTOM'
                  when 24 then 'DELIVERY_SERVICE_FAILED'
                  when 25 then 'WAREHOUSE_FAILED_TO_SHIP'
                  when 26 then 'DELIVERY_SERVICE_UNDELIVERED'
                  when 27 then 'PREORDER'
                  when 28 then 'AWAIT_CONFIRMATION'
                  when 29 then 'STARTED'
                  when 30 then 'PACKAGING'
                  when 31 then 'READY_TO_SHIP'
                  when 32 then 'SHIPPED'
                  else o.substatus::text
                    end
         , 'NONE') as substatus,
       count (*) as value
from orders o
WHERE o.rgb <> 0 and not o.fake and o.user_id != 2308324861409815965 and not (o.user_id between 2190550858753437195 AND 2190550859753437194)

  and o.context = 0 and (o.rgb <> 2 or o.created_at > '2018-11-12')
  and (o.status not in (7,6) or o.status_updated_at >= current_date)
group by o.rgb, o.status, o.substatus
order by o.rgb, o.status, o.substatus
```
</details>

При включении SQL-кода допускается рекурсия (осторожно: защиты от циклической рекурсии нет).

Внимание: нельзя использовать результат конструкции включения в качестве аргумента для другой конструкции включения. Например, такой синтаксис вызовет ошибку: `$file1($file2)`

### Разворачивание SQL-шаблонов
Поскольку шаблонизация сильно затрудняет чтение SQL-кода, в solomon-pusher есть средство для "разворачивания" (explode) SQL-кода. При этом все "включения" будут зарезолвлены и собраны в монолитный SQL-код. Выполняется это при помощи скрипта [prepare_sql.py](prepare_sql.py):
```
prepare_sql.py <sql-file>
```

`sql-file` - относительный путь к SQL-файлу (относительно корневой папки проекта)

Скрипт рекурсивно развернет все включаемые запросы, выдаст результирующий SQL-код в stdout и дополнительно скопирует его в буфер обмена для удобства. Удобно назначить вызов скрипта в IDE на комбинацию клавиш. См. [FAQ](#склеить-sql-в-idea). После этого можно сразу открывать scratch-файл, вставлять SQL-код из буфера обмена и исполнять его.

### Кросс-БД запросы
solomon-pusher умеет выполнять различные фрагменты SQL-запроса в разных БД. Это полезно, когда нужно поджойнить или еще как-то объединить данные, располагающиеся в разных хранилищах.

Чтобы выполнить кусок SQL-запроса в отдельной БД, нужно оформить этот запрос в отдельный SQL-файл, разместив его в соответствующем сервисе проекта. Далее в основном SQL-запросе (который располагается уже в другом сервисе) нужно просто "включить" первый файл, указав путь к нему относительно корневой папки сервисов.

*Пример*
Допустим, есть основной SQL-файл в сервисе checkouter:
```
select o.id, status
from orders o join order_item i on i.order_id = o.id
where i.shop_sku in $/ff_workflow/today_supplies
```

Допустим, в сервисе ff_workflow есть файл today_supplies.sql:
```
select distinct ri.article as ssku
from shop_request r join request_item ri on r.id = ri.request_id
where r.status = 10 and r.updated_at >= current_date
```

При выполнении основного SQL-запроса сначала будет выполнен запрос из today_supplies.sql в БД, описанной в конфиге сервиса ff_workflow. Результаты этого запроса будут сериализованы в конструкцию `select <values> union all ...` и вставлены в текст основного запроса:
```
select o.id, status
from orders o join order_item i on i.order_id = o.id
where i.shop_sku in (
  select '12345' union all
  select '23456' union all
  select '6789'
)
```
Далее этот основной запрос выполняется как обычно в БД, описанной в сервисе checkouter.

## FAQ
### Как добавить новый график в solomon
1. Добавить sql в services/. Запрос обязательно должен содержать колонки sensor, ts и value. Все остальные колонки станут лейблами.
2. Добавить новую запись в crontab.

### Как задеплоить изменения
1. Зайти на braavos.market.yandex.net
2. cd /home/mkasumov/solomon-pusher
3. sudo -u mkasumov ./update.sh

### Где смотреть логи
Логи лежат на braavos.market.yandex.net в папке /home/mkasumov/solomon-pusher/logs

### Склеить SQL в IDEA
 * в идее Preferences -> Tools -> External tools
 * в name придумать название
 * Program: $PyInterpreterDirectory$/python2 - вместо $PyInterpreterDirectory$ подставить путь к питону в venv, если не пользуешься, должно быть что то другое
 * Arguments: $ProjectFileDir$/prepare_sql.py $FilePathRelativeToProjectRoot$
 * Working dir: $ProjectFileDir$

Сохранить. В Keymap - External tools - добавить shortcut.

### Склеить SQL в PyCharm
 * File -> Settings -> Tools -> External tools
 * Добавить новый тул, в Name придумать название, например, SolomonPusher
 * Program: `python`
 * Arguments: `$ProjectFileDir$/prepare_sql.py $FilePathRelativeToProjectRoot$`
 * Working dir: `$ProjectFileDir$`

Открываем нужный скрипт. Запускаем Tools -> External Tools -> SolomonPusher в окне вывода будет SQL.
Так же SQL будет сразу скопирован в буфер обмена и его сразу можно всталять и исполнять.

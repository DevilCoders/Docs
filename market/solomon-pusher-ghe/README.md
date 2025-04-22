## Про репозиторий
В данную папку были перенесены коммиты из репозитория https://github.yandex-team.ru/markin-nn/solomon-pusher, см. подробности в тикете [ARCADIA-2396](https://st.yandex-team.ru/ARCADIA-2396).
В репозитории https://github.yandex-team.ru/markin-nn/solomon-pusher разработка заморожена, она продолжается здесь.
К сожалению, история коммитов после переноса в Аркадию из Гитхаба не совсем точно воспроизводит настоящую историю коммитов, как они были сделаны в Гитхабе. Поэтому, если в силу каких-то причин будет необходимость поднимать историю по коммитам, которые перенесены из Гитхаба, то лучше смотреть историю таких коммитов в Гитхабе. См. обсуждение [тут](https://st.yandex-team.ru/ARCADIA-2396#600ec9add0298358e11d4708).

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

### distributed-crontab
В корне проекта расположена папка [distributed-crontab](distributed-crontab). В ней настраиваются все запуски скриптов solomon-pusher под конкретные нужды по обработке данных. В папке [distributed-crontab](distributed-crontab) находятся json-файлы (поддерживается JSON5), описывающие крон-задачи, которые выполняются в распределённом планировщике solomon-pusher-scheduler, подробнее о котором можно прочитать [на вики](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/). [Там же](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/#konfigidljazapuskazadach) описан формат конфигурационных файлов. Формат файлов можно проверить с помощью запуска скрипта [check_distributed_crontab_configs.py](test/check_distributed_crontab_configs.py) (предназначено для запуска на машине разработчика в IDE, требует установки дополнительных пакетов, не перечисленных в [requirements.txt](requirements.txt) - пакеты указаны в коде [check_distributed_crontab_configs.py](test/check_distributed_crontab_configs.py) в комментариях). Задачи рекомендуется раскладывать в json-файлы посервисно. Т.е. если есть сервис checkouter, то в папке [distributed-crontab](distributed-crontab) удобно расположить файл [checkouter.json](distributed-crontab/checkouter.json), в котором будут содержаться все задачи, связанные с этим сервисом. Задачи, которые описаны в [distributed-crontab](distributed-crontab), выполняются на кластере из 6 инстансов в nanny: сервисы [production_market_solomon_pusher_scheduler_man](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_solomon_pusher_scheduler_man/), [production_market_solomon_pusher_scheduler_sas](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_solomon_pusher_scheduler_sas/), [production_market_solomon_pusher_scheduler_vla](https://nanny.yandex-team.ru/ui/#/services/catalog/production_market_solomon_pusher_scheduler_vla/).

## Конфиг
Для каждого сервиса обязательно присутствует конфигурационный файл **services/{название_сервиса}/{название_сервиса}.cfg**, в котором описываются настройки подключения к БД, Соломону, StarTrek и др. Дополнительно можно использовать локальный конфигурационный файл **services/{название_сервиса}/local-{название_сервиса}.cfg**, который оверрайдит настройки из основного конфига. Локальный конфиг не хранится в репозитории. Он полезен для дополнения или переопределения настроек на локальной машине (другие настройки подключения к БД, хранение секретных токенов и паролей). Также, если при запуске скриптов им передаётся переменная окружения `SP_SECRETS_DIR` с путём до некоторой папки, то в дополнение к описанному local-файлу происходит чтение конфига из файла **${SP_SECRETS_DIR}/{название_сервиса}.cfg**, если он существует. Как и в случае с local-конфигом, происходит дополнение или переопределение настроек, заданных в других ранее перечисленных файлах (файл из папки `SP_SECRETS_DIR` имеет наивысший приоритет). В nanny с помощью упомянутой переменной `SP_SECRETS_DIR` подгрузка секретов осуществляется из папки `solomon-pusher-secrets`, в которую выгружаются секреты из секретницы [solomon-pusher-secrets](https://yav.yandex-team.ru/secret/sec-01et85q8ayqwrx9emhaxcpf6g4/explore/versions). Для изменения значений секретных пропертей можно обращаться к дежурному в чат `TSUM and Market Health support`.

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

### Раздел Database
Раздел определяет настройки соединения с БД для выполнения SQL-запроса
```
[Database]
driver=psycopg2
connectURL=postgresql://user:pwd@host:port/db_name?ssl=true&sslmode=require
```
  * `driver` определяет драйвер БД:
    - `psycopg2` - Postgres
    - `pymssql` - MS SQL Server
  * `connectURL` определяет коннекшн-строку с указанием хоста, порта, имени БД, логина и пароля для соединения с БД; формат коннекшн-строки зависит типа БД. Логин и пароль нужно хранить в секретах в разделе `Database` (например, в параметрах `user` и `password`) и ссылаться на них в `connectURL` с помощью механизма подстановок, то есть с указанием `%(user)s` и `%(password)s`, если мы говорим о параметрах `user` и `password`. В результате строчка для подключения к базе данных, которая закоммичена в репозиторий, может выглядеть как-то так: `connectURL=postgresql://%(user)s:%(password)s@sas-dyeuo57r8mkzvlq1.db.yandex.net:6432/test?ssl=true&sslmode=require`. Есть возможность сослаться на переменную окружения для подстановки её значения с помощью выражения вида `${имя_переменной_окружения}`. Такое выражение можно использовать только единственный раз. Например, можно с помощью переменной окружения `CHECKOUTER_DB_HOSTS` задать список хостов таким образом `connectURL=postgresql://%(user)s:%(password)s@${CHECKOUTER_DB_HOSTS}/test?ssl=true&sslmode=require`. Переменные окружения выставляются с помощью планировщика Соломон-Пушера. Подробнее про передачу переменных окружения в скрипты можно прочитать на [wiki](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/#peremennyeokruzhenijaperedavaemyevdochernieprocessy). Для обеспечения отказоустойчивости в `connectURL` желательно указывать более 1 хоста, хотя бы 2. В случае использования драйвера `psycopg2` указать пару хостов можно просто перечислив их через запятую, например, так: `postgresql://%(user)s:%(password)s@man-t4zxdqmhwwfe5w1u.db.yandex.net:6432,vla-3h1ha3gqy1dag8bf.db.yandex.net:6432/market_tpl_production?sslmode=require`. При этом надо понимать, что при выполнении запроса `psycopg2` ищет в списке хостов первый живой и выполняет запрос на нём. То есть балансировки запросов не происходит, перечисление нужно в данном случае именно для обеспечения отказоустойчивости в случае выхода реплик из строя или учений.

В случае использования драйвера `psycopg2` запросы могут выполняться в синхронном и асинхронном режимах. Синхронный режим является режимом по-умолчанию. Асинхронный режим является экспериментальным на текущий момент. Есть гипотеза, что использование асинхронного режима позволит более экономично использовать оперативную память при выполнении скриптов. Проверка гипотезы производится в рамках тикета [MARKETINFRA-8760](https://st.yandex-team.ru/MARKETINFRA-8760). Включение асинхронного режима на этапе проведения эксперимента производится для отдельных задач с помощью добавления их имён в переменную окружения `SP_ASYNC_TASKS` (управление переменными окружения описано на [wiki](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/#peremennyeokruzhenijaperedavaemyevdochernieprocessy)). В качестве разделителя имён используется точка с запятой (`;`). Под именем задачи понимается значение поля `taskName` из соответствующего json-файла в папке [distributed-crontab](distributed-crontab).

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
Выполняет sql-запрос и пушит результаты в Соломон в виде числового значения сенсора. Результат sql-запроса определяет набор сенсоров и их значений во времени, которые нужно запушить в Соломон. По умолчанию, при работе скрипта результат итогового запроса в базу вытаскивается целиком в оперативную память, затем делается дополнение некоторых временных рядов нулями (в том случае, если в текущих данных по ним нет точек, а в целом за прошедшие сутки что-то было, см. подробнее описание этого процесса [тут](https://st.yandex-team.ru/SOLOMONPUSHER-120#6196849321efb11d4ec6478a)). Этот вариант работы скрипта возможен только в тех ситуациях, когда в ответе из базы участвует не очень много временных рядов (сенсор + метки). Когда их много, то с одной стороны они могут не умещаться в оперативную память, а с другой стороны запрос исторических данных в Соломон, на основании которого делается заполнение отсутствующих временных рядов, не отрабатывает корректно и дополнение нулями по факту не работает. Поэтому существует также альтернативный вариант работы скрипта, который включается при при передаче в скрипт переменной окружения `SP_DB_FETCH_SIZE` с целочисленным значением, определяющим максимальный размер пачки данных (в строках), которая вытаскивается из базы, обрабатывается и отправляется в Соломон. Результаты всего запроса при этом могут быть обработаны за несколько итераций, если полный ответ из базы не вмещается в 1 пачку. При обработке ответа по пачкам механизм дополнения временных рядов нулями выключен. Управление переменными окружения, передаваемыми в скрипты Соломон-Пушера, осуществляется через планировщик Соломон-Пушера, см. подробнее [тут](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/#peremennyeokruzhenijaperedavaemyevdochernieprocessy). Также для корректной работы скрипта в этом режиме он должен получать переменную окружения `SP_TASK_NAME`, содержащую название задачи Соломон-Пушера (см. подробнее [тут](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/#konfigidljazapuskazadach)). С использованием этой переменной создаётся именованный курсор, который нужен для чтения строк из результата запроса к базе пачками. Эту переменную окружения также должен проставлять планировщик Соломон-Пушера.

Для упрощения вызова скрипта есть shell-скрипт-напарник [push-service-sensor.sh](push-service-sensor.sh), принимающий следующие параметры:
  1. `-l` - опциональный параметр-флаг, включающий логирование скрипта в файл лога, находящийся в папке logs на машине выполнения. Можно использовать переменную окружения `SP_LOG_DIR` для указания нестандартной папки хранения логов.
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
  1. `-l` - опциональный параметр-флаг, включающий логирование скрипта в файл лога, находящийся в папке logs на машине выполнения. Можно использовать переменную окружения `SP_LOG_DIR` для указания нестандартной папки хранения логов.
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

Такой вызов возьмет sql-скрипт [services/checkouter/ff/delayed-packaging-monitor-smtp.sql](services/checkouter/ff/delayed-packaging-monitor-smtp.sql) (запрос ищет заказы, которые задержались на этапе сборки на складе), выполнит его в БД, указанной в конфиге сервиса checkouter [services/checkouter/checkouter.cfg](services/checkouter/checkouter.cfg), сериализует данные в csv и отправит по e-mail указанным выше адресатам.

### Общее замечание по поводу возможности выбора используемого питона
Shell-скрипты [service-sql-monitor.sh](service-sql-monitor.sh) и [push-service-sensor.sh](push-service-sensor.sh) поддерживают переменную окружения `SP_PYTHON_VENV_DIR`, в которую можно передать путь до виртуального окружения, используемого для запуска python-скриптов.

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
  * `sendFrom` - From-адресат письма. Здесь нужно указать ту часть адреса, которая находится до знака `@`. Т.е., например, если тут указать `sql-monitor`, а скрипт отработает на сервере `vla2-8739-b60-vla-market-prod--408-30616.gencfg-c.yandex.net`, то получившееся письмо будет от адресата `sql-monitor@vla2-8739-b60-vla-market-prod--408-30616.gencfg-c.yandex.net`.


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
  * `__st_deliveryName` - поле "Название СД" (блок полей "Беру.ру")
  * `__st_cost_adv` - поле "Стоимость" (блок полей "Оценка задачи")

Настройки канала определяются в конфиге в секции с названием канала:
  * `type=StarTrek` - тип канала StarTrek
  * `updateTickets` - флаг (`true`/`false`), включающий обновление тикетов; если выключено, то существующие тикеты обновляться не будут; по умолчанию включено
  * `closeTickets` - флаг (`true`/`false`), включающий закрытие тикетов; если выключено, то существующие тикеты закрываться не будут; по умолчанию включено
  * `closeDuplicateTickets` - флаг (`true`/`false`), включающий дедубликацию тикетов; если выключено, то тикеты-дубликаты закрываться не будут; по умолчанию включено
  * `attachSingleRowCsv` - флаг (`true`/`false`), включающий генерацию csv файла даже при наличии только 1 строчки
        в результатах выборки; если выключено, необходимо результат записывать, например, в `__st_description`
        в самом запросе; по умолчанию выключено
  * `reopenStrategy` - перечисление (`Always`/`WhenAddingNewOrders`), определяет стратегию переоткрытия закрытых тикетов;
    - `Always` - переоткрытие будет происходить при очередном срабатывании, если мониторинг вернул хотя бы одну
        строку; выбрано по умолчанию;
    - `WhenAddingNewOrders` - переоткрытие тикетов только при добавлении добавлении новых заказов
    в `__st_customer_order_number`.

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
where o.rgb <> 0 and not o.fake and o.user_id != 2308324861409815965 AND NOT (o.user_id BETWEEN 2190550858753437195 AND 2190550859753437194)
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
                  when 26 then 'DELIVERY_SERIVCE_UNDELIVERED'
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
WHERE o.rgb <> 0 and not o.fake and o.user_id != 2308324861409815965 AND NOT (o.user_id BETWEEN 2190550858753437195 AND 2190550859753437194)

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

Пример
```
python prepare_sql.py services\checkouter\crm\crm-union-all-monitoring.sql
```

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

Иногда хочется, чтобы результат запроса в одну базу был подставлен в следующий запрос не как `select ... union all`,
а как `values((...),(...)) as {alias}(column_1_name, column_2_name)`.
Чтобы добиться такого результата, включать дочерний скрипт надо следующим образом:
`$/ff_workflow/today_supplies#supplier -- supplier это alias для выражения values() as {alias}`
Example:
```
select o.id, o.status, supplier.ssku
from  $/ff_workflow/today_supplies#supplier -- supplier это alias для выражения values() as {alias}
join order_item i on i.shop_sku = supplier.ssku
join orders o on o.id = i.order_id
```
sql:
```
select o.id, o.status, supplier.ssku
from  (values
    ('12345'),
    ('23456'),
    ('6789')
    ) as supplier(ssku)
join order_item i on i.shop_sku = supplier.ssku
join orders o on o.id = i.order_id
```

## FAQ
### Как установить зависимости
Для запуска нужен Python2.
Установить зависимости можно так:
```
sudo python -m pip install -r requirements.txt
```
Если при установке библиотек питона что-то пойдёт не так, то, возможно, это обозначает, что предварительно надо доустановить пакеты операционной системы:
```
sudo apt install build-essential python-dev postgresql-client-common=173ubuntu0.3 postgresql-common=173ubuntu0.3 postgresql-9.5 postgresql-client-9.5 libpq-dev libffi-dev freetds-dev
```
### Как создать виртуальное python-окружение с необходимыми зависимостями
Удобно создавать в виртуальной машине.
Создать виртуальную машину можно по ссылке в [QYP](https://qyp.yandex-team.ru/create-vm).
Можно использовать дефолтный сетевой макрос `_SEARCHSAND_`.
По характеристикам достаточно 2 ядра, 4ГБ RAM, 40ГБ HDD
В качестве образа можно взять последний, соответствующий той операционке, которая лежит в основе rtc-сервисов, где будет
эксплуатироваться виртуальное окружение.
Например, для trusty надо смотреть [тут](https://sandbox.yandex-team.ru/resources?attr_name=released&attr_value=stable&owner=RCCS-ADMINS&state=READY&type=QEMU_IMAGE_SEARCH_TRUSTY_DEVEL&limit=20&attrs=%7B%7D).
К примеру, был успешно использован [этот](https://sandbox.yandex-team.ru/resource/1403338192/view) образ.
Со страницы ресурса можно скопировать Skynet ID, то есть в формате типа такого `rbtorrent:38e5e29d6fb4a80528c95c0bc748c84a6031fcf0`.
Выбрать пропускную способность для дисков. 10МБ/c будет достаточно.
Выбрать Internet Access NAT64.
Запустить виртуальную машину.
Подключиться по ssh к виртуальной машине с помощью её FQDN, который можно увидеть в настройках.
Скачать исходники скриптов SP из Аркадии, например, так:
```
svn co svn+ssh://arcadia.yandex.ru/arc/trunk/arcadia/market/solomon-pusher-ghe/
```
Зайти в папку `solomon-pusher-ghe` и выполнить скрипт `sudo ./prepare_os_for_build_python_virtual_env.sh`, который
установит необходимые пакеты операционной системы для сборки питона.
Затем выполнить скрипт `./build_python_virtual_env.sh` (можно уже без `sudo`). Примерное время выполнения около
трёх с половиной минут.
В результате в папке `solomon-pusher-ghe` появится файл `solomon_pusher_python.tar.gz`, содержащий в себе
виртуальное python-окружение с зависимостями, необходимыми для работы скриптов Соломон-Пушера.
Его можно копировать куда-то на рабочий ноутбук с помощью команды вида:
```
scp <fqdn виртуальной машины>:solomon-pusher-ghe/solomon_pusher_python.tar.gz ./
```
Например:
```
scp semin-serg-trusty-dev-2.vla.yp-c.yandex.net:solomon-pusher-ghe/solomon_pusher_python.tar.gz ./
```
А потом загрузить в sandbox на вечное хранение с помощью команды:
```
ya upload --ttl=inf solomon_pusher_python.tar.gz
```
Полученный идентификатор ресурса можно использовать в конфигурации контейнеров в rtc для того, чтобы привозить туда
виртуальное окружение.
Вообще полученное таким образом виртуальное окружение можно использовать на машинах, где нужно выполнять скрипты
Соломон-Пушера и там нет возможности доставить необходимые библиотеки для системного питона. Виртуальное окружение можно либо распаковать в папку, которая использовалась при сборке
(`/tmp`) и потом активировать с помощью `source /tmp/solomon_pusher_python/env/bin/activate`, либо распаковать
в какую-то другую произвольную папку (активация уже не будет работать) и при запуске скриптов Соломон-Пушера добавлять
в переменную `PATH` слева путь до `solomon_pusher_python/env/bin` (добавление в переменную `PATH` слева нужно для
приоритета над системным питоном) и указывать в переменной окружения `PYTHONPATH` путь до
`solomon_pusher_python/env/lib/python2.7/site-packages` (указанные пути нужно дополнить абсолютным или относительным
путём до указанных папок).

### Как добавить новый график в solomon
1. Добавить sql в services/. Запрос обязательно должен содержать колонки sensor, ts и value. Все остальные колонки станут лейблами.
2. Добавить новую запись в json-файл, соответствующий сервису, в папке [distributed-crontab](distributed-crontab) (см. подробнее [тут](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/#konfigidljazapuskazadach)).

### Как задеплоить изменения
Вмерджить изменения в trunk в папке [solomon-pusher-ghe](https://a.yandex-team.ru/arc/trunk/arcadia/market/solomon-pusher-ghe/) в Аркадии и дождаться выкладки релизной машины [solomon-pusher-scheduler](https://tsum.yandex-team.ru/pipe/projects/infra/delivery-dashboard/solomon-pusher-scheduler) в nanny. Релизная машина запускается автоматически при появлении новых коммитов. Релизы происходят по будним дням в рабочее время. В случае необходимости что-то выкатить в нерабочее время обращаться к дежурному инфраструктуры маркета в чат `TSUM and Market Health support`. Переход на эту релизную машину произошёл недавно, и если вдруг нужно посмотреть историю предшествовавших релизов, то надо смотреть релизную машину [solomon-pusher-scheduler-deb](https://tsum.yandex-team.ru/pipe/projects/infra/delivery-dashboard/solomon-pusher-scheduler-deb).

### Где смотреть логи
Для просмотра и поиска по логам нужно использовать logview-сервера, о которых подробнее написано [тут](https://wiki.yandex-team.ru/market/sre/servera-logview/). Если кратко, то после входа на один из logview-серверов с помощью команды `ssh logview.market.yandex.net` для монтирования папок с логами скриптов Соломон-Пушера, выполняемых в облаке, надо выполнить команду:
```
sudo mount-service-log -oremount production_market_solomon_pusher_scheduler_{man,sas,vla}
```
После этого в папках с именами типа `/mnt/nanny/<название nanny-сервиса>/<fqdn инстанса>/solomon-pusher` окажутся логи скриптов. Для поиска сразу по логам определённой задачи за сегодня сразу на всех инстанасах можно использовать команду вида:
```
grep "<что-то искомое>" /mnt/nanny/production_market_solomon_pusher_scheduler_{man,sas,vla}/*/solomon-pusher/<имя сервиса (в терминологии SP)><название сенсора>.log
```
Например, если что-то надо найти в логах за сегодня для задачи с командой:
```
./push-service-sensor.sh -l checkouter /orderedit/order_change_request_statuses
```
То соответствующий вызов grep будет выглядеть так:
```
grep "<что-то искомое>" /mnt/nanny/production_market_solomon_pusher_scheduler_{man,sas,vla}/*/solomon-pusher/checkouter/orderedit/order_change_request_statuses.log
```
Если заранее по админке базинги, которая для production-среды находится за балансировщиком http://solomon-pusher.vs.market.yandex.net/z/bazinga (доступ даётся с помощью добавления в abc-группу [solomonpusher2](https://abc.yandex-team.ru/services/solomonpusher2)), определить инстанс, на котором задача выполнялась в интересующий момент времени, то можно сразу работать с нужным файлом на соответствующем инстансе, а не грепать логи на всех инстансах. Чтобы не набирать руками путь до лога, может быть, кому-то окажется удобным пользоваться такой командой:
```
INST='<fqdn инстанса>' TASK='<название задачи>' bash -c 'less /mnt/nanny/production_market_solomon_pusher_scheduler_"${INST:0:3}"/${INST}/solomon-pusher/${TASK//\./\/}.log'
```
Например, чтобы посмотреть лог задачи `checkouter.delivery.delayed-delivery-based-on-shipping` на инстансе `sas2-0428-f60-sas-market-prod--336-11926.gencfg-c.yandex.net` за сегодня, можно использовать такую команду:
```
INST='sas2-0428-f60-sas-market-prod--336-11926.gencfg-c.yandex.net' TASK='checkouter.delivery.delayed-delivery-based-on-shipping' bash -c 'less /mnt/nanny/production_market_solomon_pusher_scheduler_"${INST:0:3}"/${INST}/solomon-pusher/${TASK//\./\/}.log'
```
Если логи нужны за вчерашний день, то, вероятно, нужно скорректировать имя файла, добавив в него дату сегодняшнюю, если сегодня уже произошла ротация логов, например:
```
INST='sas1-9634-64f-sas-market-prod--336-11926.gencfg-c.yandex.net' TASK='checkouter.ff.delayed-packaging-by-shipment-date' bash -c 'less /mnt/nanny/production_market_solomon_pusher_scheduler_"${INST:0:3}"/${INST}/solomon-pusher/${TASK//\./\/}.log.2021-05-19'
```
Таким образом в данном примере при выполнении команды 19 мая после ротации можно посмотреть логи, которые записывались 18 мая.
Если логи нужны за более давние дни, после которых прошли уже 2 ротации, то кроме даты в имени файла понадобится расширение `.gz`, т.к. логи затем сжимаются (если прошло больше, чем 2 суток после записи логов). Например, так можно посмотреть логи за 13 мая (в имени файла указана дата ротации, которая происходит на следующий день):
```
INST='sas1-9634-64f-sas-market-prod--336-11926.gencfg-c.yandex.net' TASK='checkouter.ff.delayed-packaging-by-shipment-date' bash -c 'less /mnt/nanny/production_market_solomon_pusher_scheduler_"${INST:0:3}"/${INST}/solomon-pusher/${TASK//\./\/}.log.2021-05-14.gz'
```

Ротация логов производится с помощью утилиты `logrotate`, конфигурационный файл которой находится по [данной ссылке](https://a.yandex-team.ru/arc_vcs/market/infra/solomon-pusher-scheduler/src/main/conf/logrotate.d/solomon-pusher).

В связи с тем, что полные логи стали занимать слишком много места, в рамках тикета [MARKETINFRA-11244](https://st.yandex-team.ru/MARKETINFRA-11244) добавлена возможность по гибкой настройке количества строк из запроса, которые попалают в лог. Это регулируется с помощью переменной окружения `SP_MAX_SQL_LINES_IN_LOG_COUNT`. Если при запуске скриптов она не определена, то ограничений нет и sql-запрос логируется целиком. Если же она определена, то она рассматривается как целое число и из sql-запроса логируется не более, чем количество строк, указанное в этой переменной окружения. Также добавлена поддержка переменной окружения `SP_MAX_SOLOMON_BODY_SIZE_IN_LOG`, влияющей на вывод в лог тела запроса к Соломону. Если переменная окружения не определена, то тело запроса логируется целиком, без ограничений. Если же она определена, то её значение рассматривается как целое число, а тело запроса логируется только в том случае, если количество символов в нём не превышает заданное в переменной значение. Про конфигурирование переменных окружения при запуске скриптов можно прочитать [тут](https://wiki.yandex-team.ru/market/development/health/solomon-pusher-scheduler/#peremennyeokruzhenijaperedavaemyevdochernieprocessy).

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
Так же SQL будет сразу скопирован в буфер обмена и его сразу можно вставлять и исполнять.

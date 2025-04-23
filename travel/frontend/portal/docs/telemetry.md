# Телеметрия

Мы логируем запросы к нашим бекендам, записываем размеры бандлов на каждый релиз в кластер ClickHouse.
Запись реализована в Data-UI Core,
подробности настройки есть в документации [Data-UI](https://ui.yandex-team.ru/core/telemetry/clickhouse).

### Использование данных

-   Графики и логи на доске здоровья сервиса на вкладках [запросы к API](https://datalens.yandex-team.ru/huurcsd89uwse-travel-frontend?tab=oXD).
-   График размера бандлов в релизе в каждом [релизном тикете](https://st.yandex-team.ru/TRAVELFRONT/order:updated:false/filter?type=12).
-   Аналитика решения тикетов в трекере.

### Работа с кластером ClickHouse

Официальная [документация](https://clickhouse.tech/docs/en/) по ClickHouse.

Наш кластер находится в Yandex Cloud [travel-front-clickhouse](https://yc.yandex-team.ru/folders/foo33m9g9m98lqipih8r/managed-clickhouse/cluster/mdb1meos322mc6qs7jft),
для доступа нужны роли в IDM:

-   [Роли в сервисах / Сервисы Поискового портала / Яндекс.Путешествия / Внутренние Службы / Фронтенд Яндекс.Путешествий / Роли сервиса / Администратор MDB](https://idm.yandex-team.ru/system/abc#role=22742904,f-role-id=22742904)
-   [Роли в сервисах / Сервисы Поискового портала / Яндекс.Путешествия / Внутренние Службы / Фронтенд Яндекс.Путешествий / Роли сервиса / Администратор баз данных](https://idm.yandex-team.ru/system/abc#role=22742905,f-role-id=22742905).

Для подключения к базе данных нужно:

1. Зайти в [кластер на YC](https://yc.yandex-team.ru/folders/foo33m9g9m98lqipih8r/managed-clickhouse/cluster/mdb1meos322mc6qs7jft).
2. На вкладке "Пользователи" нужно добавить пользователя: указать логин, пароль и базы данных с которыми планируете работу.
3. На вкладке "Базы данных" кликнуть на кебаб меню и выбрать пункт "Подключиться".
4. Выбрать нужный способ и следовать инструкциям

Для выполнения SQL запросов можно использовать [WEB интерфейс](https://yc.yandex-team.ru/folders/foo33m9g9m98lqipih8r/managed-clickhouse/cluster/mdb1meos322mc6qs7jft?section=sql) в облаке на вкладке "SQL".

Также для подключения можно использовать десктопный клиент, например [DBeaver](https://dbeaver.io/).
Для подключения нужно:

1. Создать "Database Connection"
2. Выбрать SQL > ClickHouse
3. Указать Host, Port, Database (например api_logs), Username и Password (всю информацию можно взять в интерфейсе YC на вкладке "Базы Данных" > "Подключение" (у нужной БД))
4. Указать сертификат на вкладе Driver Properties: сделать параметр ssl = true, sslrootcert = путь-до-сертификата (например /usr/local/yandex-internal-root-ca/YandexInternalRootCA.crt)

### Базы данных

На момент написания документации в нашем кластере созданы следующие БД:

-   db_bundlemeter - размеры бандлов для каждого релиза
-   api_logs - запросы к бекендам
-   db_ticket_metrics - статистика из трекера

### Оценка работы кластера

В интерфейсе Яндекс Облака в разделе ["Мониторинги"](https://yc.yandex-team.ru/folders/foo33m9g9m98lqipih8r/managed-clickhouse/cluster/mdb1meos322mc6qs7jft?section=monitoring) есть графики различных метрик кластера:
свободное место, количество запросов, продолжительность запросов и тд

Для хранения логов своей работы ClickHouse использует системную базу данных [system](https://clickhouse.tech/docs/en/operations/system-tables/).
Например, таблица [system.query_log](https://clickhouse.tech/docs/en/operations/system-tables/query_log/) содержит подробную информацию о всех поступивших в базу данных запросах.
С остальными таблицами можно ознакомится в [документации](https://clickhouse.tech/docs/en/operations/system-tables/) ClickHouse.

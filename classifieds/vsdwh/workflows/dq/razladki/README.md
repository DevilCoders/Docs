## Разладки

Конфиги алертов и ETL-процессов доставки метрик для статистичеких проверок. Для работы с конфигами используется CLI-утилита [lama](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama).

Проекты:
- Solomon - [vertis-razladki](https://solomon.yandex-team.ru/admin/projects/vertis-razladki)
- Juggler -  [vertis-razladki](https://juggler.yandex-team.ru/project/vertis-razladki/dashboard?project=vertis-razladki)
- Reactor -  [/verticals/vertis-bi/dq/razladki](https://reactor.yandex-team.ru/browse/resolve?path=/verticals/vertis-bi/dq/razladki)


### Структура репозитория
```sql
.
├── auto                   -- домен
│  ├── events              -- источник данных
│  │  ├── card_view        -- метрика
│  │  │  ├── android       -- платформа
│  │  │  │  ├── yql        -- скрипты для сбора метрик
│  │  │  │  └── lama.yaml  -- конфиг
│  │  │  └── ...
│  │  └── ...
│  └── cofe
│     ├── phone_call
│     └── ...
├── realty
├── ...
└── lama.yaml              -- конфиг общих объектов Solomon (каналы нотификаций и т.п.)
```

### Как добавить новую разладку
1. Отправить метрики в Solomon

   Метрики сofe уже есть в соответствующем проекте:
   - [cofe_autoru](https://solomon.yandex-team.ru/admin/projects/cofe_autoru/metrics) - метрики сofe Авто.ру  
   - [cofe_realty_app](https://solomon.yandex-team.ru/admin/projects/cofe_realty_app/metrics) - метрики аппов в Яндекс.Недвижимости

    Кастомные метрики нужно отправлять в проект [vertis-razladki](https://solomon.yandex-team.ru/admin/projects/vertis-razladki). Подробнее про доставку своих метрик в разделе [доставка метрик](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/workflows/dq/razladki#dostavka-kastomnyh-metrik).
2. Определить алгоритм разладки. 

   В первую очередь стоит посмотреть на алгоритмы из [пресетов](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/workflows/dq/razladki#presety-dlya-algoritmov). Если там нет ничего подходящего, можно написать свой на [языке запросов Solomon](https://docs.yandex-team.ru/solomon/concepts/querying) или использовать сервис [razladki-wow](https://razladki-wow.n.yandex-team.ru). Подробнее про разладки можно прочитать на wiki - https://wiki.yandex-team.ru/razladki/wowguide. Новый алерт желательно оберунть в пресет, по аналогии с остальными, чтобы его было удобно переиспольовать.
3. Подготовить конфиг [lama.yaml](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama)
4. Сделать PR. 

   Валидация конфига и установка в testing выполняется в джобе `Lama CI`. После мерджа PR новые сущьности Reactor/Solomon/Juggler будут установлены в production-окружение.
5. После мерджа PR можно создавать правила нотификации в [Juggler](https://juggler.yandex-team.ru/notification_rules?project=vertis-razladki)

### Доставка кастомных метрик
Кастомные метрики хранятся в проекте в проекте [vertis-razladki](https://solomon.yandex-team.ru/admin/projects/vertis-razladki), в отдельном сервисе для кажого домена и источника данных:
- [auto_events](https://solomon.yandex-team.ru/admin/projects/vertis-razladki/metrics?selectors=service%3D%22auto_events%22%2C+cluster%3D%22production%22) - метрики Авто.ру по event-логу
- [auto_billing](https://solomon.yandex-team.ru/admin/projects/vertis-razladki/metrics?selectors=service%3D%22auto_billing%22%2C+cluster%3D%22production%22) - метрики Авто.ру по логу биллинга
- [realty_events](https://solomon.yandex-team.ru/admin/projects/vertis-razladki/metrics?selectors=service%3D%22realty_events%22%2C+cluster%3D%22production%22) - метрики Недвижимости и Аренды по event-логу
- [realty_appmetrica](https://solomon.yandex-team.ru/admin/projects/vertis-razladki/metrics?selectors=service%3D%22realty_appmetrica%22%2C+cluster%3D%22production%22) - метрики Недвижимости и Аренды по AppMetrica


##### Правила именования метрик

Рекомендуется придерживаться следующего шаблона: ```<metric_name>.<platform>.<dim_1>.<dim_N>.<metric_type>```

Где:
- `metric_name` - название метрики
- `platform` - платформа (опционально)
- `dim_1`, `dim_N` - набор измерений (опционально). Вместо измерений можно указать лейблы
- `metric_type` - тип метрики. Например: `count` - кол-во событий, `users` - кол-во пользователей, `share` - доля

Примеры:
- `card_view.ios.new.dealer.count` - кол-во просмотров карточек с iOS в дилерах в новых авто
- `phone_call.android.users` - кол-во пользователей смотревших телефоны в Android
- `deeplink_error.no_internet.share` - доля ошибок открытия внешней ссылки

##### Граф
Для поставки метрик из YQL или CH можно использовать граф - [wf_solomon_collect_metrics](https://reactor.yandex-team.ru/browse/resolve?path=/verticals/vertis-bi/dq/razladki/wf_solomon_collect_metrics). Для этого нужно подготовить запрос для сбора метрик и конфиг реакции для регулярной поставки. Примеры реакций:
 - YQL - [dq/razladki/auto/events](https://a.yandex-team.ru/arc/trunk/arcadia/classifieds/vsdwh/workflows/dq/razladki/auto/events)
 - CH vsdwh - [dq/razladki/auto/billing](https://a.yandex-team.ru/arc/trunk/arcadia/classifieds/vsdwh/workflows/dq/razladki/auto/billing)
 - CH AppMetrica - [dq/razladki/realty/appmetrica](https://a.yandex-team.ru/arc/trunk/arcadia/classifieds/vsdwh/workflows/dq/razladki/realty/appmetrica)

Требования к запросу:
1) Качество метрик нужно проверить **до отправки** в Solomon, т.к. удалить их будет [не просто](https://clubs.at.yandex-team.ru/solomon/1147).
2) Фиксированная структура выборки:
    | Поле | Тип данных | Описание |
    |---|---|---|
    | `ts` | UInt32 | Unixtime
    | `metric` | String | Название метрики в формате: `one.two.three`
    | `value` | UInt64 | Значение метрики

    Пример данных:
    ```csv
    1642377600  card_view.ios.new.dealer.count  96756
    1642377600  card_view.ios.new.dealer.users  39243
    1642377600  card_view.ios.used.user.count   50004
    ```
3) В YQL-запросах выборку нужно сохранить в `INSERT INTO {{output1}}`, в CH достаточно селекта

Параметры реакции:
| Название | Обязательный | Описание | Формат |
|---|---|---|---|
| `query_type` | Да | Тип запроса | *String*, возможные значения: `yql`, `ch_vsdwh`, `ch_metrica` |
| `query_arcanum_path` | Да |Путь к запросу в аркадии | *String*, пример `classifieds/vsdwh/workflows/dq/razladki/auto/events/card_view/android/yql/query.sql` |
| `query_params` | Нет |Список параметров передаваемых в запрос. Для YQL вместо `{{param["name"]}}` будет подставляться *value* (доступны [модификаторы](https://wiki.yandex-team.ru/nirvana-ml/ml-marines/#modifikatory)). Для запросов к CH используеются Jinja2 шаблонизация | *List of Strings*, формат: `param=value` |
| `metric_labels` | Нет | Список лейблов | *List of Strings*, формат: `label=value` |
| `solomon_cluster` | Да | [Кластер](https://docs.yandex-team.ru/solomon/concepts/glossary#cluster) | *String*, возможные значения: `production`, `testing`
| `solomon_project` | Да | [Проект](https://docs.yandex-team.ru/solomon/concepts/glossary#project) | *String*, пример: `vertis-razladki`
| `solomon_service` | Да | [Сервис](https://docs.yandex-team.ru/solomon/concepts/glossary#service) | *String*, пример: `auto_events`

### Пресеты для алгоритмов
#### 1. [simple-learn-seasonal](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/presets/projects/vertis-razladki/solomon/alerts/simple-learn-seasonal.jinja)

Алгоритм проверяет отклонение в значениях заданной метрики по [правилу нескольких сигм](https://wiki.yandex-team.ru/razladki/wowguide/#normalizacija/praviloneskolkixsigm). По умолчанию проверяются коридор из **3-х** сигм в обе стороны с окном обучения **28** дней.

{% note tip %}

Прогнать алерт по историческим данным и подобрать оптимальные параметры для данного алгоритма можно в интерфейсе разладок - https://razladki-wow.n.yandex-team.ru/workspace/1688/version/7

{% endnote %}

##### Параметры
| Название | Значение по умолчанию | Описание | Формат |
|---|---|---|---|
| `multi_alert` | false | Сгруппировать метрики в [мульти-алерт](https://docs.yandex-team.ru/solomon/concepts/alerting/#multi-alerts). Рекомендуется если селектор возвращает множество метрик и все нужно проверять по заданному алгоритму. В [правилах нотификаций в Juggler](https://docs.yandex-team.ru/juggler/notifications/on_change#options) для мультиалерта **нужно указать параметр** `min_interval` (число секунд, чаще которых не будут отправляться оповещения), т.к. проверка будет флапать если сработает один из сабалертов и будет спам уведомлений | `true`/`false`|
| `multi_alert_metrics_prefix` |  | Префикс для метрик мультиалерта. При отправке событий в Juggler будет использоваться следующий шаблон: `<multi_alert_metrics_prefix>.<metric>` | Пример: `auto.events` |
| `channel_id` | *<Обязательный параметр>* | Идентификатор [канала уведомлений](https://docs.yandex-team.ru/solomon/concepts/glossary#notification-channel) в Solomon | Канал должен быть предварительно добавлен в конфиг [razladki/lama.yaml](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/workflows/dq/razladki/lama.yaml). Общий канал для разладок `vertis-razladki-juggler` |
| `metric_code` | *<Обязательный параметр>* | Уникальный код метрики. Используется как `service` в Juggler | Пример: `auto.cofe.phone_call.android.count` |
| `metric_name` | *<Обязательный параметр>* | Название метрики. Используется как заголовок алерта в Solomon | Пример: `[auto][cofe] Просмотры телефонов (Android)`|
| `sensor` | *<Обязательный параметр>* | [Селектор](https://docs.yandex-team.ru/solomon/concepts/glossary#selector) в Solomon | Список множества метрик и значений в формате `key: value`|
| `lower_crit_sigma` | -3.0  | Нижний порог отклонения от среднего (в стандартных отклонениях). Можно указать WARN и CRIT пороги через ; в любом порядке. Если задано одно число, подразумевается критический порог | |
| `lower_crit_sigma` | 3.0  | Верхний порог отклонения от среднего (в стандартных отклонениях). Можно указать WARN и CRIT пороги через ; в любом порядке. Если задано одно число, подразумевается критический порог | |
| `crit_count` | 1 | Количество плохих точек, необходимое для разладок |  |
| `input_points` | 1 | Данные по которым будет приниматься решение о разладке | Количество точек или [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration) |
| `train_points` | 1 | Данные для обучения. Желательно, чтобы не пересекался с данными для принятия решения | Количество точек или [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration) |
| `train_period_duration` | 28d | Длительность предыстории, которая необходима для оценки разладки в заданный момент времени | [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration). Примеры: `5s`, `4m`, `3.5h`, `2d`, `1.5w`; где s - секунды, m - минуты, h - часы, d - дни, w - недели  |
| `evaluation_window` |  *<train_period_duration>* | Окно вычисления алерта. По умолчанию равно периоду обучения | [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration) |
| `buckets` | 1 | Количество временных корзин, на которые разбиваются сутки. Больше корзин - лучше детализация, но сильнее переобучение. Меньше корзин - меньше переобучение, но хуже детализация. Идеальное значение - золотая середина между этими крайностями | |
| `drop` | 0.1 | Доля количества отбрасываемых экстремальных значений | |
| `profile` |  `anyday` | Разбиение дней недели на корзинки. Для каждой корзинки алгоритм будет обучаться независимо. Полезно тогда, когда поведение ряда сильно зависит от дня недели, однако требует больше данных для обучения | `anyday` - без разбивки по дням, `work` - группировать по будням (Пн-Пт) и выходным (Сб-Вс), `daily` - учитывать каждый день недели отдельно, `sunsat` - группировать по будням (Пн-Пт), субботам и воскресеньям (отдельно), `weekend` - группировать по будням (Пн-Пт), пятницам, субботам и воскресеньям (отдельно). Подробнее про [сезонные тренды](https://wiki.yandex-team.ru/users/uranix/realizacija-sezonnogo-trenda-v-solomon-v-jazyke-analiticheskix-zaprosov/#kalendar)|

##### Пример
```yaml
solomon:
  project_id: vertis-razladki
  alerts:
  - preset: projects/vertis-razladki/solomon/alerts/simple-learn-seasonal
    preset_options:
      channel_id: vertis-razladki-juggler
      metric_code: "auto.cofe.phone_call.android.count"
      metric_name: "[auto][cofe] Просмотры телефонов (Android)"
      sensor:
        project: cofe_autoru
        cluster: production
        service: metrics_daily
        metric: phone_call.android.count
        observation: 459
        testid: 0
      lower_crit_sigma: -3.0
      upper_crit_sigma: 5.0

juggler:
  checks:
  - service: "auto.cofe.phone_call.android.count"
    preset: projects/vertis-razladki/juggler/check
```

#### 2. [simple-threshold](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/presets/projects/vertis-razladki/solomon/alerts/simple-threshold.jinja)

Алерт срабатывает если значения метрики выступают за границы заданных пороговых значений.

##### Параметры
| Название | Значение по умолчанию | Описание | Формат |
|---|---|---|---|
| `multi_alert` | false | Сгруппировать метрики в [мульти-алерт](https://docs.yandex-team.ru/solomon/concepts/alerting/#multi-alerts) | `true`/`false`|
| `multi_alert_metrics_prefix` |  | Префикс для метрик мультиалерта. При отправке событий в Juggler будет использоваться следующий шаблон: `<multi_alert_metrics_prefix>.<metric>` | Пример: `auto.events` |
| `channel_id` | *<Обязательный параметр>* | Идентификатор [канала уведомлений](https://docs.yandex-team.ru/solomon/concepts/glossary#notification-channel) в Solomon | Канал должен быть предварительно добавлен в конфиг [razladki/lama.yaml](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/workflows/dq/razladki/lama.yaml). Общий канал для разладок `vertis-razladki-juggler` |
| `metric_code` | *<Обязательный параметр>* | Уникальный код метрики. Используется как `service` в Juggler | Пример: `auto.billing.withdraw.money.shift_1d.multi` |
| `metric_name` | *<Обязательный параметр>* | Название метрики. Используется как заголовок алерта в Solomon | Пример: `[auto][billing] Сумма списаний (now/1d)`|
| `sensor` | *<Обязательный параметр>* | [Селектор](https://docs.yandex-team.ru/solomon/concepts/glossary#selector) в Solomon | Список множества метрик и значений в формате `key: value`|
| `evaluation_window` | 28d  | Окно вычисления алерта (временной промежуток, показанный на графике) | [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration) |
| `lower_threshold` | 0  | Нижний порог | |
| `upper_threshold` | inf  | Верхний порог. Если не указан, проверяется **только** нижний порог | |
| `crit_count` | 1 | Количество плохих точек, необходимое для разладок |  |
| `input_points` | 1 | Данные по которым будет приниматься решение о разладке | Количество точек или [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration) |


##### Пример
```yaml
solomon:
  project_id: vertis-razladki
  alerts:
  - preset: projects/vertis-razladki/solomon/alerts/simple-threshold
    preset_options:
      channel_id: vertis-razladki-juggler
      metric_code: "auto.cofe.cars.favourite_add.count"
      metric_name: "[auto][cofe] Добавления в избранное "
      sensor:
        project: cofe_autoru
        cluster: production
        service: metrics_daily
        metric: cars.favourite_add.count
        observation: 459
        testid: 0
      lower_threshold: 120000
      upper_threshold: 400000

juggler:
  checks:
  - service: "auto.cofe.cars.favourite_add.count"
    preset: projects/vertis-razladki/juggler/check
```

#### 3. [simple-shift-diff](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analytics/tools/lama/presets/projects/vertis-razladki/solomon/alerts/simple-shift-diff.jinja)

Проверяется отклонение в текущем значении метрики со значениями за другой временной интервал. Подходит для метрик с нарастающей суммой. По умолчанию сравнивается с данными за вчера.

##### Параметры
| Название | Значение по умолчанию | Описание | Формат |
|---|---|---|---|
| `multi_alert` | false | Сгруппировать метрики в [мульти-алерт](https://docs.yandex-team.ru/solomon/concepts/alerting/#multi-alerts) | `true`/`false`|
| `multi_alert_metrics_prefix` |  | Префикс для метрик мультиалерта. При отправке событий в Juggler будет использоваться следующий шаблон: `<multi_alert_metrics_prefix>.<metric>` | Пример: `auto.events` |
| `channel_id` | *<Обязательный параметр>* | Идентификатор [канала уведомлений](https://docs.yandex-team.ru/solomon/concepts/glossary#notification-channel) в Solomon | Канал должен быть предварительно добавлен в конфиг [razladki/lama.yaml](https://a.yandex-team.ru/arc_vcs/classifieds/vsdwh/workflows/dq/razladki/lama.yaml). Общий канал для разладок `vertis-razladki-juggler` |
| `metric_code` | *<Обязательный параметр>* | Уникальный код метрики. Используется как `service` в Juggler | Пример: `auto.billing.withdraw.money.shift_1d.multi` |
| `metric_name` | *<Обязательный параметр>* | Название метрики. Используется как заголовок алерта в Solomon | Пример: `[auto][billing] Сумма списаний (now/1d)`|
| `sensor` | *<Обязательный параметр>* | [Селектор](https://docs.yandex-team.ru/solomon/concepts/glossary#selector) основной метрики | Список множества метрик и значений в формате `key: value`|
| `evaluation_window` | 1d  | Окно вычисления алерта (временной промежуток, показанный на графике) | [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration) |
| `shift_sensor` | *<sensоr>* | [Селектор](https://docs.yandex-team.ru/solomon/concepts/glossary#selector) метрики со смещением. По умолчанию используется селектор для основной метрики | Список множества метрик и значений в формате `key: value`|
| `shift_duration` | 1d  | Смещение в прошлое, со значением из которого будет сравниваться текущее значение метрики. Если задан `shift_sensor` смещение будет применено к нему | [Duration](https://docs.yandex-team.ru/solomon/concepts/querying#duration) |
| `diff_threshold` | 30  | Порог срабатывания алерта (в процентах) |  |
| `delay_sec` | 1800  | Задержка в данных метрики (в секундах) |  |

##### Пример
```yaml
solomon:
  project_id: vertis-razladki
  alerts:
  - preset: projects/vertis-razladki/solomon/alerts/simple-shift-diff
    preset_options:
      channel_id: vertis-razladki-juggler
      metric_code: "auto.billing.withdraw.moving_money.1d_shift"
      metric_name: "[auto][billing] Сумма списаний (diff today/1d)"
      sensor:
        project: vertis-razladki
        cluster: production
        service: auto_billing
        metric: withdraw.moving_money
      shift_duration: 1d
      diff_threshold: 30
      delay_sec: 1800

  - preset: projects/vertis-razladki/solomon/alerts/simple-shift-diff
    preset_options:
      channel_id: vertis-razladki-juggler
      metric_code: "auto.billing.withdraw.moving_money.1w_mean"
      metric_name: "[auto][billing] Сумма списаний (diff today/1w_mean))"
      sensor:
        project: vertis-razladki
        cluster: production
        service: auto_billing
        metric: withdraw.moving_money
      shift_sensor:
        project: vertis-razladki
        cluster: production
        service: auto_billing
        metric: withdraw.moving_money_1w_mean
      shift_duration: 0d
      diff_threshold: 30
      delay_sec: 1800

juggler:
  checks:
  - service: "auto.billing.withdraw.moving_money.1d_shift"
    preset: projects/vertis-razladki/juggler/check
    
  - service: "auto.billing.withdraw.moving_money.1w_mean"
    preset: projects/vertis-razladki/juggler/check
```

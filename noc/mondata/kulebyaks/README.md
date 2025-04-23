## Кулебяки
**Кулебяка** – единое окно входа в мониторинг. Параметры проверочных скриптов, алерты в solomon, агрегация и оповещения в juggler –
теперь всё в одном файле. Важным концептуальным отличием от старого подхода является ориентирование на группы хостов на каждый сервис,
а не по проверки вообще на всех хосты, где эта проверка может работать. Хотя технически и возможно указать фильтр на все хосты в RT, мы
осуждаем такой подход.

### Концепция:
Диаграмма связей между mondata, solomon и juggler:
![диаграмма](https://jing.yandex-team.ru/files/gescheit/mondata1%20%285%29.png)

Порядок действий по добавлению новых проверок:
![диаграмма](https://jing.yandex-team.ru/files/gescheit/chdiag%20%281%29.png)


В Solomon попадают метрики, собранные с помощью telegraf, grad и других систем. Применяя полученную от кулебяки программу
к этим данным, Solomon меняет статус алерта на один из: OK, ALARM, WARN, NODATA и т.д. Этот статус постоянно
отправляется в juggler как raw event (это настраивается в notification channels).

Аналогично работают проверочные скрипты. Juggler-client или zabbix-agent исполняют скрипт и отсылают его результат как raw event в juggler.

Далее mondata настраивает агрегат в juggler,
который собирает сырые события в одно по некоторому признаку. Например, для 100 серверов можно настроить агрегат, который сообщит о проблеме,
только если на 50 из них есть raw event в состоянии CRIT. Затем mondata настраивает notification в juggler, в котором указано, как и
кому отправить такое событие.

Раньше mondata поддерживала каждый модуль отдельно: генераторы solomon алертов в папке solomon/ (и синхронизатор update_solomon.py),
генератор агрегатов juggler – в juggler/ (и синхронизатор update_juggler.py).
Кулебяка же поддерживает все модули одновременно. Этим объясняется и название: один пирог с разными начинками.

Каждая кулебяка (файл в kulebyaks/) представляет собой описание всех проверок (juggler aggregate или solomon alert) для одного сервиса.
Предыдущий подход предполагал отдельный файл на каждую проверку, и в такой парадигме было непросто найти, откуда приезжает проверка.
Кулебяка предполагает (но не ограничивает) использование одной группы хостов и автоматическое размножение проверки и оповещений для этих хостов.

### Кулебяки:
Кулебяка представляет собой yaml-файл вида
```yaml
# AUTHOR: ololo@yandex-team.ru
# Теги по которым будет отправляться статус синхронизации
# JUGGLER_TAGS: notify_nocdev_teleg,nocdev_dashboard
- name: funny service
  description: funny service monitoring
  hosts: rt:{filter}  # список хостов, для которых будут создаваться solomon/juggler проверки. Обязательное поле
  juggler_namespace: my_namespace  # будет использоваться в качестве namespace в агрегатах, переопределяя ранее указанные значения
  defaults:
    juggler_host: my_service  # будет использоваться как host в агрегатах, если явно не указан другой
  resp: {}  # настройки оповещений
  solomon: []  # solomon alerts (из директории solomon_templates)
  aggregates: []  # juggler aggregates (из директории juggler_templates)
  templates: []  # глобальные шаблоны (из директории templates)
  scripts: []  # запуск скриптов
  groups: []  # группа проверок
```

В секциях solomon и aggregates можно использовать шаблоны (см. ниже), но они должны возвращать соответствущие проверки.
В секции templates указываются шаблоны из папки templates, они могут возвращать любой набор проверок juggler/solomon.

### Проверки прямо в кулебяке (без шаблона)

#### Solomon
Мондата может выступать генератором проверок solomon, подробную документацию на solomon [читайте тут](https://solomon.yandex-team.ru/docs/ "Solomon").
Алерт работает так: периодически solomon выбирает данные по указанному фильтру, выполняет указанные преобразования (например, подсчет среднего значения)
и меняет статус алерта в зависимости от результата. Статус алерта в зависимости от настроек может постоянно отправляться в juggler или еще куда-нибудь.
Пример одного solomon alert
```yaml
solomon:
  - alert_name: slbcloghandler process cpu usage
    description: мониторинг процесса slbcloghandler.
    program: |
      let cpu_usage = {project="slbcloghandler", cluster="all", service="procstat", sensor="cpu_usage", process_name="slbcloghandler", host="%(host)s"};
      let avg_cpu_usage = avg(cpu_usage);
      let message_val = to_fixed(avg_cpu_usage, 0);
      alarm_if(avg_cpu_usage > 400);
    period: 900
    message_template: "slbcloghandler cpu_usage is too high: {{expression.message_val}}%"
    notification_channels: [ kulebyaks-noc-juggler ]
    help_key: "slbch-proc-usage"
    juggler_tags: [ "slbcloghandler_process" ]
    juggler_service: "slbcloghandler_process"
```
Доступные поля:

**hosts** (List[str]) – Список хостов. Если не указан, то используется список хостов из кулебяки.
**program** (str) – [Программа](https://solomon.yandex-team.ru/docs/concepts/alerting/#expression "Solomon alert") алерта.
**alert_name** (str) – Имя алерта.
**alert_id** (str) - Уникальный идентификатор алерта. Не делай его длинным.
**message_template** (str) – [Шаблон сообщения](https://docs.yandex-team.ru/solomon/concepts/alerting/#templates).
**help_key** (str) – [Ключ](https://a.yandex-team.ru/arcadia/noc/mondata/mondata#21-внести-информацию-о-проблеме-и-пути-её-решения-в-вики) help_key.
**period** (int) – Окно в секундах, за которое будут выбраны данные.
**project_id** (str = noc) – [project](https://docs.yandex-team.ru/solomon/concepts/glossary#project), в котором будет создан алерт
**notification_channels** (List[str] = None) – Список [каналов оповещения](https://docs.yandex-team.ru/solomon/concepts/glossary#notification-channel).
kulebyaks-noc-juggler – стандартный канал для отсылки в juggler.
**annotations** (Dict[str, str] = None) – [Аннотации](https://docs.yandex-team.ru/solomon/concepts/glossary#annotation).
**group_by_labels** (Optional[List[str]] = None) – Группировка [мультиалерта](https://docs.yandex-team.ru/solomon/concepts/alerting/#multi-alerts).
**delay_seconds** (int = 0) – [Смещение](https://docs.yandex-team.ru/solomon/concepts/alerting/#alert-params) окна в секундах.
**no_points_policy** (Optional[Union[str, NoPointsPolicy]] = None) – Политика в случае отсутствия данных. Возможные варианты: NO_POINTS_DEFAULT, NO_POINTS_OK,
NO_POINTS_WARN, NO_POINTS_ALARM, NO_POINTS_NO_DATA, NO_POINTS_MANUAL. По умолчанию NO_POINTS_MANUAL. Выбранная политика сработает, если фильтр
находит что-то в индексе, но не находит данных. NO_POINTS_MANUAL означает, что статус алерта будет вычислен в программе.
Например так: nodata_if(count(data) == 0).
**resolved_empty_policy** (Optional[Union[str, ResolvedEmptyPolicy]] = None) – Политика в случае отсутствия индекса. Возможные варианты: RESOLVED_EMPTY_DEFAULT, RESOLVED_EMPTY_OK,
RESOLVED_EMPTY_WARN, RESOLVED_EMPTY_ALARM, RESOLVED_EMPTY_NO_DATA, RESOLVED_EMPTY_MANUAL. По умолчанию RESOLVED_EMPTY_NO_DATA. Выбранная политика сработает, если фильтр
ничего не находит в индексе (например, выбранный хост никогда ничего не слал).
**juggler_tags** (Optional[List[str]] = None) – Список тегов для juggler.
**juggler_service** (Optional[str] = None) – Имя сервиса в juggler.
**description** (str = "") – Описание алерта.
**extra_program_vars** (Optional[Dict[str, str]] = None) – Переменные, которые будут подставлены в шаблон program в формате "%(threshold)s"
**use_fqdn_juggler** - Использовать FQDN в жагглерных событиях.

Переменные из extra_program_vars подставляются в **program** так:
```yaml
extra_program_vars: {"alarm_threshold": 123}
# в program
alarm_if(oom_sum > %(alarm_threshold)s);
```
Кроме extra_program_vars всегда доступны переменные host и fqdn.
```
let retransmit = { host="%(fqdn)s",
```


#### Juggler
Mondata лишь настраивает juggler, поэтому подробную документацию по juggler [читайте тут](https://docs.yandex-team.ru/juggler/ "Juggler").
Агрегат работает так: периодически juggler выбирает сырые события по фильтру children и прогоняет по ним логику агрегации. В результате
получается новый статус. Например, если используется агрегатор logic_or, то когда хотя бы одно событие будет в CRIT – агрегат будет в CRIT.

Пример агрегата:
```yaml
aggregates:
  - host: slbcloghandler
    service: balancer_status
    description: slbcloghandler balancers status
    tags:
      - slbcloghandler
    ttl: 300
    namespace: nocdev
    aggregator: more_than_limit_is_problem
    aggregator_kwargs:
      crit_limit: 10
      mode: percent
      warn_limit: 1
    children:
      - group_type: EVENTS
        host: tag=slbcloghandler & tag=type_balancer_status
        service: all
        instance: all
```
Параметры нового агрегата:
**host** – Хост проверки.
**service** – Сервис проверки.
**tags** – Список тегов для удобного поиска по ним.

Параметры фильтрации сырых событий:
**children** (List[Dict]) – Объекты, которые надо агрегировать. По умолчанию – пустой массив.
Формат [{"host": "host1", "group_type": "HOST", "service": children_service}]. Подробности в [доке](https://docs.yandex-team.ru/juggler/aggregates/groups).
**children_service** (str) – Service сырых событий.
**children_hosts** (List[str]) – Список хостов. По умолчанию берётся из ключа `hosts` кулебяки.
Варианты указания:
- children: список словарей по [доке](https://docs.yandex-team.ru/juggler/aggregates/groups).
  Дополнительно к group_type из доки есть поддержка RT(хостнеймы из RT и добавленым фильтром and [zabbix monitoring]), RTALL(FQDN из RT), CGROUP_SHORT(хостнеймы из conductor).
- children_service: service из поля children_service, а хосты из `hosts` самой кулебяки.
  Если установлен флаг `_use_children_fqdns`, то будут использоваться fqdn вместо коротких имен.

Параметры агрегатов:
**ttl** – Время, после которого зажигается NO DATA, по умолчанию используется дефолт сервера.
**refresh_time** – Время обновления проверки, по умолчанию используется дефолт сервера.
**aggregator** – Имя агрегатора, по умолчанию пустой.
**aggregator_kwargs** – Словарь с параметрами агрегатора.

Прочее:
**active** – Имя модуля активной проверки, по умолчанию пустое.
**active_kwargs** – Словарь с параметрами модуля активной проверки.
**check_options** – Словарь с опциями для пассивной проверки, по умолчанию пустой.
**flaps_config** – Конфигурация флаподава, по умолчанию – выключен.
**notifications** – Список нотификаций, по умолчанию пустой.
**meta** – Словарь с метаданными.
**namespace** – Имя пространства имен проверки для ограничения доступа.
**description** – Строковое описание.
**pronounce** – То, как проверка будет вам зачитана в случае нотификации по телефону.

#### Groups

Используется в тех случаях, когда есть необходимость расположить проверки рядом. В корне кулебяки
проверки разбиты по типам, и если их много, то расстояние между алертом в соломоне и жагглерном может быть большим и
потребуется больший усилий, чтобы осознать связь.

Пример с расположенным рядом генератором вызова скрипта и агрегата.
```yaml
  groups:
    - scripts:
        - { script: process_status.sh, arguments: [ slbcloghandler ], interval: 30, service: &proc_status slbcloghandler_proc_status }
      aggregates:
        - templates:
            - proc_status:
                arguments: { host: slbcloghandler, service: slbcloghandler_proc_status, children_service: *proc_status }
```

#### Script

Кулебяка генерирует конфигурацию zabbix/juggler для запуска проверочных скриптов.
Пример:
```yaml
  scripts:
    - {script: olo.sh, interval: 90}
```

Параметры скриптов:
**script** (str) – Имя скрипта.
**arguments** (List[str]) – Аргументы скрипта.
**interval** (int) – Частота запуска в секундах.
**format** (str) - Один из nagios, json или wrapper. Подробнее смотри раздел juggler-client ниже.
**tags** (List[str]) - Список тегов которые будут добавлены к результату проверки. Работает только с
format==wrapper.
**delegate_host** (str) - запустить проверку на другом хосте. Если в аргументах указать '$host', то проверка размножится
на всех хосты из кулебяки с заменой этой переменной.

Если в аргументах встречается '{...}', то ... раскроется в список хостов через функцию expand_hosts().
Например
```yaml
check_path: script.py, arguments: ["{rt:{сервер grad}}"]
```
Аргумент "{rt:{сервер grad}}" заменится на "iva-b-grad1.yndx.net,iva-b-grad2.yndx.net".

Сами скрипты проверки нужно коммитить в директорию mondata/checks по [инструкции](https://a.yandex-team.ru/arcadia/noc/mondata/kulebyaks/QuickReferenceHandbook.md#хочу-запустить-свой-скрипт), либо доставлять их каким-то своим способом.

##### juggler-client
Для запуска скриптов без "лишних хопов" нужно указать format=nagios или format=json в соответствии с выводом.

format=wrapper будет запускать поставляемый вместе с мондатой  враппер juggler_client_wrapper.py.

Основные фишки враппера:
- **Важно!** Адаптирует формат заббикса из старых проверок "докулебячной эры". Дополнительно потребуется указать параметр service, соответствующий service сырого события в Juggler.
- Есть средства для отладки. Если существует файл /etc/mondata/wrapper_debug, то подробная информация про каждый запуск
проверки будет записана в /var/log/zabbix/wrapper.py.log.
- Автоматом подключается /var/spool/mondata/virtualenv/ для использования сторонних библиотек.
- В жагглер отправляется отдельное сообщение о статусе запуска скрипта с тегами juggler_client_wrapper.py и именем скрипта.
Таким образом можно поймать таймауты, ошибки выполнения и отсутствием скрипта.

##### zabbix
Агрегат для такого скрипта нужно делать по сервису mondata_check_{script} и обычному имени хоста или по тегу {script}.

### Шаблоны:
Шаблоны – это способ переиспользовать проверки. Если проверка предполагается для использования в нескольких кулебяках, то лучше создать её
как шаблон.
Шаблоны работают как обычные функции. В кулебяке указывается имя шаблона и его аргументы. Под капотом происходит поиск шаблона по имени,
и его исполнение.
Результат выполнения шаблона используется, как будто результат указан в самой кулебяке.
#### Шаблоны Solomon
Находятся в директории solomon_templates.
Пример
```python
import string

PROGRAM_TMPL = string.Template('''
let retransmit = non_negative_derivative({project="noc", service="nstat", host="%(host)s", sensor="TcpRetransSegs"});
let packets_recv = sum(non_negative_derivative({project="noc", service="net", host="%(host)s", sensor="packets_recv", interface="eth*"}) by sensor;

let retransmit_avg = avg(retransmit);
let packets_recv_avg = avg(packets_recv);
let ration = retransmit_avg/packets_recv_avg;
let message_short = to_fixed(ration, 5);
alarm_if(ration > $alarm_threshold);
warn_if(ration > $warn_threshold);
''')

def retransmit_rate(warn_threshold=0.1, alarm_threshold=1, juggler_service="retransmit_ratio"):
    res = {
        "alert_name": "retransmit ratio",
        "program": PROGRAM_TMPL.substitute(warn_threshold=warn_threshold, alarm_threshold=alarm_threshold),
        "window": 900,
        "help_key": "retransmit-ratio",
        "juggler_service": juggler_service,
        "message_template": "high retransmit ratio {{expression.message_short}}%",
    }
    return res
```

#### Шаблоны Juggler
Находятся в директории juggler_templates.
```yaml
aggregates:
  oom:
    description: мониторинг срабатываний oom killer
    service: oom_killer
    ttl: 120
    tags:
      - oom_killer
    aggregator: more_than_limit_is_problem
    aggregator_kwargs:
      mode: percent
      warn_limit: 1
      crit_limit: 10
    children_service: oom_killer
```

Переписывание результата шаблона делается через параметр override
```yaml
    - proc_status:
        arguments: { host: slbcloghandler, service: slbcloghandler_proc_status }
        override: { tags: [new_tag_1, new_tag2] }
```
В таком случае override заменит поле tags для всех возвращенных агрегатов из proc_status.

#### Глобальные шаблоны

Глобальные шаблоны возвращают и juggler и solomon алерты сразу.
Находятся в директории templates.
```yaml
# AUTHOR:
- name: service
...
  templates:
    system:
      arguments:
        cpu_alarm_threshold: 90
        cpu_warn_threshold: 80
        mem_alarm_threshold: 10
        mem_warn_threshold: 20
```
Сам шаблон
```python
from noc.packages.mondata_server.mondata.juggler_aggregate import new_juggler_aggregate
from noc.packages.mondata_server.mondata.kouilibiacs import new_solomon_alert, make_kulebyaks
import string

ALARM_THRESHOLD = 10
WARN_THRESHOLD = 20
PROGRAM_TMPL_PC = string.Template('''
let cpu_total_idle = {
    project='noc',
    cluster='all',
    sensor='usage_idle',
    service='cpu',
    $cpu,
    host='%(host)s'
};


let cpu_total_idle_avg = avg(cpu_total_idle);
let message_short = to_fixed(100 - cpu_total_idle_avg, 1);
alarm_if(cpu_total_idle_avg < $alarm_threshold);
warn_if(cpu_total_idle_avg < $warn_threshold);
''')

MEM_ALARM_THRESHOLD = 10
MEM_WARN_THRESHOLD = 20
SOLOMON_MEM_TEMPLATE_PC = string.Template('''
let available_percent = {
    project='noc',
    cluster='all',
    sensor='available_percent',
    service='mem',
    host='%(host)s'
};

let available_percent_avg = avg(available_percent);
let message_short = to_fixed(available_percent_avg, 1);
alarm_if(available_percent_avg < $alarm_threshold);
warn_if(available_percent_avg < $warn_threshold);
''')


def system(hosts, cpu_alarm_threshold=ALARM_THRESHOLD, cpu_warn_threshold=WARN_THRESHOLD,
           mem_alarm_threshold=MEM_ALARM_THRESHOLD, mem_warn_threshold=MEM_WARN_THRESHOLD):
    cpu_juggler_service = "system_koulibiac_cpu"
    mem_juggler_service = "system_koulibiac_mem"
    # тут пороги задаются как 100 - x
    cpu = new_solomon_alert(hosts,
                            alert_name="CPU load",
                            alert_id="cpu_load",
                            program=PROGRAM_TMPL_PC.substitute(alarm_threshold=100 - cpu_alarm_threshold,
                                                               warn_threshold=100 - cpu_warn_threshold,
                                                               cpu="cpu='cpu-total'"),
                            period=900,
                            help_key="highcpuload",
                            description="cpu monitoring",
                            message_template="high average CPU load {{expression.message_short}}%",
                            juggler_service=cpu_juggler_service,
                            notification_channels=["kulebyaks-noc-juggler"],
                            )
    cpu_agg = new_juggler_aggregate(host="koulibiac_cpu", service="koulibiac_cpu", children_hosts=hosts,
                                    children_service=cpu_juggler_service, description="cpu monitoring")

    mem = new_solomon_alert(hosts,
                            alert_name="mem utilization",
                            alert_id="mem_util",
                            program=SOLOMON_MEM_TEMPLATE_PC.substitute(alarm_threshold=mem_alarm_threshold,
                                                                       warn_threshold=mem_warn_threshold),
                            description="mem monitoring",
                            period=900,
                            help_key="highmemutil",
                            message_template="high mem utilization {{expression.message_short}}%",
                            juggler_service=mem_juggler_service,
                            notification_channels=["kulebyaks-noc-juggler"],
                            )
    mem_agg = new_juggler_aggregate(host="koulibiac_mem", service="koulibiac_mem", children_hosts=hosts,
                                    children_service=mem_juggler_service, description="mem monitoring")

    return make_kulebyaks(solomon=cpu + mem,
                           aggregates=[cpu_agg, mem_agg],
                           )

```
*После переезда в Аркадию изменились пути импорта вспомогательных модулей. Подробнее ниже в административной части*
### Подписки/Оповещения
Раздел используется для создания различных оповещений: сообщение в телеграмм, звонок, тикет и тп.
Автоматика добавляет тег вида $namespace_kulebyaks_$filename (например nocdev-kulebyaks-slbcloghandler.yaml) во все агрегаты в кулебяке.
Для этого тега создается подписка по параметру resp в корне кулебяки.
Пример:
```yaml
  resp:
    crit: pirogi@sms
    warn: pirogi@telegram
```
Автоматика создаст две подписки: crit будет приходить в sms пользователю pirogi, warn же уйдет ему в телеграм.
Шаблоны crit и warn определены в коде парсера кулебяк.

Произвольные подписки можно добавить так
```yaml
  notifications:
  - description: my notification
    namespace: nocdev
    selector: service=my_service&host=myhost
    template_name: on_status_change
    template_kwargs:
      status:
        - { from: OK, to: CRIT }
        - { from: OK, to: WARN }
      login:
        - pirogi
      method:
        - sms
```
Подробное описание полей смотри в [документации](https://docs.yandex-team.ru/juggler/notifications/basics)

### Даунтаймы из RT в juggler.
В RT есть кронжоба sync_downtimes.py. Скрипт резолвит фильтр "[zabbix monitoring offline]" в хосты
и создает в Juggler downtime для каждого хоста по фильтру host={rt_host}.

### Административная секция
#### Предисловие
Монолит проекта Mondata, лежащего в основе монитринга NOC и находившегося в репозитории https://noc-gitlab.yandex-team.ru/nocdev/mondata, был разбит на три части и перемещен в Аркадию.

1. Пакетная часть: https://a.yandex-team.ru/arcadia/noc/packages
2. Дашборды Heatmap: https://a.yandex-team.ru/arcadia/noc/heatmap/dashboards
3. Пользовательская часть: https://a.yandex-team.ru/arcadia/noc/mondata

#### Кулебяки в Аркадии

Если Вы ранее не работали с обще-Яндексовым репозиторием, изучите [стартер гайд](https://docs.yandex-team.ru/devtools/intro/quick-start-guide)

Для тестирования вносимых изменений необходимо собрать утилиту `update_kulebyaks` из пакетной части.

Для этого:

1. Скачиваем последнюю версию транка `arc checkout trunk && arc pull`
2. Запускаем тесты `ya make -t packages/mondata_server/cmd/update_kulebyaks` и проверяем, что при сборке не возникнет проблем
3. Собираем`ya make packages/mondata_server/cmd/update_kulebyaks`
4. По инструкции из Starter Guide создаем свою ветку и начинаем создавать мониторинг

Сейчас и далее пути для простоты указаны относительно папки noc в Аркадии. Вы можете скопировать собранную утилиту в удобную директорию, главное - случайно не загрузить ее вместе с написанной кулебякой.

**Важные изменения**

- в python шаблонах вспомогательные модули необходимо импортировать с помощью `noc.packages.mondata_server.mondata`.
- ключ `--kulebyaks_path` стал обязательным при отладке на своей рабочей станции.

#### Отладка работы Кулебяк
В процессе отладки можно посмотреть diff с текущими настройками:

```shell
packages/mondata_server/cmd/update_kulebyaks/update_kulebyaks --kulebyaks_path mondata/kulebyaks/ --diff
```
![дифф](https://jing.yandex-team.ru/files/gescheit/Screenshot%202021-08-18%20at%2000.51.16.png)
Если установлен dyff, то будет использован он, так как его вывод компактнее.

Полный же дамп получить через опцию --dump:
```bash
packages/mondata_server/cmd/update_kulebyaks/update_kulebyaks --kulebyaks_path mondata/kulebyaks/ --filter myservice.yaml --dump
```
--dump отключает синхронизацию с внешними системами и просто выводит результат парсинга.
Еще такой вызов можно использовать для проверки изменений. Нужно сохранить вывод до и после правок и сравнить их через
diff или [dyff](https://github.com/homeport/dyff).

Следующим метод проверки это запуск с опцией dry-run
```shell
packages/mondata_server/cmd/update_kulebyaks/update_kulebyaks --kulebyaks_path mondata/kulebyaks/ --filter myservice.yaml --dry-run --debug
```
Такой запуск покажет какие правки в solomon/juggler будут сделаны
```shell
2021-08-09 23:21:25,370 mondata.juggler_notification - juggler_notification.py:217 - sync_notifications() - DEBUG - delete notifications ids=['610c6aa7d9b8323d9e93e807', '610c6aa7d2bade86ce2307fc']
...
2021-08-09 23:29:04,690 mondata.solomon - solomon.py:331 - update_alert() - DEBUG - update alert SolomonAlert[kulebyaks-CPU_load-iva-sch1]
```

Без дополнительных опций скрипт внесет правки в solomon/juggler, и через некоторое время автоматика затрет эти правки.
Чтобы сохранить правки, нужно их закоммитить.

Если же хочется внести правки на долгое время, можно указать генератору свой тестовый namespace:
```shell
packages/mondata_server/cmd/update_kulebyaks/update_kulebyaks --kulebyaks_path mondata/kulebyaks/ --solomon-project-id grad_testing --juggler-namespace mondata
```

Результат парсинга кулебяки можно увидеть в [аркадии](https://a.yandex-team.ru/robots/trunk/nocdev/mondata_configs/kulebyaks).
А последний статус – в [juggler](https://juggler.yandex-team.ru/raw_events/?query=tag%3Dupdate_kulebyaks.py&limit=20)

Рядом с update_kulebyaks.py лежат скрипты для зачистки неудачных данных:
delete_juggler_notifications.py – удаление подписок,
delete_solomon.py – удаление алертов.

### Архитектурная секция
Точкой входа является скрипт update_kulebyaks.py. В нём sync() сначала вызывает get_kulebyaks(), который парсит кулебяки
и возвращает данные в виде стандартных структур питона. Это делается для возможности сериализовать данные в JSON для VCS или для вывода в файл.
Дальше этот вывод парсится в sync_kulebyaks и производится синхронизация с solomon/juggler.

Парсинг каждой кулебяки происходит в parse_koulibiac(). Там реализовано подключение шаблонов, подмешивание хостов и тегов.
Шаблоны реализованы достаточно просто: исполняемые шаблоны импортируются и выполняются, а ямловые просто вычитываются.
Есть разделение шаблонов на per-тип-проверочные и глобальные. Фича глобальных в том, что они могут
возвращать и juggler и solomon алерты и даже per-тип-проверочные шаблоны, которые развернутся как обычно. Рекурсивное подключение не поддерживается.

Синхронизация разделена на две части:
1. Обнаружение кулебяк, их выполнение и сохранение результата в [аркадию](https://a.yandex-team.ru/robots/trunk/nocdev/mondata_configs/kulebyaks).
2. Выгрузка из аркадии и синхронизация с juggler/solomon.

Такое разделение сделано для упрощения обработки ошибок. Так как у нас всегда есть распаршенные кулебяки в аркадии, мы всегда
можем синхронизировать их с solomon/juggler. Дополнительный бонус – история изменений.

##### Статус синхронизации кулебяк
[Дашборд](https://juggler.yandex-team.ru/dashboards/kulebyaks) \
Логи лежат на portugal в /var/log/mondata/.
/var/log/mondata/update_kulebyaks_to.py.log - синк в аркадию.\
/var/log/mondata/update_kulebyaks_from.py.log - синк из аркадии в solomon, juggler, etc.\
/var/log/mondata/s3_sync.py.log - генерация конфигов juggler из аркадии в s3.

### FAQ
#### Почему я должен зафиксировать проверку в мондате, а не сделать всё руками?
Мы считаем что незафиксированная в коде проверка это плохая проверка. Такую проверку легко потерять и узнать об этом
только перед LSR. Про ручную проверку нет никакой истории и сложно понять кто и её сделал и зачем.

#### Где посмотреть созданные проверки?
Сырые события по имени кулебяки можно посмотреть [тут](https://juggler.yandex-team.ru/raw_events/?query=tag%3Dslbcloghandler.yaml),
но нет гарантий, что проверочный скрипт не посылает в жагглер событий без этих тегов.

#### Почему я жагглеру проверку хочу.
Мы потихоньку съезжаем с заббикса и в светлом будущем все проверочные скрипты будут выполнятся жагглером.
Чтобы переехать, в первую очередь нужно добавить хост или группу хостов в предикат **[kulebyaks transit]**. После этой правки, кулебяка начнет
генерировать конфиги для запуска скриптов через juggler-client в [аркадию](https://a.yandex-team.ru/robots/trunk/nocdev/mondata_configs/kulebyaks/scripts).
Дальше обновляем mondata до 1.2-202108270904 или старше. Это обновление притянет крон-задачу для
скачивания конфига juggler-client в /etc/monrun/kulebyaks_all/MANIFEST.json.
Кроме того нужно убедиться что удален файл /etc/monrun/MANIFEST.json. Для FreeBSD смотрим эту [инструкцию](https://st.yandex-team.ru/NOCDEV-7271#6282cac6f364cf2c0522c91d).
Дальше читаем [доку](https://a.yandex-team.ru/arcadia/noc/mondata/kulebyaks#script).

### Перенос проверок из zabbix в juggler.
- Убедиться что установлен juggler-client
- Добавить хосты в предикат [kulebyaks transit]
- Склонировать https://a.yandex-team.ru/robots/trunk/nocdev/mondata_configs/ и там, с помощью
  ```cat * | jq '.items[] | select(.host == "sas1-grad1.yndx.net")'``` найти все проверки и перенести их в juggler.

Пример вывода jq.
```(json)
{
  "delay": 300,
  "host": "sas1-grad1.yndx.net",
  "key": "proc.num[,,,yandex-hbf-agent]",
  "name": "proc cmdline=yandex-hbf-agent count",
  "output": "int",
  "tags": ["discovery_hbf_agent.py", "process_status",
           "service_yandex-hbf-agent", "yandex-hbf-agent"],
  "type": "agent"
}
```
- В discovery (выше пример hbf_agent.py) добавить вызов set_global_rt_exception("{my_rt_filter}"),
  чтобы исключить из discovery свои хосты.
- Алерты соломона из solomon/ не сикаются в svn, поэтому найти их можно только в вебе соломона.
Например, вот так https://solomon.yandex-team.ru/admin/projects/noc/alerts?text=sas1-grad1.
### Почему не стоит исключать "{в оффлайне}" из фильтра
- Это не очень быстро работает.
- Не будут работать зависимости от unreachable. Придется убирать хост вообще из всех проверок.
- Теряется история алерта в соломоне.
### Как найти результаты своих проверок?
[Juggler агрегаты](https://juggler.yandex-team.ru/aggregate_checks/?query=tag%3Dnocdev-kulebyaks_grad.yaml) по имени кулебяки.
[Juggler сырое событие](https://juggler.yandex-team.ru/raw_events/?query=tag%3Dnocdev-kulebyaks_grad.yaml) по имени кулебяки.
[Solomon alert](https://solomon.yandex-team.ru/admin/projects/noc/alerts?text=kulebyaks_grad.yaml_+) по имени кулебяки.
### Нет данных от проверок через juggler-client
1. Проверяем что проверка есть в https://a.yandex-team.ru/robots/trunk/nocdev/mondata_configs/kulebyaks/scripts/$FQDN.json
2. На сервере запускаем /var/spool/mondata/utils/update_juggler_conf.py --debug. Возможно нет дырки до s3
3. Проверяем что в /etc/monrun/kulebyaks_all/MANIFEST.json есть нужная проверка
4. Попробовать руками запустить скрипт с аргументами из /etc/monrun/kulebyaks_all/MANIFEST.json.
5. Посмотреть лог /var/log/juggler-client/juggler-client.log
6. Можно глянуть в текущие сообщения в ожидании jclient-api print-events

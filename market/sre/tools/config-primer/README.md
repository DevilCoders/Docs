# CONFIG-PRIMER

### Установка

```
$ brew tap cs-admin/tap https://github.yandex-team.ru/cs-admin/homebrew-tap.git
$ brew install yandex-market-config-primer
```

### Краткий принцип работы
Утилита принимает на вход YAML-файлы определенного формата и наполняет данными словарные структуры в памяти, которые затем доступны при парсинге шаблонов (основанных на GO-Templates). Результатом парсинга шаблонов являются файлы конфигураций, сохраняемые в заданный каталог. В случае, если результирующий файл конфликтует с тем, что уже хранится в ранее созданном файле конфигурации, утилита переносит старый файл в архив. По желанию, каталог с файлами сгенерированных конфигураций может быть очищен от файлов не участвовавших в последней сессии прайминга.

### Переменные окружения
Утилита понимает несколько переменных окружения, в зависимости от которых меняет формат и детальность выдачи. К примеру, можно запускать утилиту так для TRACE-уровня отладочной выдачи в json-формате:
```
LOGXI="*=TRC" LOGXI_FORMAT=JSON,t=2006-01-02T15:04:05.000000-0700 config-primer ...
```
Кроме того, утилита понимает переменные окружения, начинающиеся с префикса `PRIMER_`. Подробнее о них сказано в параметрах командной строки.

### Параметры командной строки. В квадратных скобках указаны переменные окружения, значения которых перекрывают соответствуюбщие параметры
```
$ config-primer -h
Usage of src/cmd/config-primer/config-primer:
  -alternative-prefixes string
    	Additional prefixes for values.globals, values.options and other sections (ex. alt1,alt2 to parse and populate alt1_options, alt2_be1_defaults and so on) [Environment variable: PRIMER_ALT_PREFIXES]
  -archives string
    	Where to create backup copies of configs to be overwritten, or cleared (disabled if omitted or empty) [Environment variable: PRIMER_ARCHIVE_PATH]
  -collector-output-dir string
    	Where to dump collected instance data, [Environment variable: PRIMER_COLLECTOR_OUTPUT_DIR]
  -conductor-disabled
    	Don't use conductor [Environment variable: PRIMER_CONDUCTOR_DISABLED]
  -conductor-project string
    	Comma separated list of conductor projects [Environment variable: PRIMER_CONDUCTOR_PROJECTS] (default "cs")
  -conductor-top-groups string
    	Limit primer's regexp hostname matching to a subset of hosts [Environment variable: PRIMER_CONDUCTOR_TOP_GROUPS] (default "cs_deb-stable,cs_deb-prestable,cs_deb-testing,cs_deb-unstable")
  -config-prefix string
    	Prefix of configuration files [Environment variable: PRIMER_CONFIG_PREFIX]
  -configs string
    	Where to search for configs (values) [Environment variable: PRIMER_CONFIGS]
  -configs-ext string
    	Extension for YAML-configs (values) to parse [Environment variable: PRIMER_CONFIG_EXT] (default "yaml")
  -dc string
    	Set local DC by hand [Environment variable: PRIMER_DC]
  -debug
    	Turn on debug logging [Environment variable: DEBUG]
  -dns-requests int
    	Set maximum number of parallel DNS-requests [Environment variable: PRIMER_DNS_REQUESTS] (default 32)
  -env string
    	Set local environment [Environment variable: PRIMER_ENV]
  -exclude-dc string
    	Exclude common separated list of datacenters from results [Environment variable: PRIMER_EXCLUDE_DC]
  -fqdn string
    	Set local FQDN, [Environment variable: PRIMER_FQDN]
  -http-requests int
    	Set maximum number of parallel http-requests, [Environment variable: PRIMER_HTTP_REQUESTS] (default 16)
  -http-retries int
    	Set maximum number of retries for http-requests, [Environment variable: PRIMER_HTTP_RETRIES] (default 3)
  -http-timeout duration
    	Timeout in ms for http-requests, [Environment variable: PRIMER_HTTP_TIMEOUT] (default 5s)
  -log-file string
    	Logging destination: STDOUT, STDERR, real file name [Environment variable: LOG_FILE] (default "STDERR")
  -log-level string
    	Logging level: DEBUG, INFO, WARN, ERROR, DPANIC, PANIC, FATAL [Environment variable: LOG_LEVEL] (default "INFO")
  -log-style string
    	Force log style to be: console, json or auto. Default is auto. [Environment variable: LOG_STYLE] (default "auto")
  -nocache
    	Don't use conductor cache [Environment variable: PRIMER_NOCACHE]
  -results string
    	Where to place result [Environment variable: PRIMER_RESULTS]
  -results-clean
    	Remove all files with template-extension, which're not generated in a current run of primer [Environment variable: PRIMER_RESULTS_CLEAN]
  -results-ext string
    	Extension for resulting config [Environment variable: PRIMER_RESULTS_EXT] (default "conf")
  -show-stats
    	Show stats on exit (default true)
  -static-files string
    	Where to search for static files [Environment variable: PRIMER_STATIC_FILES]
  -templates string
    	Where to search for templates [Environment variable: PRIMER_TEMPLATES]
  -templates-ext string
    	Extension for templates to parse [Environment variable: PRIMER_TEMPLATES_EXT] (default "tpl")
  -threads int
    	Set maximum number of GO-routines to execute at once [Environment variable: PRIMER_THREADS] (default 12)
  -trace
    	Turn on trace logging [Environment variable: TRACE]
  -version
    	Show version and exit
  -yp-cluster string
    	YP-Cluster for requests, [Environment variable: PRIMER_YP_CLUSTER] (default "xdc")
  -yp-disabled
    	Disable YP-backend (fallback to YPSD), [Environment variable: PRIMER_YP_DISABLED]
  -yp-max-parallel-requests int
    	Set maximum number of parallel requests to YP, [Environment variable: PRIMER_YP_MAX_PARALLEL_REQUESTS] (default 16)
  -yp-max-retries int
    	Set maximum number of YP request retries, [Environment variable: PRIMER_YP_MAX_RETRIES] (default 5)
  -yp-sd-max-parallel-requests int
    	Set maximum number of parallel requests to YP Service Discovery, [Environment variable: PRIMER_YPSD_MAX_PARALLEL_REQUESTS] (default 16)
  -yp-sd-max-retries int
    	Set maximum number of YP SD request retries, [Environment variable: PRIMER_YPSD_MAX_RETRIES] (default 3)
  -yp-sd-url string
    	URL YP Service Discovery URL, [Environment variable: PRIMER_YPSD_SD_URL] (default "sd.yandex.net:8081")
  -yp-token string
    	Token for YP, [Environment variable: PRIMER_YP_TOKEN]
  -yp-token-env string
    	Environment variable with token for YP, [Environment variable: PRIMER_YP_TOKEN_ENV] (default "YP_TOKEN")
  -yp-token-file string
    	File with token for YP, [Environment variable: PRIMER_YP_TOKEN_FILE] (default "/Users/maxk/.yp/token")
```

### Формат YAML-файла для деплоя
YAML-файлы в комбинации с config-primer'ом и config-linker'ом можно использовать для подкладывания кастомных (сделанных руками) конфигов. Пример такого файла:
```
params:
  default:
    static_file: default
  "%market_slb_search":
    generate: no
  "%market_slb_search@man":
    generate: yes
```
В данном случае primer попытается найти в папке, заданной параметром `-static-files`, файл с именем YAML-файла, но с расширением `-results-ext`. Вместо default можно указать имя файла (с расширением).

### Формат YAML-файла для шаблонизации
YAML-файл со значениями для конфигураций состоит из 4-х секций верхнего уровня. Каждая из секций не обязательная к использованию.
```
# Параметры обработки
params:
  default:
    templates:
      - user_mslb_http.tpl
  "%market_slb_search@man":
    generate: no

# Значения, доступные в шаблоне
values:
  default:
    defaults:
      check: "check observe layer7"
      maxconn: 10
    globals:
      display_port: 17053
      http_reuse:   aggressive
      listen_port:  17253
      min_nbsrv:    24
      ping_expect:  "status 200"
      service_name: market-preport.yandex.net
      service_port: 17050
    options:
      allbackups:
  testing:
    globals:
      service_name: mslb.tst.vs.market.yandex.net
      min_nbsrv:    1

# Именованные списки серверов, доступные в шаблоне
servers:
  default:
    main:
      - name: "%market_search-parallel@local"
        weight: 55
      - name: "/msh-par0[1,9][a-z].market.yandex.net/"
        weight: 45
      - name: "/msh-par17[a-z].market.yandex.net/"
        weight: 45
      - name: "/msh-par25[a-z].market.yandex.net/"
        weight: 45
      - name: "/msh-par33[a-z].market.yandex.net/"
        weight: 45
      - name: "%market_search-parallel"
        track: report
  testing:
    main:
      - name: "msh01ht.market.yandex.net"
        weight: 45
      - name: "%market_search-testing-trusty"
        track: report
      - name: -msh09ht.market.yandex.net
      - name: -msh10ht.market.yandex.net

# Именованные упорядоченные списки доступные в шаблоне
lists:
  default:
    handles:
      - name: "/ping"
        access_log: off
      - name: "/"
```

Каждая из секций внутри делится по окружениям хоста, на котором происходит обработка (environment, регулярное выражение по FQDN, кондукторная группа, или просто FQDN). Параметры всегда изначально берутся из окружения `default`, а в последующем дополняются и изменяются в зависимости от окружения. Рассмотрим пример работы с окружениями для секции `params`: 
```
params:
  default:
    output: 101-service-production.conf
    templates:
      - user_mslb_http.tpl
  testing:
    output: 101-service-testing.conf
  "%market_slb_search@man":
    generate: no
  "/mslb[0-9][0-9][a-z]t?.supermarket.yandex.net/":
    generate: no
```
Читается пример так: 
* использовать шаблон `user_mslb_http.tpl`
* имя выходного файла будет `101-service-production.conf`, но если хост в тестинге (т.е. содержимое `/etc/yandex/environment.type`, или параметр командной строки `-env` равны testing), то имя выходного файла - `101-service-testing.conf`
* если FQDN-хоста (который может быть задан и параметром командной строки `-fqdn`) подпадает под регулярное выражение `mslb[0-9][0-9][a-z]t?.supermarket.yandex.net`, либо хост входит в кондукторную группу `market_slb_search` (определяется по FQDN), располагаясь при этом в Финлнядии (можно принудительно указать параметром командной строки `-dc`), то никакой конфиг сгенерирован не будет.

#### Секция `params`:
Секция может содержать следующие параметры:
* `generate` – нужно ли обрабатывать данный YAML-файл. Если значение false, или no - конфигурационный файл опускается из обработки.
* `resolve` – нужно ли резолвить хосты в данном YAML-файле. По умолчанию – нет, не нужно. Если значение yes, или true – все хосты из секции servers будут отрезолвлены, а адреса (по одному каждого типа) попадут в аттрибуты `addr_ip4`/`addr_ip6`. Кроме того, в аттрибут `addr` попадет ip6-адрес хоста, если он есть, либо ip4, если ip6-адреса у хоста нет. Аналогичный резолвинг будет выполнен и для values.globals.service_name, если он указан, но не указан при этом service.globals.addr_ip6 (в этом случае, будет еще автоматически создано поле addr_fdee).
* `fail_on_resolve` – Нужно ли падать при ошибках резолвинга хостов. По умолчанию – да, нужно.
* `output` – имя файла с результирующим конфигом, задается относительно "каталога назначения", который может быть указан параметром командной строки (по-умолчанию – текущий каталог).
* `templates` – упорядоченный список имен файлов, заданных относительно каталога, переданного в параметре `-templates`. Все файлы, указанные в данном списке, будут последовательно загружены в память и объединены в один документ, переданный парсеру. Кроме перечисленных файлов, предварительно в память будут загружены все файлы из каталога `-templates`, имя которых соответствует маске `lib_*.tpl`. В списке можно предварить имя шаблона знаком `-`, тогда этот файл не будет включен в результирующий список (полезно, если нужно отключить какой-либо `lib_*.tpl`).

#### Секция `values`:
В данной секции хранятся именованные словари, доступные для использования в шаблонах.

#### Секция `sections`:
В данной секции хранятся именованные словари, доступные для использования в шаблонах. Но, в отличие от `values`, здесь есть дополнительный уровень пложенности.

#### Секция `lists`:
В данной секции хранятся именованные списки словарей, доступных для использования в шаблонах.

#### Секция `servers`:
Эта секция хранит именованные списки серверов. Каждый элемент списка - словарь с обязательным ключом `name`. Формат ключа следующий:
* Если имя ключа начинается с символа `%` – это кондукторная группа (ex.: `%market_search-parallel`). При этом, имя может иметь необязательный спецификатор датацентра, заданный после символа `@` (ex.: `%market_search-parallel@sas`). Кроме `sas`, `ugr` и т.п. можно использовать спецификатор `local`, который будет соответствовать хостам, находящимся в одном датацентре, с хостом, на котором запущена утилита. Этот локальный ДЦ можно переопределить через параметр командной строки `-dc`.
* Если имя ключа начинается и заканчивается символом `/` это регулярное выражение. При этом для поиска хостов, соответствующих регулярному выражению, используется ограниченное множество хостов, входящих в кондукторные группы, указанные в параметре командной строки `-conductor-top-groups string`.
* Если имя ключа начинается с `MACRO@` – это имя HBF-макроса. На выходе имеем список сетей, в этот макрос входящих. Если поставить параметр `unique: true`, то сети будут уникальны. У каждой сети есть чаще всего пустой параметр `project_id`. Отсортирован результат по младшему адресу сети по возрастанию, а потом по длине маски по убыванию. Если в макросе попались fqdn'ы - они будут выданы как обычные сервера, т.е. вероятнее всего записи `MACRO@_C_MARKET_DEVEL_ADMIN_` и `%market_devel-admin` будут эквивалентны.
* Если имя ключа начинается с `N@` – это имя инстанса в Nanny. Для этих инстансов можно использовать дополнительный параметр в элементах секции server – port_offset. Это числовое смещение от базового порта. Кроме того, есть ещё параметр agent_port_offset, при наличии которого для сервиса формируется agent_port как port + agent_port_offset. А ещё сервера в няня-сервисах можно фильтровать по шардам ($номер_шарда) и репликам (#номер_релики). К примеру, `N@prod_report_market_sas$1#2@local` вернет вторую реплику первого шарда при условии, что няня-сервис в том же ДЦ, что и праймер.
* Если имя ключа начинается с `YP@` – это имя endpoint set'а в YP. Эти инстансы автоматически резолвятся в списки `fqdn:порт`. Для них желательно указывать спецификатор ДЦ, т.к. иначе селекция будет сделана по всем YP-кластерам.   
* Если имя ключа не начинает с символов `%`, `/`, или `-` – это просто FQDN, он будет передан как есть.
* Если имя хоста начинается с символа `-` – это исключающий элемент списка. Он может быть как кондукторной группой со спецификатором, или без, так и регулярным выражением, или просто FQDN.

Для каждого хоста из этой секции генерируется дополнительный аттрибут `hostname`, в котором сохраняется краткое имя хоста (без доменной части).
Кроме того, может генерироваться адресная часть, если у хоста указано `resolve: true`, либо эта опция взведена в секции `params`.

Для управления сортировкой конечного списка используются два спец. атрибута:
* `order` - позиция группы серверов в конечном списке. Все группы без этого атрибута по-умолчанию имеют `order = 10000`.
* `sort_order` - как сортировать хосты с одинаковым значением `order`. Есть три варианта: `ascending` - по возрастанию (этот вариант используется по-умолчанию), `descending` - по убыванию и `shuffled` - в случайном порядке. `Shuffled` гарантирует персистентный порядок при неизменном FQDN-хоста.

Конечный именованный список хостов, доступный для обработки в шаблонах формируется следующим образом: обработчик идет последовательно по всем элементам списка и, "распаковывая" шаблоны имен, формирует результирующий "словарь-словарей" (`fqdn сервера -> пары ключ-значение`). При этом, если пара `ключ-значение` была задана в предшествующем элементе списка, то она не перезаписывается последующими. Исключающие элементы списка, убирают соответствующие им хосты из результата. При этом, последующие элементы могут снова их добавить, к примеру для того, чтобы переопределить параметры. Пример:
```
servers:
  testing:
    main:
      - name: "msh01ht.market.yandex.net"
        weight: 45
      - name: "%market_search-testing-trusty"
        track: report
        weight: 50
      - name: -msh09ht.market.yandex.net
      - name: -/msh1[0-9]ht.market.yandex.net/
      # Ну и для понимания работы механизма переопределения параметров:
      - name: -/msh0[23]ht.market.yandex.net/
      - name: "%market_search-testing-trusty"
```
После обработки, в шаблон будет передано следующее дерево:
```
servers:
  testing:
    main:
      - name: "msh01ht.market.yandex.net"
        weight: 45
        track: report
      - name: "msh02ht.market.yandex.net"
      - name: "msh03ht.market.yandex.net"
      - name: "msh04ht.market.yandex.net"
        weight: 50
        track: report
      - name: "msh05ht.market.yandex.net"
        weight: 50
        track: report
      - name: "msh06ht.market.yandex.net"
        weight: 50
        track: report
      - name: "msh07ht.market.yandex.net"
        weight: 50
        track: report
      - name: "msh08ht.market.yandex.net"
        weight: 50
        track: report
```
### Магия
В секции `servers` можно указывать параметры с offset'ами: `agent_port_offset`, `check_port_offset`, `track_port_offset` и `port_offset`.
Обычно они нужны, чтобы добавлять нужное смещение к базовому порту из Няни (iport) и сохранять значение в соответствующих `agent_port`, `check_port`, `track_port` и `port` параметрах.
Но, если вышеуказанные `_port`-параметры зачем-то указаны явно, `_offset`-параметры будут применены к ним. Кроме одного исключения: заданный явно `port`-параметр остается неизменным.

Я уже упоминал автоматический resolv'ing service_name. Уточню, что он не случится, если в секциях `globals` и `fe_globals` принудительно не указан `addr_ip6`.

Также можно принудительно запретить, или разрешить резолвинг хостов в секциях серверов, указав там `resolve: no`, например. Кроме того, `resolve: no`, или `resolve: yes` может повлиять на резолвинг, если находится в секциях `^be.*_globals`, `globals`, или `<имя секции серверов>_globals`.

Помимо возможности автоматического резолвинга `service_name` и хостов из серверной секции, `config_primer` умеет еще кое что.
1. Утилита знает, что в секции `values` бывают разделы `defaults`, `globals`, `headers`, `options`, `no_options`. Так вот, утилита ищет такие разделы и для каждого из них ищет разделы `[bf]e_имя`, например, для `global`, она ищет `fe_globals` и `be_globals` (backend и frontend). Если таких разделов нет – утилита их создает. В любом случае, в эти разделы будут занесены все пары ключ/значение из родительского раздела, кроме тех ключей, что были определены в дочерней секции.
2. Аналогично, для `be_`-разделов ищутся дочерние, соответствующие маске `^be[^_]+_(globals|headers|...)$`. В эти дочерние вносится недостающая информация из родительских. Таким образом, в момент обработки шаблона, коду в шаблонизаторе достаточно обратиться, скажем, к секции `be1_globals`, чтобы получить значения всех пар ключ/значение из секций `be1_globals`, `be_globals` и `globals`. При этом, сами дочернии секции можно даже не объявлять. Утилита гарантирует автоматическое создание секций `be1..be5`.
3. И, наконец, если вы указали непустое значение для параметра -alt-prefixes, то помимо секций, указанных в предыдущих параметрах, появятся еще и альтернативные
Пример с пустым -alt-prefixes:
```
...
values:
  default:
    be_globals:
      http_reuse:     aggressive
      ping_expect:    "string 0;OK"
      timeout_server: 1s
      timeout_queue:  100
    be1_globals:
      balance:        leastconn
      timeout_connect: 25
    be3_globals:
      balance:        leastconn
      min_nbsrv:      24
      min_nbsrv_tcp:  16
    fe_globals:
      timeout_client: 5s
    globals:
      addr_ip6:       ::1
      listen_port:    17253
      display_port:   17053
      service_name:   market-preport.yandex.net
      service_port:   17050
...
```
Превратится в:
```
values:
  default:
    be_globals:
      display_port:   17053
      http_reuse:     aggressive
      ping_expect:    "string 0;OK"
      service_name:   market-preport.yandex.net
      service_port:   17050
      timeout_queue:  100
      timeout_server: 1s
    be1_globals:
      balance:        leastconn
      display_port:   17053
      http_reuse:     aggressive
      ping_expect:    "string 0;OK"
      service_name:   market-preport.yandex.net
      service_port:   17050
      timeout_connect: 25
      timeout_queue:  100
      timeout_server: 1s
    be2_globals:
      display_port:   17053
      http_reuse:     aggressive
      ping_expect:    "string 0;OK"
      service_name:   market-preport.yandex.net
      service_port:   17050
      timeout_queue:  100
      timeout_server: 1s
    be3_globals:
      balance:        leastconn
      display_port:   17053
      http_reuse:     aggressive
      min_nbsrv:      24
      min_nbsrv_tcp:  16
      ping_expect:    "string 0;OK"
      service_name:   market-preport.yandex.net
      service_port:   17050
      timeout_queue:  100
      timeout_server: 1s
    fe_globals:
      addr_ip6:       ::1
      display_port:   17053
      listen_port:    17253
      service_name:   market-preport.yandex.net
      service_port:   17050
      timeout_client: 5s
    globals:
      display_port:   17053
      service_name:   market-preport.yandex.net
      service_port:   17050
...

```

Пример с -alt-prefixes "grpc,http":
```
...
values:
  default:
    defaults:
      param: 1
    be_defaults:
      param: 2
    grpc_defaults:
      param: 3
    grpc_be2_defaults:
      param: 4
...
```
Превратится в:
```
...
values:
  default:
    defaults:
      param: 1
    fe_defaults:
      param: 1
    be_defaults:
      param: 2
...
    grpc_defaults:
      param: 3
    grpc_fe_defaults:
      param: 3
    grpc_be_defaults:
      param: 3
    grpc_be1_defaults:
      param: 3
    grpc_be2_defaults:
      param: 4
...
    http_defaults:
      param: 1
    http_fe_defaults:
      param: 1
    http_be_defaults:
      param: 2
    http_be1_defaults:
      param: 2
    http_be2_defaults:
      param: 2
...
```

### Пример запуска утилиты:
```
#!/bin/bash
export LOGXI=*=DBG
v_path="${HOME}/packages/config-primer/test"
config-primer \
  -configs   "${v_path}/values-enabled" \
  -results   "${v_path}/configs-generated" \
  -templates "${v_path}/templates/" \
  -archives  "${v_path}/configs-generated/archive" \
  -results-clean \
  -env       testing \
  -fqdn      mslb01ht.market.yandex.net \
  -dc        sas
```
Утилита будет считать, что запущена на хосте `mslb01ht.market.yandex.net`, имеющем environment `testing` и расположенном в ДЦ Сасово. Она возьмет все `*.yaml` файлы из каталога `-configs`, поставит им в соответствие шаблоны `*.tpl` из каталога `-templates`, запустит обработку и полученные результаты сохранит в каталог `-results`. Если после обработки в каталоге `-results` будет уже существующий файл то, если содержимое идентично, файл перезаписан не будет, а если содержимое различается – старый файл будет перенесен в каталог `-archives` с добавлением к его имени окончания `.ГГГГММДДЧЧММСС` от даты его же модификации. Т.к. задан параметр `results-clean`, после обработки всех YAML-файлов, каталог `-results` будет очищен от всех файлов `*.conf`, которые появились не в результате текущего сеанса работы, учитывая неизменившиеся файлы.

### Формат файлов-шаблонов
В шаблонах используется стандартный синтаксис Go-templates. Синтаксис расширен для более удобной работы с кондуктором и дополнен helper'ами из проекта [Hugo templates](https://gohugo.io/templates/functions). Список дополнительных функций:
* `add` – Сложение двух целых чисел: `{{add 1 2}} → 3`
* `after` – Возвращает остаток массива после N-ного элемента: `{{ range after 10 .Data.Pages }}{{ .Render "title" }}{{ end }}`
* `base64decode` – Декодирует строку из base64: `{{ "SGVsbG8gd29ybGQ=" | base64Decode }} → "Hello world"`
* `base64encode` – Кодирует строку в base64: `{{ "Hello world" | base64Encode }} → "SGVsbG8gd29ybGQ="`
* `chomp` – Удаляет все символы переноса строки в конце переданного текста: `{{chomp "Blockhead\n"}} → "Blockhead"`
* `complement` – Возвращает элементы коллекции, отсутствующие в других коллекциях: `{{ $other := $pages | complement $news $blog }}`
* `cond` – Возвращает первый, или второй аргумент в зависимости от истинности третьего аргумента: `{{ cond (eq (len $geese) 1) "goose" "geese" }}`
* `contains` – Содержится ли подстрока в строке: `{{ cond (contains "Test" "est") "yes" "no" }}`
* `containsAny` – Проверят, содержит ли строка хотя бы один unicode point из параметра
* `countrunes` – Возвращает количество символов в строке: `{{ "Hello, 世界" | countrunes }} → 8`
* `countwords` – Возвращает количество слов в строке: `{{ "Hugo is a static site generator." | countwords }} → 6`
* `default` – Передача параметра по умолчанию, ex.: `{{ .timeout_connect | default 50 }}`.
* `dateFormat` – Преобразует текстовое представление datetime в иную форму, либо в Go-тип time.Time: `{{ dateFormat "Monday, Jan 2, 2006" "2015-01-21" }} → “Wednesday, Jan 21, 2015”`
* `delimit` – Объединяет элементы переданной коллекции в строку с помощью указанного разделителя. Принимает третий необязательный параметр "разделитель для крайнего объекта": `Tags: {{ delimit .Params.tags ", " }}`, или `Tags: {{ delimit .Params.tags ", " " and " }}`
* `dict` – Формирование словаря для передачи его как параметра в шаблоны: `{{- template "server" (dict "server" . "defaults" $defaults "globals" $globals)}}`.
* `div` – Деление двух целых чисел: `{{div 6 3}} → 2`
* `echoParam` – Выводит значение параметра, если он установлен: `{{ echoParam .Params "project_url" }}`
* `eq` – Возвращает true, если параметры равны: `{{ if eq .Section "blog" }}current{{ end }}`
* `fileExists` - Возвращает true, если указанный файл существует: `{{ cond (fileExists "/etc/passwd") "true" "false" -}}`
* `fileStat` – Возвращает информацию о файле по заданному пути: `{{ $stat := fileStat "README.txt" }}{{ $stat.Name }}{{ $stat.Size }}`
* `findRe` – Возвращает список строк подходящих под заданное регулярное выражение. По-умолчанию будут возвращены все совпадения. Количество возвращаемых совпадений может быть ограничено третьим параметром: `{{ findRE "<h2.*?>(.|\n)*?</h2>" .Content 1 }}`
* `first` – Возвращает первые N элементов массива: `{{ range first 10 .Data.Pages }}{{ .Render "summary" }}{{ end }}`
* `jsonify` – Кодирует переданный объект как json: `{{ dict "title" .Title "content" .Plain | jsonify }}`
* `ge` – `>=`
* `getenv` – Возвращает значение переменной окружения: `{{ getenv "HOME" }}`
* `gid` – Возвращает gid основной группы пользователя: `{{ gid "root" }} → “0”`
* `gt` – `>`
* `groupHosts` – Список хостов группы из кондуктора.
* `hasPrefix` – Начинается ли строка с искомого префикса: `{{ hasPrefix "Hugo" "Hu" }} → true`
* `hasSuffix` – Заканчивается ли строка на указанный суффикс: `{{ hasSuffix "Hugo" "go" }} → true`
* `home` – Возвращает путь к домашней папке указанного пользователя: `{{ home "root" }} -> “/root”`, или текущего пользователя `{{ home }} -> “/home/vasya_p”`
* `hostExtension` – Значение "расширения" для хоста из кондуктора.
* `hostGroups` – Группы, в которые входит хост.
* `hostTags` – Теги, которые навешаны на хост.
* `in` – Проверяет, входит ли переданный 2-ой параметр в объект, заданный 1-ым: `{{ if in .Params.tags "Git" }}Follow me on GitHub!{{ end }}`, или `{{ if in "this string contains a substring" "substring" }}Substring found!{{ end }}`
* `index` – Возвращает объект масссива, словаря или слайса по переданному ключу: `{{ index .Params "font" | default "Roboto" }}`
* `int` – Создает целое число: `{{ int "123" }} → 123`
* `intersect` – Возвращает пересечение двух переданных множеств: `{{ $has_common_tags := intersect $tags .Params.tags | len | lt 0 }}`
* `isSet`, или `isset` – Используется в условиях для проверки "есть ли значение в словаре": `{{- if isSet . "addr_ip4" }}bind ipv4@{{ .addr_ip4 }}:{{ .listen_port | default .service_port }}{{- end }}`
* `isTrue`, или `istrue` – Возвращает истину, если переданный параметр равен без учета регистра "1", "yes", "true", или "да": `{{ cond (isTrue ssl) "with SSL" "without SSL" }}`
* `last` – Возвращает последние N элементов массива: `{{ range last 10 .Data.Pages }}{{ .Render "summary" }}{{ end }}`
* `le` – `<=`
* `lower` – Преобразует строку в нижний регистр: `{{lower "BatMan"}} → “batman”`
* `lt` – `<`
* `md5` – MD5-хеш от параметра в виде строки: `{{ md5 "Hello world, gophers!" }} → “b3029f756f98f79e7f1b7f1d1f0dd53b”`
* `mod` – Остаток от деления двух целых чисел: `{{mod 15 3}} → 0`
* `modBool` – true, если остаток от деления двух целых чисел равен 0: `{{modBool 15 3}} → true`
* `mul` – Перемножает два целых числа: `{{mul 2 3}} → 6`
* `ne` – `!=`
* `now` – Текущее время: `{{ now.Format "2006-01-02"}} -> "2018-11-28"`
* `numfmt` – Форматирует число: `{{ lang.NumFmt 1 -12345.6789 "- . ," }} → -12,346.7`
* `projectGroups` – Все группы указанного проекта.
* `readDir` – Получает список файлов в указанном каталоге: `{{ range (readDir ".") }}{{ .Name }}{{ end }} → "README.txt"`
* `readFile` – Получает тело указанного файла: `{{readFile "README.txt"}} → "Hello, World!"`
* `repeat` – Возвращает несколько копий заданной строки: `{{ strings.Repeat "yo" 3 }} → "yoyoyo"`
* `replace` – Заменяет все вхождения строки, переданной вторым параметром, строкой, переданной третьим параметром: `{{ replace "Batman and Robin" "Robin" "Catwoman" }} → “Batman and Catwoman”`
* `replaceRE` – Производит замену вхождений, подпавших под регулярное выражение, согласно паттерну: `{{ replaceRE "^https?://([^/]+).*" "$1" "http://gohugo.io/docs" }} → “gohugo.io”`, или `{{ "http://gohugo.io/docs" | replaceRE "^https?://([^/]+).*" "$1" }} → “gohugo.io”`
* `returnWhenSet` – возвращает второй параметр, если в словаре существует ключ с именем первого параметра: `{{ returnWhenSet .defaults "check" }}`
* `sha`, или `sha1` – SHA1-хеш от параметра: `{{ sha1 "Hello world, gophers!" }} → "c8b5b0e33d408246e30f53e32b8f7627a7a649d4"`
* `sha256` – SHA256-хеш: `{{ sha256 "Hello world, gophers!" }} → "6ec43b78da9669f50e4e422575c54bf87536954ccd58280219c393f2ce352b46"`
* `seq` – Возвращает последовательность целых чисел, работает по аналогии с GNU seq: `3 => 1, 2, 3`, `1 2 4 => 1, 3`, `-3 => -1, -2, -3`, `1 4 => 1, 2, 3, 4`, `1 -2 => 1, 0, -1, -2`
* `shuffle` – Рандомизирует порядок элементов переданного массива, или слайса: `{{ shuffle (seq 1 5) }} → [2 5 3 1 4]`
* `slice` – Формирует массив из всех переданных аргументов для передачи в вышестоящие функции: `{{ delimit (slice "foo" "bar" "buzz") ", " }} → "foo, bar, buzz"`
* `slicestr` – Возвращает подстроку [a:b-1], второй параметр может быть опущен: `{{slicestr "BatMan" 3}} → “Man”`, или `{{slicestr "BatMan" 0 3}} → “Bat”`
* `sort` – Сортирует переданный массив, слайс, или словарь. Словарь будет возвращен отсортированным, но без ключей. У функции есть два необязательных аргумента: "по какому полю сортировать" и "как сортировать": `{{ range sort .Params.tags }}{{ . }} {{ end }}`, или `{{ range sort .Params.tags "value" "desc" }}{{ . }} {{ end }}`, или `{{ range sort .Site.Params.authors "lastName" "desc" }}{{ .lastName }} {{ end }}`
* `split` – Разбивает строку в массив по указанному символу-разделителю: `{{split "tag1,tag2,tag3" "," }} → [“tag1” “tag2” “tag3”]`
* `string` – Возвращает строку: `{{string "BatMan"}} → “BatMan”`
* `symdiff` – Возращает разницу между двумя коллекциями: `{{ slice 1 2 3 | symdiff (slice 3 4) }} → [1 2 4]`
* `sub` – Вычитание двух целых чисел: `{{sub 3 2}} → 1`
* `substr` – Возвращает подстроку [начало:начало + количество символов], количество символов может быть отрицательно, тогда отсчет идет от конца строки: `{{substr "BatMan" 0 -3}} → “Bat”`, или `{{substr "BatMan" 3 3}} → “Man”`
* `title` – Переводит В Titlecase: `{{title "BatMan"}} → “Batman”`
* `time` – Превращает строку в объект типа time, что позволяет использовать его аттрибуты: `{{ time "2016-05-28" }} → “2016-05-28T00:00:00Z”`, или `{{ (time "2016-05-28").YearDay }} → 149`, или `{{ mul 1000 (time "2016-05-28T10:30:00.00+10:00").Unix }} → 1464395400000 (Unix time in milliseconds)`
* `union` – Возаращет множество элементов принадлежащие той, или иной коллекции: `{{ union (slice 1 2 3) (slice 3 4 5) }} → [1 2 3 4 5]`
* `uniq` – Возвращает коллекцию без дублирующихся элементов: `{{ uniq (slice 1 2 3 2) }} → [1 2 3]`
* `uid` – Возвращает uid пользователя: `{{ uid "root" }} → “0”`
* `trim` – Удаляет первые и последние символы строки, если они попадают в указанное множество: `{{ trim "++Batman--" "+-" }} → “Batman”`
* `trimLeft` – Удаляет из начала строки заданный набор символов: `{{ trimLeft "a" "aabbaa" }} → "bbaa"`
* `trimPrefix` – Удаляет из начала строки заданный префикс: `{{ trimPrefix "a" "aabbaa" }} → "abbaa"`
* `trimRight` – Возвращает строку, удалив все переданные символы справа: `{{ trimRight "abba" "a" }} → "abb"`, или `{{ trimRight 1221 "12" }} → ""`
* `trimSuffix` – Возвращает строку без заданного окнчания (если найдено): `{{ trimSuffix "aa" "aabbaa" }} → "aabb"`
* `upper` – ПЕРЕВОДИТ ВСЕ СИМВОЛЫ В ВЕРХНИЙ РЕГИСТР: `{{upper "BatMan"}} → “BATMAN”`
* `where` – Возвращает только те элементы массива, которые имеют указанное значение для указанного поля: `{{ range where .Data.Pages "Section" "post" }}{{ .Content }}{{ end }}`
* `whoami` – Возвращает логин текущего пользователя: `{{ whoami }} → “vasya_p”`

#### Пример
```
{{- define "section" }}
{{- $defaults := .defaults }}
{{- $globals  := .globals  }}
{{- $options  := .options  }}
{{- /* Space collapse */ -}}
listen {{ $globals.display_name | default $globals.service_name }}:{{ $globals.display_port | default $globals.listen_port }}
  bind    ipv4@127.0.0.1:{{ $globals.listen_port | default $globals.service_port }}
  bind    ipv6@::1:{{       $globals.listen_port | default $globals.service_port }}
  mode    tcp
  balance {{ $globals.balance | default "leastconn" }}

{{- template "options" $options }}
{{- template "defaults" $defaults }}

{{- range $srv := .servers }}
{{- template "server" (dict "server" . "defaults" $defaults "globals" $globals) }}
{{- end }}

{{- end }}
{{ template "section" (dict "defaults" $defaults "globals" $values.globals_slaves "options" $values.options_slaves "servers" .servers.slaves) }}

{{ template "section" (dict "defaults" $defaults "globals" $values.globals_first  "options" $values.options_first  "servers" .servers.first) }}
  server {{ $values.globals_second.display_name | default $values.globals_second.service_name }} 127.0.0.1:{{ $values.globals_second.listen_port | default $values.globals_second.service_port }} backup

{{ template "section" (dict "defaults" $defaults "globals" $values.globals_second "options" $values.options_second "servers" .servers.second) }}
```

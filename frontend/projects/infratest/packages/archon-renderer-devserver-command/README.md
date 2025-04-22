# archon-renderer-devserver-command

Пакет содержит команды для [archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html),
которые запускают девсервер [kotik](https://doc.yandex-team.ru/si-infra/local_devserver/kotik.html) с необходимыми дополнениями.

## Девсервер с renderer

Подключены:

- kotik
- tunneler (публичная бета)
- renderer
- компоненты для проверки счётчиков и метрик

Для подключения к проекту укажите `@yandex-int/archon-renderer-devserver-command/commands/kotik` в [списке команд конфига archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html#commands).

{% cut "Пример запуска" %}

```text
$ npx archon kotik
Сертификаты найдены => пропускаем генерацию
Найдены конфиги DNS => пропускаем настройку
INFO: creating tunnel to 2a02:06b8:0c0d:5286:0000:0696:b994:5fb1:6825
INFO: Tunnel created to 2a02:06b8:0c0d:5286:0000:0696:b994:5fb1:6825
Loading renderer configuration file: /Users/slava-b/projects/customers/frontend/dev/services/health/.config/templates/renderer.json
Add renderer configuration: {"template":"../../build/renderer.js"}
Loading renderer configuration file: /Users/slava-b/projects/customers/frontend/dev/services/health/.config/templates/turbo-renderer.json
Add renderer configuration: {"template":"../../build/turbo-renderer.js"}
Loading renderer configuration file: /Users/slava-b/projects/customers/frontend/dev/services/health/.config/templates/router.json
Add renderer configuration: {"template":"../../build/router.js"}
Report-renderer запущен; pid: 12440; порты воркеров: 3334; devops-ручка на порту 62754
(node:12453) Warning: N-API is an experimental feature and could change at any time.
[2019-06-10T17:19:37.884] [INFO] worker #1 (12453) - Kotik слушает на http://localhost:3333
[2019-06-10T17:19:37.889] [INFO] worker #1 (12453) - Kotik слушает на https://local.yandex.ru:3443
```

{% endcut %}

Опции командной строки: `npx archon kotik --help`

```text
kotik options
  --kotik-local                         Запустить без поддержки ssl и dns (только localhost)  [boolean] [default: false]
  --kotik-public                        Запуск с поддержкой публичной прокси                  [boolean] [default: false]
  --kotik-cache-public-url              Кешировать url публичной прокси                        [boolean] [default: true]
  --kotik-play                          Запуск в режиме проигрывания дампов данных                             [boolean]
  --kotik-create                        Запуск в режиме создания дампов данных. Если дамп существует, то он не изменится
                                                                                                               [boolean]
  --kotik-save                          Запуск в режиме записи дампов данных. Если дамп существует, то он будет
                                        перезаписан                                                            [boolean]
  --kotik-cache-file                    Загрузить дамп данных из файла по явно переданному пути                 [string]
  --kotik-required-cache-param          Если указана, дампы будут читаться/записываться только при наличии указанного
                                        параметра в урле                                                        [string]
  --kotik-workers                       Количество воркеров Котика                                 [number] [default: 1]
  --kotik-port                          Порт для http-сервера                                                   [number]
  --kotik-ssl-port                      Порт для https-сервера                                                  [number]
  --kotik-verbose                       Включить логирование всех событий                     [boolean] [default: false]
  --kotik-log-time                      Включить логирование времени работы мидлвар и времени обработки запроса.
                                                                                              [boolean] [default: false]
  --kotik-exit-threshold                Минимально допустимое время жизни воркера после старта [number] [default: 10000]
  --kotik-allowed-sequential-deaths     Количество последовательных падений воркера, считающееся фатальным
                                                                                                   [number] [default: 1]
  --kotik-incognito                     Не отправлять статистику использования в статфейс     [boolean] [default: false]
  --kotik-data-fetch-timeout            Таймаут получения данных из источника                   [number] [default: 5000]
  --kotik-cache-root                    Директория хранения дампов данных
                                                             [string] [default: "/Users/fenice/.yandex-int/kotik/cache"]
  --kotik-template-flag                 Версточные флаги в формате JSON-объекта, например, '{"f1": true, "f2": 0, "f3":
                                        "1" }'. Требует middleware "templateFlag"               [string] [default: "{}"]
  --kotik-check-template-flag           Проверять, что в каждом источнике есть item с типом "flags"
                                                                                               [boolean] [default: true]
  --kotik-graph, -g, --graph            Пререквизит: в проекте должна использоваться утилита `apphost-service`.
                                        Позволяет указать имя файла с графом (из директории `graphs`), с которым будет
                                        выполнен запрос.
                                        Граф будет загружен в админку графов, в префиксе id графа будет использован ваш
                                        username.
                                        Стратегии загрузки графа в админку контролируются опцией kotik-graph-upload.
                                                                                                                [string]
  --kotik-graph-upload, --graph-upload  Загружать новую ревизию в админку всегда, либо только в случае если это новый
                                        граф.          [string] [choices: "always", "if-not-exists"] [default: "always"]
  --kotik-counters, --counters          Включить компоненты для работы проверок счетчиков     [boolean] [default: false]
  --kotik-metrics, --metrics            Включить компоненты для работы проверок метрик        [boolean] [default: false]

tunneler options
  --tunneler-domain  Домен для генерируемых url'ов. Несколько опций будут преобразованы в список доменов.
                                                                                          [array] [default: "yandex.ru"]

dns options
  --dns-port    Порт для dns-сервера                                                            [number] [default: 3053]
  --dns-domain  Подменяемый домен. Несколько опций будут преобразованы в список доменов
  [array] [default: ["local.yandex.ru","local.yandex.by","local.yandex.ua","local.yandex.kz","local.yandex.uz","local.ya
  ndex.com","local.yandex.com.tr","local.yandex.az","local.yandex.com.am","local.yandex.com.ge","local.yandex.co.il","lo
  cal.yandex.kg","local.yandex.lv","local.yandex.lt","local.yandex.md","local.yandex.tj","local.yandex.tm","local.yandex
                        .uz","local.yandex.ee","local.yandex.fr","local.yandex.fi","local.yandex.pl","local.yandex.eu"]]

log-cleaner options
  --log-cleaner-log-dir             Путь до директории хранения логов
                                                                    [string] [default: "/Users/fenice/.yandex-int/logs"]
  --log-cleaner-max-dir-size        Максимальный размер директории логов в байтах.
                                    При превышении старые логи будут удалятся пока общий размер директории не станет
                                    меньше указанного значения.
                                    Если равно -1, то файлы с логами не удаляются         [number] [default: 1073741824]
  --log-cleaner-max-files           Максимальное количество файлов с логами                      [number] [default: 200]
  --log-cleaner-keep-files-per-dir  Mинимальное количество файлов с логами в каждой поддиректории, которые нужно
                                    сохранить при удалении                                        [number] [default: 20]

click-daemon options
  --click-daemon-port  Порт для http-сервера click-daemon                                                       [number]

calc-metrics-daemon options
  --calc-metrics-daemon-port     Порт для http-сервера calc-metrics-daemon                                      [number]
  --calc-metrics-daemon-version  Версия CALC_METRICS_DAEMON_EXECUTABLE (атрибут Sandbox-ресурса resource_version; по
                                 умолчанию последний build_type=release ресурс)                                 [string]

metrics-fetcher options
  --metrics-fetcher-port                    Порт для http-сервера metrics-fetcher                               [number]
  --metrics-fetcher-checked-metrics-enable  Включить запись данных о выполненных в тестах проверках метрик.
                                                                                              [boolean] [default: false]
  --metrics-fetcher-checked-metrics-path    Путь к директории, в которой необходимо создать отчет о выполненных
                                            проверках метрик.                                                   [string]
  --metrics-fetcher-prepare-logs            Включить создание архива с запросом в демон метрик и логами демона метрик.
                                                                                              [boolean] [default: false]
  --metrics-fetcher-prepare-logs-all        Включить создание файлов с запросами в демон метрик в независимости от того,
                                            совпали они с ожидаемыми или нет. По умолчанию (false) логи пишутся только
                                            при несовпадении посчитанных метрик с ожидаемыми. [boolean] [default: false]
  --metrics-fetcher-prepare-logs-raw        Включить создание файла с запросом в демон метрик с незашифрованными логами.
                                                                                              [boolean] [default: false]

renderer options
  --renderer-port                       Порт для мастер-процесса                                                [number]
  --renderer-devops-port                Порт для devops-ручки                                                   [number]
  --renderer-workers                    Количество воркеров                                        [number] [default: 1]
  --renderer-inspector                  Запуск с поддержкой v8 inspector                      [boolean] [default: false]
  --renderer-custom-env                 Дополнительные переменные окружения в формате `VAR=1,ANOTHER_VAR=3`     [string]
  --renderer-coverage-profile           Включить сбор coverage                                [boolean] [default: false]
  --renderer-coverage-profile-dir       Путь до логов coverage                                                  [string]
  --renderer-routes-config-path         Путь до routes.json
  [string] [default: "/Users/fenice/Work/FEI-24215/frontend/projects/infratest/packages/archon-renderer-devserver-comman
                                                                              d/test/fixtures/test-project/routes.json"]
  --renderer-start-with-no-templates    Запускает renderer c опцией --start-with-no-templates, позволяет грузить шаблоны
                                        динамичеси через http api по необходимости                             [boolean]
  --renderer-start-mode                 Режим запуска renderer'a
                                   [string] [choices: "production", "development", "development-with-preload-templates"]
  --renderer-exit-threshold             Минимально допустимое время жизни воркера после старта [number] [default: 10000]
  --renderer-allowed-sequential-deaths  Количество последовательных падений воркера, считающееся фатальным
                                                                                                   [number] [default: 1]
  --renderer-apphost                    Запуск с поддержкой apphost                            [boolean] [default: true]
  --renderer-geobase                    Запуск с поддержкой геобазы                           [boolean] [default: false]
```

## Девсервер без renderer

Подключены:

- kotik
- tunneler (публичная бета)

Для подключения к проекту укажите `@yandex-int/archon-renderer-devserver-command/commands/just-kotik` в [списке команд конфига archon](https://doc.yandex-team.ru/si-infra/local_devserver/archon/archon.html#commands).

Опции командной строки: `npx archon kotik --help`

```text
kotik options
  --kotik-local, -l, --local                                    Запустить без поддержки ssl и dns (только localhost)
                                                                                              [boolean] [default: false]
  --kotik-public, --public                                      Запуск с поддержкой публичной прокси
                                                                                              [boolean] [default: false]
  --kotik-cache-public-url, --cache-public-url                  Кешировать url публичной прокси[boolean] [default: true]
  --kotik-play, --play                                          Запуск в режиме проигрывания дампов данных     [boolean]
  --kotik-create, --create                                      Запуск в режиме создания дампов данных. Если дамп
                                                                существует, то он не изменится                 [boolean]
  --kotik-save, --save                                          Запуск в режиме записи дампов данных. Если дамп
                                                                существует, то он будет перезаписан            [boolean]
  --kotik-cache-file, --cache-file                              Загрузить дамп данных из файла по явно переданному пути
                                                                                                                [string]
  --kotik-required-cache-param, --required-cache-param          Если указана, дампы будут читаться/записываться только
                                                                при наличии указанного параметра в урле         [string]
  --kotik-workers, -w, --workers                                Количество воркеров Котика         [number] [default: 1]
  --kotik-port, -p, --port                                      Порт для http-сервера                           [number]
  --kotik-ssl-port, --ssl-port                                  Порт для https-сервера                          [number]
  --kotik-verbose, -v, --verbose                                Включить логирование всех событий
                                                                                              [boolean] [default: false]
  --kotik-log-time, --log-time                                  Включить логирование времени работы мидлвар и времени
                                                                обработки запроса.            [boolean] [default: false]
  --kotik-exit-threshold, --exit-threshold                      Минимально допустимое время жизни воркера после старта
                                                                                               [number] [default: 10000]
  --kotik-allowed-sequential-deaths,                            Количество последовательных падений воркера, считающееся
  --allowed-sequential-deaths                                   фатальным                          [number] [default: 1]
  --kotik-incognito, --incognito                                Не отправлять статистику использования в статфейс
                                                                                              [boolean] [default: false]
  --kotik-data-fetch-timeout, --data-fetch-timeout              Таймаут получения данных из источника
                                                                                                [number] [default: 5000]
  --kotik-cache-root, --cache-root                              Директория хранения дампов данных
                                                             [string] [default: "/Users/fenice/.yandex-int/kotik/cache"]
  --kotik-template-flag, --template-flag                        Версточные флаги в формате JSON-объекта, например,
                                                                '{"f1": true, "f2": 0, "f3": "1" }'. Требует middleware
                                                                "templateFlag"                  [string] [default: "{}"]
  --kotik-check-template-flag, --check-template-flag            Проверять, что в каждом источнике есть item с типом
                                                                "flags"                        [boolean] [default: true]

tunneler options
  --tunneler-domain  Домен для генерируемых url'ов. Несколько опций будут преобразованы в список доменов.
                                                                                          [array] [default: "yandex.ru"]

dns options
  --dns-port    Порт для dns-сервера                                                            [number] [default: 3053]
  --dns-domain  Подменяемый домен. Несколько опций будут преобразованы в список доменов
  [array] [default: ["local.yandex.ru","local.yandex.by","local.yandex.ua","local.yandex.kz","local.yandex.uz","local.ya
  ndex.com","local.yandex.com.tr","local.yandex.az","local.yandex.com.am","local.yandex.com.ge","local.yandex.co.il","lo
  cal.yandex.kg","local.yandex.lv","local.yandex.lt","local.yandex.md","local.yandex.tj","local.yandex.tm","local.yandex
                        .uz","local.yandex.ee","local.yandex.fr","local.yandex.fi","local.yandex.pl","local.yandex.eu"]]

log-cleaner options
  --log-cleaner-log-dir             Путь до директории хранения логов
                                                                    [string] [default: "/Users/fenice/.yandex-int/logs"]
  --log-cleaner-max-dir-size        Максимальный размер директории логов в байтах.
                                    При превышении старые логи будут удалятся пока общий размер директории не станет
                                    меньше указанного значения.
                                    Если равно -1, то файлы с логами не удаляются         [number] [default: 1073741824]
  --log-cleaner-max-files           Максимальное количество файлов с логами                      [number] [default: 200]
  --log-cleaner-keep-files-per-dir  Mинимальное количество файлов с логами в каждой поддиректории, которые нужно
                                    сохранить при удалении                                        [number] [default: 20]
```

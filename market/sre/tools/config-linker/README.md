# config-linker
Утилита config-linker служит для полу-автоматического подключения/отключения конфигов в зависимости от членства хоста в кондукторных группах. Иными словами, она ищет конфиги в каком-то "sites-available" и автоматически линкует нужные в какой-то "sites-enabled". При этом, есть возможность автоматически вычищать sites-enabled от неактуальных симлинков. 

### Параметры командной строки
```
$ config-linker -h
Usage of src/cmd/config-linker/config-linker:
  -cgroup-strip
      Strip conductor groups names from destination symlinks [Environment variable: LINKER_CGROUP_STRIP]
  -debug
      Turn on debug logging [Environment variable: DEBUG]
  -dry-run
      Don't actually delete or link anything [Environment variable: LINKER_DRY_RUN]
  -dst string
      Destination folder (should be different from source folder) [Environment variable: LINKER_DST] (default "/Users/maxk/packages/arcadia/market/sre/tools/config-linker")
  -dst-clean
      Remove all files with src-extension, which're not generated in a current run of linker [Environment variable: LINKER_CLEAN_DST]
  -fqdn string
      Set local FQDN [Environment variable: LINKER_FQDN]
  -http-requests int
      Set maximum number of parallel http-requests, [Environment variable: LINKER_HTTP_REQUESTS] (default 16)
  -http-retries int
      Set maximum number of retries for http-requests, [Environment variable: LINKER_HTTP_RETRIES] (default 3)
  -http-timeout duration
      Timeout in ms for http-requests, [Environment variable: LINKER_HTTP_TIMEOUT] (default 5s)
  -log-level string
      Logging level: DEBUG, INFO, WARN, ERROR, DPANIC, PANIC, FATAL [Environment variable: LOG_LEVEL] (default "INFO")
  -log-style string
      Force log style to be: console, json or auto. Default is auto. [Environment variable: LOG_STYLE] (default "auto")
  -multithreaded-io
      Do delete and symlink file operation in parallel [Environment variable: LINKER_MULTITHREADED_IO]
  -nocache
      Don't use conductor cache [Environment variable: LINKER_NOCACHE]
  -src string
      Source folder (should be different from destination folder) [Environment variable: LINKER_SRC] (default "/Users/maxk/packages/arcadia/market/sre/tools/config-linker")
  -src-ext string
      Source files' extension [Environment variable: LINKER_SRC_EXT]
  -verbose
      Be verbose and show trace-messages [Environment variable: VERBOSE]
  -version
      Show version and exit
```

### Алгоритм работы
Файлы в каталоге `-src` должны иметь расширение `-src-ext` (по-умолчанию – любое) и подпадать под регулярное выражение `/^\d+-.*\.[^\.]+\.[^\.]$/`, т.е. начинаться с числа, заканчиваться каким-то расширением и иметь суффикс. Этот суффикс воспринимается утилитой как кондукторная группа и, если локальный хост (можно для тестирования задать параметром командной строки `-fqdn`) входит в эту группу, конфиг будет слинкован в директорию `-dst`. При этом, могут существовать несколько файлов, начинающихся с одного и того же номера (префикса), но в этом случае будет слинкован только один – тот, у которого кодукторная группа максимальной длины. Пример:
если в исходном каталоге 2 файла:
```
258-market-preport.market_slb-testing.yaml
258-market-preport.market_slb.yaml
```
Слинкован будет только `258-market-preport.market_slb-testing.yaml`, т.к. длина кондукторной группы `market_slb-testing` больше длины `market_slb`.

Имя файла назначения обычно будет совпадать с именем файла источника, но можно указать опцию `-cgroup-strip` и тогда из него будет выкушен суффикс-кондукторная группа, ex: `258-market-preport.market_slb-testing.yaml` -> `258-market-preport.yaml`.

Если задан параметр `-dst-clean`, то после операции линковки будет произведена очистка каталога `-dst` от файлов с расширением `-src-ext`, имена которых начинаются с числа (`/^\d+-/`). Удаляться будут только симлинки, обычные файлы и каталоги не удаляются.

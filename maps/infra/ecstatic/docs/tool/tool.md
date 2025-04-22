## Ecstatic tool

Ecstatic tool - cmdline тулза для работы c ecstatic 

### Установка {#install}

Ecstatic tool является частью карточного [базового образа](https://a.yandex-team.ru/arc/trunk/arcadia/maps/infra/baseimage). Никаких доплонительных действий для использования делать не надо.

Для установки на dev-тачки необходимо поставить пакет`yandex-maps-ecstatic-tool` следующим образом:

1. Добавить в sources.list репозиторй yandex-musl:
```
# Пишем следующее в /etc/apt/sources.list.d/yandex-musl.list
deb http://yandex-musl.dist.yandex.ru/yandex-musl unstable/all/
deb http://yandex-musl.dist.yandex.ru/yandex-musl unstable/$(ARCH)/
deb http://yandex-musl.dist.yandex.ru/yandex-musl testing/all/
deb http://yandex-musl.dist.yandex.ru/yandex-musl testing/$(ARCH)/
deb http://yandex-musl.dist.yandex.ru/yandex-musl prestable/all/
deb http://yandex-musl.dist.yandex.ru/yandex-musl prestable/$(ARCH)/
deb http://yandex-musl.dist.yandex.ru/yandex-musl stable/all/
deb http://yandex-musl.dist.yandex.ru/yandex-musl stable/$(ARCH)/
```
2. Устанавливаем пакет:
```shell
sudo apt update && sudo apt install yandex-maps-ecstatic-tool
```

### Использование {#usage}

Для работы с ecstatic tool необходимо переопределить environment ecstatic-а. По дефолту берется environment хоста.
Это можно сделать с помощью переменной окружения `ENVIRONMENT_NAME`.
Существует 4 окружения ecstatic:
- [unstable](http://core-ecstatic-coordinator.common.unstable.maps.yandex.net)
- [testing](http://core-ecstatic-coordinator.testing.maps.yandex.net)
- [datatesting](http://core-ecstatic-coordinator.datatesting.maps.yandex.net)
- [stable](http://core-ecstatic-coordinator.maps.yandex.net)

Также, при необходимости использования авторизации нужно указать tvm-id приложения указанного в секции `generate` у датасета в конфигах, а также опционально секрет. 

```shell
# ecstatic tool попробует сходить в секретницу и получить секрет tvm приложения
ecstatic --tvm-id 12345 remove yandex-maps-jams-speeds:1of8=1234

# ecstatic tool обменяет tvm secret из cmdline на тикет и будет с ним работать
ecstatic --tvm-id 12345 --tvm-secret qwerty remove yandex-maps-jams-speeds:1of8=1234 
```

Также, есть возможность определить эти аргументы через переменные окружения:

- `--tvm-id` = `ECSTATIC_TVM_ID`
- `--tvm-secret` = `ECSTATIC_TVM_SECRET`

### Команды {#commands}

#### ecstatic download {#download}

Скачивает указанный датасет в определенную директорию

```shell
Usage: ecstatic download [OPTIONS] <dataset>=<version>

  Download datasets to specified local directories

Options:
  -o, --out TEXT                  Directory to download
  --debug-torrent                 Turn on debug logs from torrent client
  --libtorrent-option <TEXT TEXT>...
                                  Libtorrent options
  --help                          Show this message and exit.
```

Пример использования:

```bash
# скачается в папку ./yandex-maps-jams-speeds:8of8_2020.12.22.13.44.30
ecstatic download yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30

# скачается в папку ./jams
ecstatic download yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 -o jams
```

#### ecstatic move {#move}

Перемещает датасет в определенный бранч.

{% note warning "Attention" %}
Необходима авторизация
{% endnote %}

```shell
Usage: ecstatic move [OPTIONS] <dataset>=<version> [BRANCHES]...

  Switch dataset for specified branch(es) in form +<branch>[/hold] or
  -<branch> ...

Options:
  --help  Show this message and exit.
```

Пример использования:

```shell
# мувает указанный датасет в stable и testing
ecstatic --tvm-id=12345 move yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 +stable +testing

# удаляет указанный датасет из бранча stable
ecstatic --tvm-id=12345 move yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 -- -stable
```

#### ecstatic remove {#remove}

Удаляет указанный датасет из ecstatic 
{% note warning "Attention" %} Необходима авторизация {% endnote %}

```shell
Usage: ecstatic remove [OPTIONS] <dataset>=<version>

  Remove specified version

Options:
  --help  Show this message and exit.
```

Пример использования:

```shell
ecstatic --tvm-id=12345 remove yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30
```

#### ecstatic reset_errors {#reset_errors}

Сбрасывает ошибки на хуках, чтобы поретраить их запуск

```shell
Usage: ecstatic reset_errors [OPTIONS] <dataset>=<version> GROUP

  Unset hooks errors on group for version of dataset, likely will restart
  hooks

Options:
  --help  Show this message and exit.
```

Пример использования:

```shell
ecstatic reset_errors yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 rtc:maps_core_ecstatic_coordinator_stable
```

При появлении ошибок на `* NEW` группах при реаллокации, нужно указать именно `* NEW` группу

Например:

```shell
ecstatic reset_errors yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 "rtc:maps_core_ecstatic_coordinator_stable NEW"
```

#### ecstatic upload {#upload}

Загружает указанный датасет в ecstatic и опционально мувает его в бранч
{% note warning "Attention" %} Необходима авторизация {% endnote %}

```shell
Usage: ecstatic upload [OPTIONS] <dataset>=<version> DIRECTORY [BRANCHES]...

  Upload torrent from local directory and switch branch (if any) in form
  +<branch>[/hold]

Options:
  -v, --verbose                   Turn on verbose output from Torrent
  --debug-torrent                 Turn on debug mode for Torrent client
  --libtorrent-option <TEXT TEXT>...
                                  libtorrent options
  --help                          Show this message and exit.
```

Пример использования:

```shell
# Просто загрузить датасет
ecstatic --tvm-id=12345 upload yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 dataset_dir

# Загрузить и мувнуть в stable
ecstatic --tvm-id=12345 upload yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 dataset_dir +stable
```

#### ecstatic versions {#versions}

Показывает список версий датасета, а также (опционально) статус активации

```shell
Usage: ecstatic versions [OPTIONS] DATASET [BRANCH]

  Get versions of dataset

Options:
  --with-status  Include status information
  --help         Show this message and exit.

```
Пример использования:

```shell
# просто вывести список версий
ecstatic versions yandex-maps-jams-speeds

# показать статус активации всех версий датасета
ecstatic versions yandex-maps-jams-speeds --with-status
```

#### ecstatic wait {#wait}

Дождаться активации определенной версии в бранче

```shell
Usage: ecstatic wait [OPTIONS] <dataset>=<version> BRANCH

  Wait for dataset=version to became active

Options:
  --target-state status  Target status of dataset to wait for
  --timeout n            Timeout in seconds for wait process (by default -
                         wait 1 hour)
  --help                 Show this message and exit.
```

Пример использования:

```shell
ecstatic wait yandex-maps-jams-speeds:8of8=2020.12.22.13.44.30 stable
```

#### ecstatic client run_with_local_lock {#local_lock}

Запускает команду под локальным локом, который приостанавливает активацию новых данных в ecstatic client

```shell
Usage: ecstatic client run_with_local_lock [OPTIONS] [COMMAND]...

Options:
  --lock-timeout INTEGER  The maximum time waited for the lock.
                          If `timeout <
                          0`, there is no timeout and this command will
                          block
                          until the lock could be acquired.
                          If `timeout = 0`
                          there is only one attempt to take the lock.
  --help                  Show this message and exit.
```

Пример использования:

```shell
ecstatic client run_with_local_lock -- curl example.com
```

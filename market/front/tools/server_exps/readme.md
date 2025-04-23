# Утилита для управления серверными экспериментами

Это консольная утилита позволяющая выкатывать различные конфигурации серверных экспериментов в разные сервисы.
В качестве входных параметров используются название дашборда, тип окружения и конфигурация флагов экспериментов.

## Установка

```bash
ya make --checkout market/front/tools/server_exps
```

### Использование

```
market/front/tools/server_exps/bin/server_exps --help

usage: server-exps [-h]
                   (-d dash_id | -s {partner,vendors,affiliate,red,white_desktop,white_touch,blue_desktop,white_fapi,blue_fapi,blue_touch})
                   [-e {test,prod,prestable}] [-t TICKET] [--all]
                   [--no-common] [--sample | --no-sample]
                   [--kraken | --no-kraken] [--preview | --no-preview]
                   [--canary | --no-canary] [--dry]
                   config

Configuration and deploy of server experiment flags

positional arguments:
  config                path to flags configuration file

optional arguments:
  -h, --help            show this help message and exit
  -d dash_id, --dashboard dash_id
                        nanny dashboard id
  -s {partner,vendors,affiliate,red,white_desktop,white_touch,blue_desktop,white_fapi,blue_fapi,blue_touch}, --service {partner,vendors,affiliate,red,white_desktop,white_touch,blue_desktop,white_fapi,blue_fapi,blue_touch}
                        service alias
  -e {test,prod,prestable}, --env {test,prod,prestable}
                        environment name
  -t TICKET, --ticket TICKET
                        ticket and description
  --all                 deploy on all instance types
  --no-common           skip deploy on common instances
  --sample              deploy on sample instances
  --no-sample           skip deploy on sample instances (overrides --all
                        option)
  --kraken              deploy on kraken instances
  --no-kraken           skip deploy on kraken instances (overrides --all
                        option)
  --preview             deploy on content preview instances
  --no-preview          skip deploy on content preview instances (overrides
                        --all option)
  --canary              deploy on canary instances
  --no-canary           skip deploy on canary instances (overrides --all
                        option)
  --dry                 dry-run (do not actually do something, only print
                        messages)
```

Основные параметры:

 * `config` единственный пропозиционный параметр - конфиг флагов эксперимента
 * `--dashboard / -d` название дашборда
 * `--service / -s` название сервиса. Короткий алиас вместо названия дашбора
 * `--env / -e` название окружения. По-умолчанию `prod`
 * `--ticket / -t` номер и название тикета в стартреке (используется для описании выкатки в Няне). Если не указан, будет запрошен позже в интерактивном режиме.

Дополнительные параметры:

 * `--all` выбирает все возможные сервисы из дашборда. По-умолчанию исключаются сервисы типа canary, kraken, sample, preview
 * `--no-common` удаляет из выборки обычные сервисы (не canary, kraken, preview, sample)
 * `--canary / --no-canary` добавляет / удаляет из выборки canary сервисы
 * `--kraken / --no-kraken` добавляет / удаляет из выборки kraken сервисы
 * `--sample / --no-sample` добавляет / удаляет из выборки sample сервисы
 * `--preview / --no-preview` добавляет / удаляет из выборки preview сервисы
 
Отладочные параметры:

 * `--dry` делает запуск в холостом режиме. Изменения никуда не отправляются и не активируются.

### Формат конфига

Конфиг представляет из себя json, в котором ключи - это названия флагов, а значение - это описание группы хостов на которые требуется выкатить этот флаг.

Описание может быть в одном из 3х форматов:

  * дробное число x, `0 < x && x < 1` - процент хостов на который требуется выкатить флаг
  * целое число x, `x >= 1` - количество хостов на которые требуется выкатить флаг
  * массив строк - конкретные названия хостов на которые требуется выкатить флаг  

```json
{
  "deploy_on_1/4_of_all_hosts": 0.25,
  "deploy_on_5_hosts": 5,
  "deploy_on_hosts": ["host1", "host2", "host3"]
}
```

Технически допустимо использовать все 3 формата в одном файле, однако это крайне не рекомендуется - желательно выбрать только один формат и использовать его для всех перечисленных флагов.

### Результат

Результатом работы скрипта является запущенный деплой сервисов с файлом `experiments.json` в корне инстанса с содержимым вида:

```json
{
  "deploy_on_1/4_hosts": [
    "host4", "host5", "host6"
  ],
  "deploy_on_5_hosts": [
    "host7", "host8", "host9", "host10", "host11"
  ],
  "deploy_on_hosts": [
    "host1", "host2", "host3"
  ]
}
```

Данный файл будет идентичным для всех сервисов на которые он раскатывается (т.е. в нём будут перечисленны в том числе хосты из других сервисов)

Флаги экспериментов распределяются максимально равномерно и пропорционально по дата-центрам и сервисам без пересечений. В случае если невозможно распределить флаги по хостам в соответствии с заданным конфигом, возникнет ошибка исполнения (например при попытке выкатить флаги суммарно на 20 хостов при том что всего в наличии 12 хостов)

Равномерность означает, то при возможности в каждом сервисе будет выбран как миниум 1 хост. Пропорциональность означает, что если в сервисе `A` хостов в 2 раза больше чем в сервисе `B`, то и в выборку из этого сервиса попадёт в 2 раза больше хостов. Например при выкатке флагов `good` и `bad` на 50% каждый в такие сервисы:

```
service1: host1, host2, host3, host4, host5, host6, host7, host8
service2: host9, host10, host11, host12
service3: host13, host14
```

Получится такой список хостов (конкретный выбор хостов может отличаться):

```
good: host1, host2, host3, host4, host9, host10, host13
bad: host5, host6, host7, host8, host11, host12, host14
```

Выбор хостов не стохастический - при одинаковых конфигах флагов и списках хостов, результат будет одинаков.

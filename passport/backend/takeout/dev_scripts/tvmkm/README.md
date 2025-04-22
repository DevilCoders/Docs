# tvmkm - TVM Keyring Manager

Программа для управления связками TVM client_id и alias

## Настройка

В корень проекта надо положить файл `tvmkm.conf` со следующим содержанием:
```
keyring_testing: путь_до_конфига_tvm_keyring_в_тестинге
keyring_production: путь_до_конфига_tvm_keyring_в_проде
```

## Добавление нового сервиса

```
$ ./dev_scripts/tvmkm/tvmkm add --help
usage: tvmkm add [-h] [-c CONFIG] alias client_id_testing client_id_production

positional arguments:
  alias
  client_id_testing
  client_id_production

optional arguments:
  -h, --help            show this help message and exit
  -c CONFIG, --config CONFIG
```

## Удаление потребителя

```
$ ./dev_scripts/tvmkm/tvmkm del --help
usage: tvmkm del [-h] [-t] [-p] [-c CONFIG] alias

positional arguments:
  alias

optional arguments:
  -h, --help            show this help message and exit
  -t, --test            Delete from test keyring
  -p, --prod            Delete from production keyring
  -c CONFIG, --config CONFIG
```

## Отобразить текущую конфигурацию

```
$ ./dev_scripts/tvmkm/tvmkm list --help
usage: tvmkm list [-h] [-c CONFIG]

optional arguments:
  -h, --help            show this help message and exit
  -c CONFIG, --config CONFIG
```

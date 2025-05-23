# Скрипт закрытия/открытия в рамках учений

## Проверка перед учениями

* Установлен `executer`,
    * Информацию про `executer` можно найти [здесь](https://wiki.yandex-team.ru/users/serj0/executer/),
    * Конфиги лежат в `/etc/executer` или в `~/.executer.conf`.
    * В конфиге указан `project_filter = ofd,paysys`.
* Установлен [ya](https://docs.yandex-team.ru/yatool/).
* Есть все нужные права и всё необходимое настроено.

Пример проверки для Ивантеевки:
```bash
$ ya make
$ ./spirit_drills status --dc iva
```

## Закрыть все наши сервисы
Пример для Ивантеевки:
```bash
./spirit_drills stop --dc iva
```

## Открыть все наши сервисы
Пример для Ивантеевки:
```bash
./spirit_drills start --dc iva
```

## Дополнительные опции

* `--silent` - скрипт не будет спрашивать подтверждение намерений пользователя перед запуском команды на каждом компоненте, попросит только в самом начале подтвердить что он корректно понял аргументы
* `--cache` - не обновлять кэш `executer`-а перед стартом скрипта (можно добавлять если есть уверенность что локальный кэш актуален)

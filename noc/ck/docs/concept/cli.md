# Использование cli

Небольшой пример взаимодействия с cli приведен в разделе Быстрый старт. `noc-ck-cli` развернут на сервере `noc-sas`.
Перед началом работы требуется выполнить `noc-ck-cli auth` для получения токена аутентификации.
Если токен не работает, надо удалить файл `~/.noc-ck` и выполнить `noc-ck-cli auth` заново.

Текущий набор поддерживаемых аргументов можно получить по `noc-ck-cli --help`

```
% noc-ck-cli --help
Usage: run.py [OPTIONS] COMMAND [ARGS]...

Options:
  --host TEXT    CK backend server
  --local        Use localhost as server
  -v, --verbose  Will print verbose messages.
  --help         Show this message and exit.

Commands:
  auth                     Получить токен для аутентификации
  create-declarative       Создать новый сценарий через YAML-файл
  get-declarative          Получить текущее содержимое YAML по имени
  job-action-list          Список action-ов джобы.
  job-cancel               Отменить джобу.
  job-ctx-show             Показать контекст джобы.
  job-list                 Список джобов.
  job-resume               Продолжить выполнение джобы ушедшей в paused.
  job-run                  Запустить джобу после ее создания.
  job-show                 Информация о джобе.
  launch-cancel            Отменить запуск.
  launch-create            Создать запуск сценария.
  launch-create-from-file  Создать запуск сценария по списку из файла.
  launch-list              Список запусков.
  launch-run               Запустить запуск после его создания.
  launch-show              Информация о запуске.
  replace-declarative      Обновить существующий сценарий через...
```

Через cli так же можно общаться с локальным dev-инстансом ЦК. Для того чтобы его развернуть следуйте инструкциям в пункте ниже. После инициализации dev-окружения `noc-ck-cli` будет доступен в venv'e:

```
azryve@azryve-osx noc-ck % ./venv/bin/noc-ck-cli --help
Usage: noc-ck-cli [OPTIONS] COMMAND [ARGS]...
...
```

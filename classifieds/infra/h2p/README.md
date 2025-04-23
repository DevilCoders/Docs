# h2p

wiki: https://wiki.yandex-team.ru/vertis-admin/h2p/

## Компоненты
- **h2p**
   - Является ssh сервером и tcp проксей для клиентов.
- **h2p-idm**
   - Является бэкендом для IDM https://wiki.yandex-team.ru/intranet/idm/
- **cli**
   - cli тулза на замену баш скрипта

## Локальная разработка
```shell
# Для установки cli для миграций 
> make reqs
# Для поднятия зависимостей из докер файла и запуска миграций
> make up
```

### Cli 

Для локальной разработки и тестирования можно переопределить переменные конфига.
Для этого:
1. скопировать файл `cmd/cli/test.env` в `cmd/cli/.h2p.env`
    ```shell script
    cp cmd/cli/test.env cmd/cli/.h2p.env
    ```
2. Переопределить переменные в `cmd/cli/.h2p.env`

### Запуск тестов

```go test ./...```

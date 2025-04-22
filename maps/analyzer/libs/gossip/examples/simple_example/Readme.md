# Пример использования протокола.

## Usage:

Создаём конфиги системы(defaultServers.json - пример готового)

Запускаем серверы скриптом bootstrapper/bootstrapper.
Скрипт читает конфиг с конфигурацией серверов(default_servers.json) и запускает требуемое количество процессов.

```bash
./bootstrapper -C="path_to_config"
```

Даллее можно вручную слать запросы, например:

```bash
curl "http://consumer_host/upload?mesId=1&server=localhost"
```

server=localhost - нужно указывать вместо localhost имя любого хоста из дистрибьютеров, указанных в
конфиге.

Логи пишутся в папку consumer/logs - у каждого сервера свой файл.

Чтобы убить процессы:

```bash
cd bootstrapper/killer && ./killer
```

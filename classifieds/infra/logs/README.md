# Disclaimer

Логи вертикалей. Перенесено из github, для go-приложений сохранён vendor на случай специальной операции и потери данных

## Структура проекта

TODO: backend/vtail - это группа микросервисов вокруг логов, должны съехаться в один фолдер

### backend

- cmd/agent: хелпер-процесс для сборки логов с процессов
- cmd/docker-driver: драйвер для сборки логов из контейнеров в
- cmd/collector: приёмщик логов для перекладывания в logbroker
- cmd/golf: сервис по перекладыванию логов из logbroker в clickhouse
- cmd/golf-cleaner: сервис по очистке старых партов в кликхаусе, в текущей реализации запускается по cron

### vtail

Сервис по поставке live-логов и бекенд к графана-плагину

- cmd/cli: cli-тулза для запросов за live-логами
- cmd/backend: сервис для обработки api-запросов
- cmd/streamer: сервис буферизации логов из логброкера, перекладывает их в backend
- cmd/query: бекенд для запросов исторических логов для grafana-плагина

### grafana-plugin

datasource-плагин к grafana для отображения логов

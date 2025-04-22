# logs
Недомонореп про поставку логов контейнеров

## components

### logs-driver

Docker logging driver. [Доп. инфо](../master/cmd/docker-driver/README.md)

### logs-agent
Компонент отправки логов в Y.Deploy
Сборка:
- `make agent-rootfs`
- зайти по ссылке в sandbox
- прописать новый rbtorrent в конфиге shiva

### logs-collector

Локальный запуск:
 - [Создать топик](https://lb.yandex-team.ru/docs/quickstart/) в лог брокере.
 - [Получить OAuth](https://logbroker.yandex-team.ru/docs/concepts/security/#oauth) токен.
 - Создать файл `local.env`, где переопределить все переменные из файла `dev.env`, которые отмечены строкой `#override me`
 - Запустить зависимости `docker-compose -f teamcity-services.yml up -d`

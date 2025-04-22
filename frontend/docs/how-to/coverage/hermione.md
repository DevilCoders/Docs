# Подсчет покрытия в hermione

## Подключение

1. Установить пакет [@yandex-int/hermione-coverage](../../packages/hermione-coverage/), подключить плагин для hermione и настроить сборку согласно [инструкции](../../packages/hermione-coverage/README.md)
2. Добавить в package.json скрипт `ci:hermione:coverage` который запускает hermione с переменной окружения `COVERAGE=1`. Пример: `"ci:hermione:coverage": "COVERAGE=1 npm run ci:hermione"`

[Пример подключения](https://a.yandex-team.ru/review/1896796/files/f624129abbf8b37a49e103d61868102b20fa2a05) подсчета покрытия для сервиса на RR в монорепозитории.

## Просмотр отчета в транке

Джоба для посчета покрытия в hermione запускается в транке, поэтому в ПРе на данный момент посмотреть покрытие нельзя. Покрытие в транке после мержа ПРа можно найти при помощи [инструкции](./find-trunk-build.md) в отчете джобы "Hermione: coverage master".

Пример отчета о покрытии: ![image](../../images/hermione-coverage.png)

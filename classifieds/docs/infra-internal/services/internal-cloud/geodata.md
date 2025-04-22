# Привоз geodata6.bin

Официальная документация про `geodata6.bin` - [тут](https://wiki.yandex-team.ru/geotargeting/libgeobase/)

## Основная информация

geodata6.bin - бинарный файл, обновляющийся 2 раза в сутки, который поставляется из [sandbox](https://sandbox.yandex-team.ru/tasks?children=false&created=14_days&hidden=false&type=GEODATA6BIN_STABLE_BUILDER) средствами пакета `p2p-distribution-geodata6-config`.

Плюсы такого пакета: собирается и контролируется другой командой, распределенное скачивание файла.

Минусы пакета: файлы доезжают с большой задержкой, поэтому часто горят мониторинги, а хосты встают в кластер позже.

Мы написали свою замену `p2p-distribution-geodata6-config`, которая состоит из серверной части и клиентской части.

## Серверная часть

Исходный код серверной части лежит в репозитории [admin-dockerfiles](https://a.yandex-team.ru/arc_vcs/classifieds/infra/admin-dockerfiles/geodata-transfer).

Это bash-скрипт, который перекладывает актуальную версию `geodata6.bin` из sandbox в s3 с проверкой актуальности. В качестве маркера актуальности выступает `resource id`, который при перекладывании файла записывается в метадату файла в s3. Если файл с `resource id` уже есть в s3, скрипт выводит в лог соответствующее сообщение и завершает работу.

Скрипт живет в виде батч-джобы [geodata-transfer](https://a.yandex-team.ru/arc_vcs/classifieds/services/deploy/geodata-transfer.yml) в шиве. Текущую актуальную версию сервиса можно узнать в телеграм-боте.

## Клиентская часть

Клиентская часть упакована в пакет [yandex-vertis-geodata6](https://a.yandex-team.ru/arc_vcs/classifieds/infra/vertis-packages/yandex-vertis-geodata6). Пакет привозит:
* скрипт `bring-geodata.sh`;
* крон-файл для периодического запуска `bring-geodata.sh`;
* проверку для monrun.

Скрипт `bring-geodata.sh` выполняет действия, аналогичные серверной части. Он перекладывает `geodata6.bin` из s3 на хост с проверкой актуальности по `resource id`.
Логи пишутся в `/var/log/bring-geodata/bring-geodata.sh`. Туда же пишется информация об изменении локального файла с его текущим и устаревшим `resource id`.

## Мониторинг

На дашборде [basic components version](https://grafana.vertis.yandex-team.ru/d/BnBoBHMnk/basic-components-versions?orgId=1) представлены метрики по текущим `resource id` в s3 и на хостах и текущая версия пакета `yandex-vertis-geodata6` на хостах.

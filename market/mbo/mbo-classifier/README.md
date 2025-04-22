Интерфейс классификатора
================

Выкладка пакетов происходит релизной машиной автоматически при мержах в мастер.
Релизная машина: https://tsum.yandex-team.ru/pipe/projects/mbo/delivery-dashboard/mbo-classifier-arcadia

###Ручной запуск переливки индекса с базы

Переливку можно запустить с помощью скрипта mbo-classifier2-reload.sh.

Формат запуска:

`sudo ./mbo-classifier2-manual-reload.sh <что переливать> <куда переливать> <директория для записи логов>`

Пример:

`sudo ./mbo-classifier2-manual-reload.sh ru_markup ru_markup_reloading /var/log/yandex/mbo-classifier`

Пример в RTC, из хомки (в rtc также надо передавать окружение в запуск):
`sudo ./bin/mbo-classifier2-manual-reload-rtc.sh ru_markup ./pdata/mbo-classifier/ru_markup_reloading ./logs/mbo-classifier testing`

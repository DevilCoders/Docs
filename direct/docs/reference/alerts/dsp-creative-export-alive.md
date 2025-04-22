# dsp-creative-export-alive

[Алерт](https://solomon.yandex-team.ru/admin/projects/direct/alerts/dsp-creative-export-alive) на живость выгрузки креативов из `canvas` в YT.
[Сырое событие](https://juggler.yandex-team.ru/raw_events/?query=service%3Ddsp-creative-export-alive&last=1DAY) в Juggler.

## Описание { #description }
В данной проверке проверяется, что неудачно выгруженных креативов в YT было не слишком много: не больше, чем успешных и не больше 50 в абсолютном значении за последние 15 минут.
Если креативы не выгружаются, то БК не видит изменения в существующих и не получает новые, что негативно сказывается
на доступности Директа.

## Диагностика { #diagnostics }
Сначала надо посмотреть на [график](https://solomon.yandex-team.ru/?project=direct&cluster=push&service=push&env=production&flow=dsp_creative_export&graph=dsp-creative-export) в Solomon.
По нему будет понятно, в какой момент началась проблема и продолжается ли она. Если проблема присутствует,
то следует посмотреть `messages` логи, например [так](https://direct.yandex.ru/logviewer/short/PPYGZZg43dGpEi).

## Ссылки { #links }
- [график выгрузки креативов в Solomon](https://solomon.yandex-team.ru/?project=direct&cluster=push&service=push&env=production&flow=dsp_creative_export&graph=dsp-creative-export)
- [алерт в Solomon](https://solomon.yandex-team.ru/admin/projects/direct/alerts/dsp-creative-export-alive)
- [сырое событие в Juggler](https://juggler.yandex-team.ru/raw_events/?query=service%3Ddsp-creative-export-alive&last=1DAY)
- [логи в Logviewer](https://direct.yandex.ru/logviewer/short/PPYGZZg43dGpEi)
- [очередь в YT](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/adv/queues/DspCreativeQueue/queue)
- [таблица в YT](https://yt.yandex-team.ru/markov/navigation?offsetMode=key&path=//home/adv/DspCreative)
- [сервис в канвасе](https://a.yandex-team.ru/arc/trunk/arcadia/direct/canvas/src/main/java/ru/yandex/canvas/service/RTBHostExportService.java)

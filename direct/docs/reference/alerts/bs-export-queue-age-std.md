# queue_std.age_minutes

[juggler](https://juggler.yandex-team.ru/check_details/?host=direct.perl_bsexport&service=queue_std.age_minutes&query=&last=1DAY)

## Описание { #description }
Проверка о возрасте очереди std экспорта в БК.

Состоит из нескольких частей:
- queue_std.age_minutes_p80 — если 80 перцентиль возраста превышает 45 минут (половина SLA) — покрывает массовые поломки
- queue_std.age_minutes_p99 — пытаемся ловить проблемы, пропуская единичные аномалии (бывают большие кампании):
    - warn на 90 минут
    - crit на 3 часа
- queue_std.age_minutes_p100 — проверяем максимальный возраст очереди — против застревания кампаний совсем. поэтому тут пороги еще выше:
    - warn при превышении 4.5 часов (3хSLA)
    - crit при превышении суток

## Диагностика { #diagnostics }
По дашборду об [очереди STD](https://solomon.yandex-team.ru/?project=direct&dashboard=bs-export-queue-templated&queue=std&service=bs-export-queue&cluster=app_java-jobs) — понять в каком шарде проблема,
потом по [общему дашборду](https://solomon.yandex-team.ru/?project=direct&dashboard=bs-export-perl&b=6h) убедиться,
что это не глобальная проблема (из-за ошибок отправки или проблем с другими очередями).

Посмотреть кампании в [голове очереди std]({{bsexport-queue-std}}),
определить проблемные и диагностировать их по [общей инструкции](../bs-export-diag.md#how-to).

## Решение { #solution }
Смотри [{#T}](../bs-export-diag.md#debug).

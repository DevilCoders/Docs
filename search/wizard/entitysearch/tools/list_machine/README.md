# Шеф, все упало!

При падении YT пишет корки в табличку, которая указана как второй выход кубика (core). Чтобы понять, что произошло, необходимо:

## Подготовка

### Скачиваем бинарь

Общая команда выглядит как `curl --fail -H "Authorization: OAuth $NIRVANA_TOKEN" https://nirvana.yandex-team.ru/api/.../data -o list_machine`.

Если вы запускали кубик с вшитым бинарем, то на странице кубика нужно будет кликнуть `... -> Export Dump` ([like this](https://jing.yandex-team.ru/files/greengrape/UNADJUSTEDNONRAW_thumb_5.jpg)) и в дампе найти `storedDataId` и вместо `...` подставить `storedData/{id}`.
Если вы запускали кубик с кастомным бинарем, то просто достаньте его из sandbox (или же найдите `id` ресурса в нирване ([like this](https://jing.yandex-team.ru/files/greengrape/Image%2012-11-20%20at%201.32%20PM.jpg)) и вместо `...` подставьте `ui/storedItem/{первая часть id}/{вторая часть id}`).

### Скачиваем корку

Тут все просто -- `ya tool yt download-core-dump --core-table-path {табличка}`. Команда по умолчанию скачает одну случайную корку в файл `core.0` (не пугайтесь размера самой таблички, в реальности одна корка весит порядка 6gb).

## Исследуем корку

`ya tool gdb --core core.0 list_machine`

Делаем `bt`, прыгаем по фреймам, зовем везде `info args/info locals` и радуемся жизни! Стоит помнить, что команды здесь выполнять нельзя, в частности, `DebugString()` у протобафа.

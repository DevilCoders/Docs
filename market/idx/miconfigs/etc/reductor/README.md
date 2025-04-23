# Конфиги раскладки

## Генерация конфигов из шаблонов
1. В `conf-available-tmpls` лежат шаблоны конфигов в формате jinja2
2. В файле `variables.ini` перечисляются подстановки в формате `key.subkey = value`, которые будут подставляться во все шаблоны
3. На выходе генерируется папка `conf-available-gen`

## Добавление нового конфиг файла
1. Новый файл в `conf-available-tmpls`
2. В `ya.make` по аналогии надо добавить две строки `${ARCADIA_ROOT}/market/idx/miconfigs/etc/reductor/conf-available-tmpls/new_config` в секцию `IN`, а в секцию `OUT_NOAUTO` добавляем `${ARCADIA_BUILD_ROOT}/market/idx/miconfigs/etc/reductor/conf-available-gen/new_config`. Если этого не сделать, то шаблон не будет генерироваться и даже не попадет в финальную сборку.

## Конфиги быстрых данных
Все аналогично, но редактируем в директории `updater`.

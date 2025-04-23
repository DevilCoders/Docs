# realty-router

Роутера Недвижимости.
---
\
Внутри используется [susanin](https://github.com/YandexClassifieds/susanin). \
Сейчас в рамках [VTF-486](https://st.yandex-team.ru/VTF-486) мы выносим роутер в отдельный сервис (`realty-router-api`).

Роуты разделены на 2 вида:
* синхронные (не использующие json-маппинги из `realty-router/data/`)
* асинхронные (за ними нужно идти в `relaty-router-api`)

Синхронные урлы иcпользуются в `packages/shared/realty-router-static`.

Команды для генерации файлов связанных с метро:
* `make generate-metro` - обновление файла realty-router/data/metro.json
* `make generate-metro-lines` - обновление файла realty-router/data/metro_lines.json (запускать всегда при использовании `make generate-metro`)
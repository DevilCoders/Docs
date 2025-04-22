Эта библиотека собирает из нескольких табличек в YT таблицу с объектами, для которых нужно собирать сниппеты для геопоиска.

Сейчас есть два типа таких объектов:
- Организации справочника. Берутся вот из этой таблицы: https://yt.yandex-team.ru/hahn/navigation?path=//home/sprav/altay/prod/snapshot/company.
- Адреса, например "Льва Толстого, 16". Берутся из таблиц addr в YMapsDF https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest.

На выходе получается таблица с двумя колонками:
- `id` - идентификатор объекта, по которому геописк будет искать для него сниппет в SaaS.
- `location` - координаты этого объекта. Парсить значение из этой колонки нужно функцией `maps::snippets::locations::pointFromNode`.
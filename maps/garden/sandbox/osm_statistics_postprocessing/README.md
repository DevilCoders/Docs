# Постобработка таблиц со статистикой OpenStreetMap

Билды модуля `ymapsdf_osm` после сборки генерируют таблицу `statistics`, которая потом добавляется в конец
таблицы `all_statistics` для всех билдов этого модуля, запущенных в одном контуре. Так как потом эта таблица
используется для построения дашбордов, то для ускорения работы нужно проводить сортировку по определенным
столбцам. Результат сортировки записывается в таблицу `all_statistics_sorted`.

Дашборд [для стабильного контура](https://datalens.yandex-team.ru/60qyl2afztxex-statistika-konvertacii-dannyh-openstreetmap-v-ymapsdf).

Сортируемая таблица [в стабильном контуре](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf_osm/all_statistics).
[Результат сортировки](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/prod/ymapsdf_osm/all_statistics_sorted)

Модуль генерации вспомогательных датасетов для построения пробок HERE
===

<b>UPDATE: </b>
Модуль разобран, все ресурсы освобождены. Код сохранён до лучших времен. Тикет закрытия сервиса: https://st.yandex-team.ru/MAPSJAMS-3316

---
Модуль зависит от следующих данных:
- [`tmc_locations`](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/here-tmc-locations) - таблицы в YT, которые предоставляет партнёр (раз в 3 или 6 месяцев)
- road_graph - дорожный граф, строящийся в Огороде (graph, persistent_index, rtree, ...)

Модуль привязывает полилинии HERE к графу, создаёт датасет с mms-файлами и загружает их в экстатик. Конкретный формат mms можно посмотреть здесь: [`tmc_storage.h`](/arc/trunk/arcadia/maps/analyzer/libs/tie_here_jams/include/tmc_storage.h)
Датасет используется затем сервисом [`jams_external`](/arc/trunk/arcadia/maps/analyzer/services/jams_external)

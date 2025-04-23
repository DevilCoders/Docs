# Пешеходная, велосипедная и транспортная навигация

staff: [yandex_content_geodev_geonavi_geo](https://staff.yandex-team.ru/departments/yandex_content_geodev_geonavi_geo)

цели группы: [Goals](https://goals.yandex-team.ru/filter?group=1213)

очередь в трекере: [MTDEV](https://st.yandex-team.ru/MTDEV)

abc root: [maps-core-masstransit](https://abc.yandex-team.ru/services/maps-core-masstransit)

wiki: [maps/dev/core/masstransit](https://wiki.yandex-team.ru/maps/dev/core/masstransit)

mail: [masstransit@](http://ml.yandex-team.ru/lists/masstransit)

## Сервисы

### maps_core_masstransit_predictor
Прогноз движения общественного транспорта.
Делает прогнозы для движения меток и ожидаемых прибытий на остановки.

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/ydbfree/services/predictor

### maps_core_masstransit_mtinfo
Информация об остановках и маршрутах общественного транспорта.
В том числе раздает статические данные о нитках и остановках, а также прогнозы от сервиса predictor.

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/mtinfo

### maps_core_masstransit_realtime_receiving
Доставка realtime-сигналов общественного транспорта в predictor.
Ходит за данными к поставщикам и пересылает их в [jams analyzer dispatcher](https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/services/jams_analyzer)

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/realtime_receiving

### maps_core_masstransit_partners_proxy
Сервис партнерского прокси.
Устанавливает VPN соединение с поставщиком данных и проксирует HTTP запросы на внутренние сервера этого поставщика.

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/info/partners_proxy

### maps_core_masstransit_router
Пешеходный и ОТ маршрутизатор.
Строит пешеходные маршруты и маршруты на общественном транспорте (смешанные).

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/router

### maps_core_masstransit_matrix
Матричный маршрутизатор общественного транспорта. Строит матрицы времен движения на общественном транспорте между парами наборов точек.

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/matrix

### maps_core_bicycle_router
Велосипедный маршрутизатор. Строит велосипедные маршруты.

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/router

### maps_core_bicycle_matrix
Матричный велосипедный маршрутизатор. Строит матрицы времен движения на велосипеде между парами наборов точек.

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/bicycle/matrix

## Непрофильные сервисы

### maps_core_time
Серверное время.
Сервер позволяет мапкиту узнать настоящее время для случаев, когда в клиенте выставлено неправильное время или неверный часовой пояс.

страничка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/mobile/server/time

## Оффлайн-процессы

### Прогноз движения общественного транспорта
Код процессов: https://a.yandex-team.ru/arc/trunk/arcadia/maps/analyzer/sandbox/masstransit

Процессы запускаются в Sandbox-шедулером таски типа `ANALYZER_REGULAR_YT_PROCESS` от имени роботов `robot-jams-testing` и `robot-jams`:
- [тестинг](https://sandbox.yandex-team.ru/schedulers?author=robot-jams-testing&task_type=ANALYZER_REGULAR_YT_PROCESS&tags=MASSTRANSIT)
- [продакшен](https://sandbox.yandex-team.ru/schedulers?author=robot-jams&task_type=ANALYZER_REGULAR_YT_PROCESS&tags=MASSTRANSIT)

### Остальные процессы
Код процессов: https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/masstransit

_todo: добавить описание каждого процесса_

## Дашборды

### Прогноз движения общественного транспорта
Показывает качество предсказаний прибытий транспорта на остановки, а также качество движения меток по карте.

ссылка: https://datalens.yandex-team.ru/mxcyjknqnfrqf-obshestvennyy-transport-ot

### Регрессия ОТ-маршрутизатора

ссылка: https://datalens.yandex-team.ru/g4ib8ofl06psc-mtrouter-regression-dashboard

### Пешеходное ведение
Метрики пешеходного ведения: количество сессий, сходы, аннотации и пр.

ссылка: https://datalens.yandex-team.ru/6u7as3wbxwcez-metriki-masstransit

### Курьерские метрики
Метрики качества маршрутизации для курьеров (Яндекс Еда, Лавка)

ссылка: https://datalens.yandex-team.ru/2duapfvtex6ou-kurerskaya-metrika

### OSM-данные
Сравнение качества велосипедной маршрутизации на данных ymapsdf и OSM

ссылка: https://datalens.yandex-team.ru/rjxj8vx1dnb8i-compare-routers-dashboard

## Документация

### Прогноз движения общественного транспорта
Вся информация про модель предсказания движения ОТ, ее структуру, исходные данные и пр.

ссылка: https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/ydbfree/docs

### Wiki
ссылка: https://wiki.yandex-team.ru/maps/dev/core/masstransit

## Роботы
https://staff.yandex-team.ru/robot-mtr

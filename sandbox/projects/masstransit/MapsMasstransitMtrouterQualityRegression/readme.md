## Общие сведения

Эта задача вычисляет регрессию качества маршрутов ОТ роутера, т.е. проверяет насколько маршруты роутера соответствуют идеальным маршрутам.
Задача запускается регулярно через планировщики для [production](https://sandbox.yandex-team.ru/scheduler/22479/view) и [testing](https://sandbox.yandex-team.ru/scheduler/22065/view) окружений ОТ роутера.
Маршруты для проверки и эталонные ответы лежат в аркадии в [файле](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/router/regression/data/routes.json).
Результаты лежат в таблице YT ([testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/yatransport-prod/testing/mtroute-statistics/regression/history&) и [production](https://yt.yandex-team.ru/hahn/navigation?path=//home/yatransport-prod/production/mtroute-statistics/regression/history&)) и представлены на [графиках](https://dash.yandex-team.ru/g4ib8ofl06psc).
Также в задаче создается ресурс Sandbox с файлом `failed.json`, в который попадют все запросы, которые не прошли проверку.


## Алгоритм работы

- Из аркадии забирается [файл](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/router/regression/data/routes.json) cо списком запросов и эталонных ответов.
- Запросы из файла отправляются на роутер (по-умолчанию в testing). Полученные ответы проверяются с помощью [библиотеки](https://a.yandex-team.ru/arc/trunk/arcadia/maps/masstransit/statistics/router/pylibs/common/lib/calc_regression.py) на наличие среди полученных маршрутов эталонный из файла.
- Создается отдельный файл (ресурс Sandbox) с запросами, для которых не нашлось эталонных ответов.
- Количество запросов и найденных эталонных ответов записывается в таблицу YT ([testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/yatransport-prod/testing/mtroute-statistics/regression/history&) и [production](https://yt.yandex-team.ru/hahn/navigation?path=//home/yatransport-prod/production/mtroute-statistics/regression/history&)).
 
## Запуск задачи в Sandbox

Задача сделана [бинарной](https://wiki.yandex-team.ru/sandbox/tasks/binary/), поэтому просто запустить ее из веб интерфейса Sandbox не получится.
Для регулярного запуска созданы планировщики ([production](https://sandbox.yandex-team.ru/scheduler/22479/view) и [testing](https://sandbox.yandex-team.ru/scheduler/22065/view)), в которых указан (в `Advanced -> Task resource`) номер ресурса с последним бинарником задачи.
При изменении кода задачи или зависимых библиотек, чтобы изменения вступили в силу, нужно загрузить новый бинарник в Sandbox и обновить id бинарника в планировщиках.
Чтобы запустить задачу руками, проще всего изпользовать кнопку `Run once` в планировщикe. 

## Визуализация данных

На [графиках](https://dash.yandex-team.ru/g4ib8ofl06psc) представлены зависимости отношения количества маршрутов, успешно прошедших проверку, к общему количеству проверенных маршрутов от времени для роутера в testing и production. Графики сделаны через публичный [ClickHouse over YT](https://yt.yandex-team.ru/docs/description/chyt/about_chyt).

Квартирные гипотезы (временно остановлено)
===

## Общая информация

По различным данным пайплайн генерирует гипотезы на добавление/исправление квартир в домах,
которые разбирают картографы. Перед добавлением гипотез в народную карту
проверяется, что рядом есть панорамы или зеркала - чтоб у картографов были какая-то
дополнительная информация для разбора гипотез.

### Информация для потребителей
| Key | Value |
| --- | --- |
| Мейнтейнеры | [Maps.GeoQuality](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) |
| Шедулеры в Sandbox| [Квартирные гипотезы, stable](https://sandbox.yandex-team.ru/scheduler/307016/view) <br/> [Квартирные гипотезы, testing](https://sandbox.yandex-team.ru/scheduler/275487/view) |
| ABC-сервис | [NMAPS Map errors hypothesis generator](https://abc.yandex-team.ru/services/maps-core-nmaps-hypgen/) |
| Исходники | [Arcadia](https://a.yandex-team.ru/arc/trunk/arcadia/maps/geoq/hypotheses/flats) <br/> [Sandbox таска](https://a.yandex-team.ru/arc_vcs/sandbox/projects/maps/geoq/hypotheses/GeoqFlatsHypotheses/__init__.py)|
| Исходные данные на YT | [ymapsdf](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/core/garden/stable/ymapsdf/latest) <br/> [Панорамы](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/streetview/release/stable/description) <br/> [Зеркала](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/maps/core/nmaps/dynamic/replica/mrc/signals_feature) |
| Последняя отгрузка гипотез | [stable](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/stable/hypotheses) <br> [testing](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/poi/flats/testing/hypotheses) |
| Робот | [robot-flats-export](https://staff.yandex-team.ru/robot-flats-export) |
| Изначальная варка квартирных интервалов | [flat_ranges](https://a.yandex-team.ru/arc/trunk/arcadia/maps/poi/flat_ranges) |
| Аналитика | [График варки гипотез](https://datalens.yandex-team.ru/u5dphv7qku7ko-flat-ranges?tab=ko) <br> [Отчеты на стате](https://stat.yandex-team.ru/Maps.Wiki/Flats) <br> [Графики разбора гипотез](https://datalens.yandex-team.ru/81wamx0ohpua1-nmaps-feedback-dashboard) |

#### Something broken?

Contact ([or create a ticket](https://st.yandex-team.ru/createTicket?queue=GEOQ)) [GEOQ](https://staff.yandex-team.ru/departments/yandex_content_geodev_3808/) ([Slack helpline channel](https://yndx-all.slack.com/archives/C01RN8Z27MX)).

### Гипотезы
Будем говорить, что квартирный интервал точный, когда у него `is_exact` == True.  
Будем говорить, что подъезд точно размечен, когда у него есть хотя бы один точный
квартирный интервал.

1. **geoq-flats-exact-entrance** - ищем дома с точно размеченными подъездами. Если
в таких домах есть подъезды, в которых нет точно размеченных квартирных интервалов,
то мы генерируем в таких подъездах гипотезу на доразметку. В целом, эта гипотеза
основана на том, что достаточно часто попадаются типовые панельные дома, где один
подъезд точно размечен, а остальные подъезды нет - и их должно быть можно доразметить.
2. **geoq-flats-entrance-coverage** - ищем дома, где квартирные интервалы из заказов
покрывают больше, чем 80% всего дома. Считаем, что пропуски при таком покрытии можно
дозаполнить, и полностью разметить дом.
3. **geoq-flats-similar-building** - ищем такие дома, которые похожи на дома, в которых
есть точно размеченные подъезды. Дома сравниваются по количеству подъездов, количеству
этажей и форме самого дома (`shape` из ymapsdf). Предлагается скопировать разметку
у похожего дома.

## Технические детали
Пайплайн разделен на два бинарника - `prepare` и `upload`.  
Сначала с помощью `prepare` подготавливаются все нужные гипотезы, а потом
финальная обработка и заливка гипотез в Народные Карты происходит уже в `upload`.

### Зачем нужна папка yql_udf и как вообще запустить пайплайн
В пайплайне используется nile-over-yql. Он работает гораздо быстрее nile-over-yt,
однако есть парочка ньюансов.

Запускать пайплайн надо так:
```sh
cd ~/arc/arcadia/maps/geoq/hypotheses/flats
ya make -r
# Prepare
NILE_YQL_PYTHON_UDF_PATH=yql_udf/libflats-yql_udf.so YT_TOKEN=$(cat ~/.yt/token) YQL_TOKEN=$(cat ~/.yql/token) bin/prepare/prepare --output-table //home/maps/users/kremius/flats/hypotheses/similar_building_example similar-building
NILE_YQL_PYTHON_UDF_PATH=yql_udf/libflats-yql_udf.so YT_TOKEN=$(cat ~/.yt/token) YQL_TOKEN=$(cat ~/.yql/token) bin/prepare/prepare --output-table //home/maps/users/kremius/flats/hypotheses/exact_entrance_example exact-entrance
# Upload
NILE_YQL_PYTHON_UDF_PATH=yql_udf/libflats-yql_udf.so ENVIRONMENT_NAME=testing TVM_SECRET=$(cat ~/.tvm/flats) YT_TOKEN=$(cat ~/.yt/token) YQL_TOKEN=$(cat ~/.yql/token) bin/upload/upload --hypotheses-tables //home/maps/users/kremius/flats/hypotheses/similar_building_example //home/maps/users/kremius/flats/hypotheses/exact_entrance_example
```

Исполнение сложного кода (например, редьюсеров или мапперов) на YQL требует
передачи на бэкэнд YQL специальным образом скомпилированного кода - yql udf.
Поэтому надо дополнительно собрать из либы yql udf и добавить путь в специальную
переменную окружения - тогда локально будет запускаться бинарь, а уезжать на
YQL редьюсится будет отдельная so-шка.

Подробнее:  
https://logos.yandex-team.ru/statbox/nile/manual_detailed.html#nile.api.v1.environment.Environment.yql_python_udf_path  
https://st.yandex-team.ru/STATLIBS-1884

### Фильтрация по панорамам и зеркалам
В бинаре `upload` так же происходит фильтрация гипотез по панорамам и зеркалам.  
Все гипотезы с помощью [footage_filter](https://a.yandex-team.ru/arc/trunk/arcadia/maps/geoq/hypotheses/flats/lib/footage_filter.py)
фильтруются по наличию рядом [Панорамы](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/streetview/release/stable/description)
(30 метров) или [Зеркала](https://yt.yandex-team.ru/hahn/navigation?offsetMode=key&path=//home/maps/core/nmaps/dynamic/replica/mrc/signals_feature)
(15 метров).

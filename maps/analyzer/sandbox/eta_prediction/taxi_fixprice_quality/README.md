Оценка качества fixprice для taxi
---

Регулярный процесс оценки качества fixprice. Для этого используются данные о заказах, логи маршрутизатора и треки (эталонные travel-times).

### Результаты

* [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/taxi-fixprice-quality)
* [Тестинг](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/testing/taxi-fixprice-quality)

Метрики хранятся вечно, на графики выводятся с помощью датасета на диапазоне таблиц.
Также хранятся архивные метрики со старого статбокса (и добавлены в датасет через линк в директорию с метриками (*)):
* [Продакшн](https://yt.yandex-team.ru/hahn/navigation?path=//home/maps/jams/production/taxi-fixprice-quality/archive/metrics)

### Ссылки

* [Панель на дашборде](https://datalens.yandex-team.ru/5q70qk3wf8ww2-probki?tab=X1Z)

### Эксперименты на инфраструктуре такси

Чтобы запустить эксперимент, нужно обратиться к [команде разработки моделей ценообразования](https://staff.yandex-team.ru/departments/yandex_distproducts_browserdev_mobile_taxi_9720_2944_9770_dep40374/)

[Договорились](https://st.yandex-team.ru/MAPSJAMS-4254), что делаем это следующим образом:
1) Мы сообщаем команде прайсинга экспериментальный параметр и выбираем некоторый фэйковый контрольный (нужно это для того, чтобы иметь возможность отличать контрольную выборку).
2) Они запускают AB эксперимент на своей стороне и сами считают качество
3) Параллельно мы можем посчитать свое качество поджойнившись с их таблицами

* [Логи](https://yt.yandex-team.ru/hahn/navigation?path=//home/logfeller/logs/taxi-pricing-data-preparer-yandex-taxi-v2-prepare-route-json-log/1d) с `route_id` (там это `uuid`)
* [Логи](https://yt.yandex-team.ru/hahn/navigation?sort=asc-false,field-name&path=//home/logfeller/logs/taxi/production/taxi-lib-client-routing-router-queries-log/1d) с настройками запроса (колонка `router_settings`)

[Пример](https://yql.yandex-team.ru/Operations/Yl1rC65OD3WOizeEquoSu74HHIsdmOrjIiXQY4CE5vw=) запроса, как можно поджойнить таблицы

##### Сноски

(*) Даталенс не позволяет добавлять много разных источников без образования связей между ними, а источник на базе SQL не позволяет сделать `union all` разносхемным таблицам. Потому источник один - диапазон, в который ссылкой добавляется архив.

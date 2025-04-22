# Static Maps API

Static API позволяет получить изображение нужного фрагмента карты в ответ на HTTPS-запрос, разместить его на сайте или в приложении. Параметрами URL задается центр и размер карты, отмечаются нужные объекты, отображаются пробки. Пример:

[![](sample.png "Пример запроса к API (clickable)")](https://static-maps.yandex.ru/1.x/?l=map&z=17&pt=37.588264,55.733862,placemark&size=600,240&api_key=66e592f8-5b03-11eb-ae93-0242ac130002&signature=9Da7Wmlj8bTGr-lRSK34s8YA6vr2LxVNJqnLbFPczhM=)


## Как получить доступ к API { #quickstart }

Чтобы в яндексовом проекте использовать API статических карт, нужно
- посчитать какая предполагается нагрузка с какими размерами картинки (подробней см. [квоты](quotas.md)),
- обратиться к [команде сервиса]({{ contacts_url }}), мы сделаем вам [ключи API](credentials.md) для прода и тестинга и настроим для них квоту.

Для внешних пользователей см. [{#T}](external_usage.md).

{% note info %}

Использование API без ключа устарело. Для анонимных запросов введена общая квота, которая будет постепенно уменьшаться в пользу индивидуальных квот.

{% endnote %}


## Где найти описание API { #api }

Публичная документация с описанием API и примерами запросов доступна по ссылкам
* на русском: <https://yandex.ru/dev/maps/staticapi/>
* in English: <https://yandex.com/dev/maps/staticapi/>

Список параметров и примеры есть на [wiki](https://wiki.yandex-team.ru/maps/dev/core/printer/).


## Контакты { #contacts }

* Команда разработки в ABC: [maps-core-renderer-staticapi](https://abc.yandex-team.ru/services/maps-core-renderer-staticapi)
* Очередь в Трекере: [MAPSPRINTER](https://st.yandex-team.ru/MAPSPRINTER)

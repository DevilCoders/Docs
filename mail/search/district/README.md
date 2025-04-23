# Поиск по Яндекс.Район
* Чатик district-search-support - линка нет, просите Влада @tabolin / Олега @generatorfive
### Прод
* стенд https://local.yandex.ru, https://local.yandex.ru/search/moscow/events?request=hello
* балансер поиска https://district-proxy-prod.search.yandex.net
* балансер индексации https://district-producer-prod.search.yandex.net
#### Cервисы в няне:
* Индексатор + Продюсер [district_search_producer_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_producer_prod/)
* Прокся [district_search_proxy_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_proxy_prod/)
* Бекенд [district_search_backend_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_backend_prod/)
* Бекенд куда переезжаем [district_search_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_prod/)
* Очередь [district_search_queue_prod](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_queue_prod/)

#### Графики и логи
* [Прокси/общая панель](https://yasm.yandex-team.ru/panel/vonidu.district-search-prod/)
* [Бекенд](https://yasm.yandex-team.ru/template/panel/ps_search_backend/prj=district-search;ctype=prod,prestable/)
* [Панель алертов](https://yasm.yandex-team.ru/template/panel/pssearch_service_alert_template/abc=pssearch;prj=district-search/)

### Тест
* стенд https://test.local.yandex.ru, https://test.local.yandex.ru/search/moscow/events?request=asdas
* балансер https://district-proxy-test.search.yandex.net
#### Cервисы в няне:
* Индексатор + Продюсер [district_search_producer_test](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_producer_test/)
* Прокся [district_search_proxy_test](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_proxy_test/)
* Бекенд [district_search_backend_test](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_backend_test/)
* Очередь [district_search_queue_test](https://nanny.yandex-team.ru/ui/#/services/catalog/district_search_queue_test/)

#### Графики и логи
* [Прокси/общая панель](https://yasm.yandex-team.ru/panel/vonidu.district-search-test/)
* [Бекенд](https://yasm.yandex-team.ru/template/panel/ps_search_backend/prj=district-search;ctype=test/)
* [Панель алертов](https://yasm.yandex-team.ru/template/panel/pssearch_service_alert_template/abc=pssearch;prj=district-search/)

## Описание
Индексируем посты и комментарии для сервиса Яндекс.Район. Поставка данных происходит через вызов ручки у нас `/api/index` в продюсере-индексаторе. Дергает ручку сервис. 
Документы конвертируются 1 в 1, т.е каждый комментарий - 1 документ в индексе. 1 пост - 1 документ в индексе. Префикс - id города. Рядом лежит старый индекс с старым префиксованием по id района, он не используется

## Памятка дежурному
* То что очередь district_change_log - большая не обращай внимания, это старый индекс. district_city_change_log - важная очередь
* Проверь жива ли очередь
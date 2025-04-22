# Фемида

- [Тестинг](https://femida.test.yandex-team.ru)
- [Продакшн](https://femida.yandex-team.ru)

Какие стенды Фемиды использовать для КП, прописано тут: [тестинг](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/backends/JOBS/FEMIDA_TEST_EXTERNAL.json) и [продакшн](https://a.yandex-team.ru/arc/trunk/arcadia/apphost/conf/backends/JOBS/FEMIDA_PROD.json).

### Добавление публикаций для тестирования

Добавлять публикации в тестинг Фемиды можно через [админку](https://femida.test.yandex-team.ru/admin/publications/publication/). Для того, чтобы пользоваться админкой, [попросите бэкенд Фемиды](#kudapisatkogozvat) выдать вам нужные права.

### Ручки Фемиды для КП

1. Ручка списка вакансий: `https://hamster.yandex.ru/jobs/api/publications`.

   Доступные queryparams:
   - page_size
   - page
   - locations
   - cities
   - professions
   - levels

2. Ручка фильтров `https://hamster.yandex.ru/jobs/api/publications/_filter_form/`
3. Ручка городов `https://hamster.yandex.ru/jobs/api/cities/`
4. Ручка города `https://hamster.yandex.ru/jobs/api/cities/<slug>`
5. Ручка сервисов `https://hamster.yandex.ru/jobs/api/services/`
6. Ручка сервиса `https://hamster.yandex.ru/jobs/api/services/<slug>`
7. Ручка профессий `https://hamster.yandex.ru/jobs/api/professions/`
8. Ручка профессии `https://hamster.yandex.ru/jobs/api/profession/<slug>`

### Как сходить в ручку Фемиды напрямую

Чаще всего мы ходим в ручки Фемиды через нашу проксю в КП: `https://hamster.yandex.ru/jobs/api/<ручка>`.
Но иногда есть необходимость сходить в Фемиду напрямую. Это можно сделать так: ???

Ручки Фемиды отдают нам данные по сервис-тикетам: [тестинг](https://abc.yandex-team.ru/services/vacancies/resources/?show-resource=26285359) и [продакшн](https://abc.yandex-team.ru/services/vacancies/resources/?show-resource=26152334).

Чтобы дернуть курлом или постманом ручку Фемиды, надо сделать следующее:
1) Установить ya
2) Выполнить в консоли: `ya tool tvmknife get_service_ticket client_credentials -s 2025166 -S <service ticket from above> -d 2000376`
-s - это наш tvm_id, в примере - тестовый,
-d - это destination, в примере - тестовая Фемида (данные взяты из abc-сервиса)
3) Полученную кракозябру использовать в запросе, передав ее в заголовке `X-Ya-Service-Ticket`


### Куда писать, кого звать

- Канал в слаке [`#femida`](https://yndx-search.slack.com/archives/C023856Q41G)
- Призывать группу `@femida-back`

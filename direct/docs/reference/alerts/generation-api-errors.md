# generation-api-errors

- image_search_client_getImageByText - поиск картинок по тексту
- image_search_client_getImageByTextAndDomain - поиск картинок по тексту и сайту
- search_query_recommendation_client_getSearchQueryRecommendation - подбор ключевых фраз для объявления
- rich_content_client_getUrlInfo - запрос сниппета для сайта

[Все проверки в juggler](https://juggler.yandex-team.ru/raw_events/?query=host%3Ddirect.solomon-alert.java-web%26(service%3Dimage_search_client_getImageByText%7Cservice%3Dimage_search_client_getImageByTextAndDomain%7Cservice%3Drich_content_client_getUrlInfo%7Cservice%3Dsearch_query_recommendation_client_getSearchQueryRecommendation)).
<br>[Проверка в solomon](https://solomon.yandex-team.ru/admin/projects/direct/alerts/generation-api-errors)

## Описание { #description }
Превышена доля ошибок на запросах в смежные сервисы, которые используются для генерации рекомендаций заполнения рекламных объявлений в UC.

## Диагностика { #diagnostics }
Запросы и ошибки ручек видно на [графике в соломоне](https://nda.ya.ru/t/jqQoqAz13uGqy6).
<br>Конкретные ошибки можно смотреть в logviewer в зависимости от запрашиваемого сервиса так:
- [image_search_client](https://nda.ya.ru/t/V2a3AFlE4tQQgG)
- [search_query_recommendation_client](https://nda.ya.ru/t/OM3N_Ebo4tQQhw)
- [rich_content_client](https://nda.ya.ru/t/TYcV3mFa4tQRAY)

Про ошибки rich_content_client

## Решение { #solution }
Ошибки rich_content_client можно сдавать в [Telegram чат RcaSupport
](https://t.me/joinchat/DdwBiVWsDFEn4Ih_TNn47w)
<br>Ошибки image_search_client можно сдавать в [Telegram чат Yandex Images DevOps
](https://t.me/joinchat/AAAAAEDjhLwxZPvwn29CIw)
<br>С ошибками search_query_recommendation_client пока что разбираемся в [тикете](https://st.yandex-team.ru/DIRECT-142349).

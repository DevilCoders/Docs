# Трассировка

Для трасировки запросов используем Jaeger.
Инициализируется в [мидлваре](https://github.com/YandexClassifieds/internal-frontend/blob/master/internal-core/server/middlewares/tracing.js).

### Как посмотреть трейс?
1. Перейти на https://jaeger.vertis.yandex.net/search (или https://jaeger.test.vertis.yandex.net/search, если речь о тестинге)
2. Ввести в поле ввода в шапке id трейса и нажать enter.

id трейса при этом можно взять из заголовка `x-request-id` ответа ajax-запроса (этот хедер есть в ответе любого запроса в наши сервисы, проставляется балансером). Для этого можно использовать dev-tools браузера.


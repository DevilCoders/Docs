# мидлвары
см. [что такое мидлвара](https://expressjs.com/ru/guide/using-middleware.html)

## base-page-html
Основа SPA приложений, статическая страница с кодом инициализации react-приложения, а также инициализация window._store. Мы испольузуем это хранилище для передачи контекста запроса и сокращения времени инициализации (preinit configs)

## check-permission
Проверка наличия разрешений на запрос. Передаем в конструктор ключ роли, текущий пользователь берем из req.user
> КАЖДЫЙ эндпоинт наших nodejs приложений обязан быть покрыт check на роли. Если ручка не покрыта check, то на это должна быть причина, описанная рядом с обьявлением ручки.

## logger
Инициализация pino-logger-express. Каждый запрос логгируется, каждый важный шаг - логируем самостоятельно импортируя `internal-core/server/logger`

## metrics
Инициализация Prometheus и сбор RED метрик

## tracing
Инициализируем Jaeger. Обогащает `req.tracer` и `req.tracer.startChildSpanByReq`. Уже в контроллерах или ресурсах регистрируем спаны.

## user
При каждом запросе делает запрос к [getUser](https://github.com/YandexClassifieds/internal-frontend/blob/ead4df0698da85bd3fdef98b869b6393c983d9ea/idm-api/lib/controller.js#L63). Обогащает req.user.

## x-request-id
Обогащает `req.xRequestId` и устанавливает полученный нами (от nginx) заголовок в список заголовков ответа.

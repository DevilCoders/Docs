# Общий серверный код

* [constants](./constants) Серверные константы
* [middlewares](./middlewares) Мидлвары
* [resources](./resources) Ресурсы

## base-resource
Базовый ресурс: логирует запросы, регистрирует трейсы, инициализирует запрос (обогащает конфигами) 

## logger
Возвращает инстанс pino-logger. Импортируем и в важных местах делаем logger.<level>(...) =)

## metrics-app
express приложение, которое на отдельном порту возвращает `/metrics` с Prometheus health сервиса и `/ping`

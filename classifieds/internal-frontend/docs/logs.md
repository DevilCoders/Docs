# Логи

Для просмотров логов используем Графану: https://docs.yandex-team.ru/classifieds-infra/logs/grafana

Для логирования используем pino. Форматируем в особом формате админском формате. Для разработки, дополнительно форматируем вывод с помощью pino-pretty.

На уровне кода логгер обьявляем тут:
https://github.com/YandexClassifieds/internal-frontend/blob/master/internal-core/server/logger.js

Мидлвара, для дефолтного вывода логов при запросах
https://github.com/YandexClassifieds/internal-frontend/blob/master/internal-core/server/middlewares/logger.js

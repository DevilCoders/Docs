# promo-safety-2017


## Начало работы
1. Ставим зависимости ``npm ci``
2. Запускаем magicdev ``npm run magic``

## Доступные команды
``npm start`` запуск приложения на localhost

``npm run magic`` запуск приложения в режиме локальной разработки (см. magicdev)

``npm run build`` сборка проекта в production режиме (``NODE_ENV=production``)

> Powered by [Reactive-Stub](https://github.yandex-team.ru/reactive-stub/generator-reactive-stub) v1.3.1 and unicorns

## Как выкатить в продакшен
* [Cборка релиза](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fsafety&id=release)

6. Следить за джобой `Deploy`; когда она успешно выполнится, убедиться, что новая версия выкатилась в [тестовое окружение](https://platform.yandex-team.ru/projects/webmaster/safety-l7-www/test)
7. Смерджить пулреквест.
8. Убедиться, что в [тестинге](https://l7test.yandex.ru/safety/) ничего не развалилось.
9. Обновить компонент `frontend` в [продакшен-окружении](https://platform.yandex-team.ru/projects/webmaster/safety-l7-www/prod)
10. Убедиться, что и в проде ничего не развалилось, можно тут: https://yandex.ru/safety/

# Промо Яндекс.ОФД

https://ofd.yandex.ru

## Начало работы


1. Переходим в servises/ofd-promo и ставим зависимости ``npm ci``
2. Устанавливаем переменные окружения:

   `export SECRET_KEY_SALT=abc`

3. Запускаем magicdev. Проект будет доступен на localhost.msup.yandex.ru 

    ``npm run magic``
    
4. Статический контент хранится в проекте [Бункера](https://bunker.yandex-team.ru/promo-ofd-2018)
5. Сборка релиза в таске сандбокса [METRIKA_FRONTEND_RELEASE](https://sandbox.yandex-team.ru/task/463989697/view), параметры Сервис: ofd-promo, Новый релиз: true
6. Проект находится в deploy: [тестовое окружение](https://deploy.yandex-team.ru/stages/ofd-promo-testing) и [прод окружение](https://deploy.yandex-team.ru/stages/ofd-promo-production)

## Доступные команды
``npm start`` запуск приложения на localhost

``npm run magic`` запуск приложения в режиме локальной разработки (см. magicdev)

``npm run build`` сборка проекта в production режиме (``NODE_ENV=production``)

> Powered by [Reactive-Stub](https://github.yandex-team.ru/reactive-stub/generator-reactive-stub) v1.8.1 and unicorns

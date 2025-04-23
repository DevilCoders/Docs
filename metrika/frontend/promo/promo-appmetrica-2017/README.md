# promo-appmetrica-2017

## Начало работы
1. Ставим зависимости ``npm install -g --registry=http://npm.yandex-team.ru``
2. Добавляем tvmSecret в `.tvm.json`
2. Запускаем magicdev ``npm run magic``

## Секреты для локальной разработки
Для старта разработки необходимо cкопировать файл `.tvm-example.json` под именем `.tvm.json`. Вставить в поле секрет tvmSecret из [секретницы](https://yav.yandex-team.ru/secret/sec-01dd1dkjqp2adk1zfvtw6gdk92/explore/version/ver-01eb1ep9ctfpfgwvwgrsmmnje1)

## Доступные команды
``npm start`` запуск приложения на localhost

``npm run magic`` запуск приложения в режиме локальной разработки (см. magicdev)

``npm run build`` сборка проекта в production режиме (``NODE_ENV=production``)

> Powered by [Reactive-Stub](https://github.yandex-team.ru/reactive-stub/generator-reactive-stub) v1.1.1 and unicorns

## Выкладка в прод
- Идём в [deploy](https://deploy.yandex-team.ru/stages/metrika-frontend-promos/config/du-appmetrica/box-appmetrica) и смотрим текущую версию, используемого докер образа.
- Клонируем и запускаем [таску сборки образа](https://sandbox.yandex-team.ru/task/1285780304/view), в двух местах подставляя версию, инкрементную проду.
- Клонируем и запускаем [таску загрузки статики](https://sandbox.yandex-team.ru/task/1285787674/view), указав ту же самую версию что и в прошлой таске.
- Идём в [deploy](https://deploy.yandex-team.ru/stages/metrika-frontend-promos/config/du-appmetrica/box-appmetrica), редактируем конфиг указав новую версию.



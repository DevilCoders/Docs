# vh-validation
Скрипты для проверки ответов от ручек vh.
Испольуются в периодических проверках в тимсити

* https://teamcity.yandex-team.ru/viewType.html?buildTypeId=PortalMorda_VhValidation
* https://teamcity.yandex-team.ru/viewType.html?buildTypeId=PortalMorda_VhSchemaValidation

Дергают ручки channels, episodes.json и vod-libraries.json, проверяют, что
* Формат ответа каждой ручки соответствует соответствующей json схеме
* Каналы есть
* У каждого канала с флагом has_vod есть vod библиотеки
* У каждого канала с флагом has_schedule есть расписание
* Передачи в расписании без дырок и пересечений покрывают запрощенный временной интервал

## Подготовка

0. Установить nodejs-6
1. Установить зависимости `npm install --registry http://npm.yandex-team.ru`

## Запуск

* Проверка на соответствие json схемам

  `./node_modules/.bin/mocha validate-schema.js --reporter dots --delay [--host ...] [--shift ...] [--window ...]`

* Проверка корректности данных

  `./node_modules/.bin/mocha validate.js --reporter dots --delay [--host ...] [--shift ...] [--window ...]`

`--host` Хост видеохостинга. По-умолчанию https://frontend.vh.yandex.ru

`--shift` Время в секундах от текущего момента до начала запрашиваемого интервала. По-умолчанию 12 часов.

`--window` Длительность интервала в секундах. По-умолчанию 24 часа.

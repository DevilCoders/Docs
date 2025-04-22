# CTRBlocks

> CTRBlocks это расширение для Chromium браузеров, которое позволяет просматривать статистику по блокам аналитики в интерфейсе Яндекс.Карт

## Установка CTRBlocks

1.  Скачайте [Расширение](https://sandbox.yandex-team.ru/resources?any_attr=false&limit=20&attrs=%7B%22ext%22%3A%22ctrblocks%22%7D)
2.  Откройте страницу `browser://tune` в Яндекс.Браузере
3.  Перетащите туда `ctrblocks.crx`

Расширение ходит за данными в [https://stat.yandex-team.ru/Maps/Adhoc/CTRBlocks](https://stat.yandex-team.ru/Maps/Adhoc/CTRBlocks), поэтому убедитесь, что у вас есть туда доступ и вы залогинены во внутреннем паспорте.

## Установка devtool расширения

1.  Скачайте [Расширение](https://sandbox.yandex-team.ru/resources?any_attr=false&limit=20&attrs=%7B%22ext%22%3A%22devtool%22%7D)
2.  Откройте страницу `browser://tune` в Яндекс.Браузере
3.  Перетащите туда `devtool.crx`

## Как пользоваться

- После установки расширения в правом верхнем углу на сайте карт у вас появится кружок расширения. Если он красный, значит страница загружена без параметра loggers=analytics, нажмите на него, чтобы перейти на страницу с включенным параметром
- Когда кружок загрузился синим, значит все хорошо и расширение работает
- **Зажмите ctrl/cmd и наведите на элемент** для которого вы хотите посмотреть статистику
- Данные появятся в правом верхнем углу
- Если расширение вам мешает смотреть на карту, его можно свернуть, нажав на крестик. После того как вы свернете расширение оно не раскроется назад пока вы не нажмете на кружок чтобы открыть его опять (или пока не обновите страницу).

## Wiki

[https://wiki.yandex-team.ru/maps/analytics/web/CTRBlocks/](https://wiki.yandex-team.ru/maps/analytics/web/CTRBlocks/)

## Разработка

1. `npm i`
2. `npm run watch`
3. идете на страницу `browser://extensions`, включаете режим разработчика и загружаете распакованное расширение из папки `ctrblocks-ext/dist`
4. открываете страницу карт и все работает

В дев режиме работает livereload расширения

## Production

1. `npm run build`
2. `browser://extensions` -> упаковать расширение
3. положите его в папку [ext/](ext/)
4. `arc push`

## Ссылка на секрет

[https://yav.yandex-team.ru/secret/sec-01fmmnnwe4qdyjmw5nwp7zbep6](https://yav.yandex-team.ru/secret/sec-01fmmnnwe4qdyjmw5nwp7zbep6)

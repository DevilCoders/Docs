## Fast smoke tests

**Старт**

1. `npm install`
2. Положить токены в файл `.token.json`. Скачать можно [здесь](https://yav.yandex-team.ru/secret/sec-01ep45wv8pkmb935bn6shbksb5/explore/versions)
3. `npm run test:{service}`

#####scripts:

1. `npm run test:{service}` - запускает тесты для указанного сервиса
2. `npm run saveref:{service}` - выкачивает новые референсы
3. `npm run approve:{service}` - сохраняет новые референсы

По-умолчанию тесты смотрят на unstable окружение, можно натравить на testing окружение. Например `npm run test:go:testing`

**Если вылезает куча модалок:**, отключаем в настройках безоспасности firewall



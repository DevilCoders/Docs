## Usage

1. ```npm run init```

**Запуск тестов КК**
1. В env записать токен для получения авторизационных данных пользователей:
    * Запросить доступ к секрету https://yav.yandex-team.ru/secret/sec-01ew058w0t6d5ycykyj2k78773/explore/versions
    * token получить тут https://oauth.yandex-team.ru/authorize?response_type=token&client_id=ce68fbebc76c4ffda974049083729982
    * Записать в env командой```export YAV_TOKEN=token```
```
cd packages/corp-client
npx cypress open
```
**Запуск тестов логистики**
1. Для запуска в env записать [tus](https://wiki.yandex-team.ru/test-user-service/) токен для получения авторизационных данных пользователей
    * token получить тут https://oauth.yandex-team.ru/authorize?response_type=token&client_id=9052de6e4cf142039a7ee44ac03e4614
    * Записать в env командой```export TUS_TOKEN=token```
```
cd packages/logistics
npm run test

Запуск одного теста для отладки
RUNNER=debug npx wdio run wdio.conf.js --spec ./tests/order/all-resolutions/points-count.js
```

# taxi-monitoring
Скрипт для мониторинга доступности сервиса (Проверка на ответ с кодом 200)
[wiki juggler](https://wiki.yandex-team.ru/taxi-ito/NewJugglerCheck/)

https://github.yandex-team.ru/taxi/infra-cfg-juggler/tree/master/checks

**Сборка**
`npm run build:monitoring`

**Проверка**
`node libs/monitoring/build/check-taxi-frontend.js -- -service=uber`

**Важное**
Добавлять url в мониторинг только после выкатки nginx (иначе сработает мониторинг, т.к. url ещё не доступен)

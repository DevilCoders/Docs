## Прокси, соединяющий кастомные блоки пользователей и наш репозиторий

Умеет делать всего одну вещь: получать `xml` в `POST` запросе, и возвращать результирующий `html`,
с походом на фронт турбо с дополнительным cgi-параметром. `CGI`-параметр `custom-blocks-development`
не виден пользователю, потому что его добавляет прокси.

### Разработка

Запустить `PORT=<port-num> npm run start:dev`, перейти на `localhost:<port-num>`, дефолтный порт 80.

### Сборка

Продакшн сборка выполняется с помощью `npm run build`.

### Деплой

1. Обновить версию в `package.json`.
1. Собрать ts с помощью `npm run build`.
1. Собрать докер-контейнер с помощью `docker build -t registry.yandex.net/turbopages/custom-components-proxy:<version-number> .`.
1. Запушить новую версию в registy. Про это [wiki/Docker distribution](https://wiki.yandex-team.ru/qloud/docker-registry/)
1. Обновить версию в [deploy/yandex-turbo_turbo-custom-components_pro](https://deploy.yandex-team.ru/stage/yandex-turbo_turbo-custom-components_pro)

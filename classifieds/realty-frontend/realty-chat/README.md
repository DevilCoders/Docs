# Фронтенд чатов

Состоит из:
- nodejs приложение, которое отвечает на ajax запросы из верстки чатов,
- realty-chat.js и realty-chat.css - верстка чатов, заливается на S3 и загружается в браузер [через скрипт-загрузчик](app/middleware/static-loader.js)

### Установка и настройка 
Настроить nginx через ansible в realty-frontend:
```sh
cd .. # в realty-frontend

make ansible-local
```
Это должно добавить в nginx-конфиги нужные чатам строчки.

Установить зависимости
```sh
yarn
```

Скачать секреты
```sh
make secrets
```

Запустить сборку webpack
```sh
make webpack
```

Запустить nodejs (Разработка локально)
```sh
make start-local # или start-local-debug, порт для дебаггинга - 9230
```

### Детали подключения к фронтенду недвижимости:

Настройка nginx: см. [ansible в realty-frontend](../ansible/roles/dev-local/templates/include/locations-chat.j2)

Подключение лоадерa:  см. [подключение скрипта в realty-frontend](../realty-core/view/react/libs/chat/initialize.ts)

Также, для работы с чатами сервис устанавливает куку `_csrf_token`: см. [тут](../realty-core/app/lib/middleware/csrf-protection.js)

## Основная информация

| Service | URL                                                                                                            |
|---|----------------------------------------------------------------------------------------------------------------|
| Arcanum CI | https://a.yandex-team.ru/projects/realty/ci/releases/timeline?dir=classifieds%2Frealty-frontend&id=realty-chat |
| Deploy | https://admin.vertis.yandex-team.ru/services/realty-front-chat                                                 |
| Grafana | https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?var-job=realty-front-chat            |

## Важно

Выкатывать нужно в тестинг. Бранчи не работают, сборка чатов одна на все бранчи и общий тестинг `realty-frontend`.

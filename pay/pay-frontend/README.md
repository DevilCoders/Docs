# Yandex.Pay

## Быстрый старт
### Окружение
Для разработки:
* Node 12.x (LTS)
* NPM 7.x

Для релизов:
* Docker 20.x

### Подготовка
1. Установить [yav](https://vault-api.passport.yandex.net/docs/#cli) \
   _Ставить лучше через `pip3`_ \
   _Может потребоваться отдельно поставить `pip3 install cryptography`_
2. Установить [Hivemind](https://github.com/DarthSim/hivemind) или [Overmind](https://github.com/DarthSim/overmind)
3. Скачать dev-сертификат\
   `cd tools/local && . copy-cert.sh`
4. Подготовить локальную dev-середу\
   `cd tools/local && . prepare-dev.sh`
5. Обновить `/ect/hosts`\
   `127.0.0.1	pay.local.yandex.ru`
6. Установить [tvmtool](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/#iznpm)\
   `npm install -g tvmtool-bin --registry=http://npm.yandex-team.ru/`
7. Установить [devkit](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/devkit) для тунеллера\
   `npm install -g @yandex-int/devkit --registry=http://npm.yandex-team.ru/`
8. Завести собственный `merchant-id`
   1. Запросить собственный `merchant-id` у [дежурного бэкенда](https://abc.yandex-team.ru/services/swat-finsrv/duty/?role=3098) для локальной разработки.\
      Бэк должен завести мерчанта для адреса `https://<username>-8080-ws2.tunneler-si.yandex.ru/web/api/playground/v1/order/render`
   2. Добавить полученный `merchant-id` в `playground`\
      `services/playground/src/config => BOLT_MERCHANTS['https://pay.local.yandex.ru:3010']`
    

### Локальная разработка
1. Установить все зависимости — `npm run deps`
2. Установить pre-commit hooks — `npm run husky` \
_Нужно сделать только один раз._

Локальный стенд поднимается по адресу [https://pay.local.yandex.ru:3010/web/playground/](https://pay.local.yandex.ru:3010/web/playground/)

`hivemind` — запускает Classic форму \
`hivemind Procfile.checkout` — запускает Checkout форму

_Разработка требует залогина в тестовом Паспорте — [https://passport-test.yandex.ru/](https://passport-test.yandex.ru/)._


## Структура проекта
- `_config` — скрипты для сборки статики и локальной разработки
- `packages` — общие пакеты
- `server` — Duffman-сервер
- `services/playground` — Стенд для разработки и отладки Yandex Pay (эмулирует работу Мерчанта)
- `services/pay-form` — Страница с формой Yandex Pay
- `services/checkout` — Страница с чекаутом Yandex Pay
- `services/sdk` — SDK для подключения Yandex Pay
- `tools` — Скрипты для CI/CD


## Yandex.Deploy

Фронтбэк развернут [тут](https://deploy.yandex-team.ru/stage/yandex-pay).
Пока нет балансеров, можно смотреть по FQDN конкретного Пода.


## Деплой

Делается через отдельный репозиторий — [trust/ci-frontend](https://github.yandex-team.ru/trust/ci-frontend#таски)


## Документация

* [Интеграция](https://wiki.yandex-team.ru/yandexpay/public-docs/web-api/tutorial/)
* [Мониторинги](./docs/monitoring.md)
* [Логи](./docs/logs.md)
* [WebAPI](./docs/web-api.md)
* [MobileAPI](./docs/mobile-api.md)

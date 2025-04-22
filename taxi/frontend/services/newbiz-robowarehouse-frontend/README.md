# Фронтенд сервиса Робосклад

Интерфейс работы с Робоскладом

## Хосты

[Сервис в Tariff Editor](https://tariff-editor.taxi.yandex-team.ru/services/151/edit/356028/info)

* NGINX
    * [newbiz-robowarehouse-frontend](/services/newbiz-robowarehouse-frontend/docker/etc/nginx/sites-available/newbiz-robowarehouse-frontend.conf)
* unstable - Отсутствует
* testing - [nanny](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_robowarehouse-frontend_testing/)
* pre-stable - [nanny](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_robowarehouse-frontend_pre_stable/)
* stable - [nanny](https://nanny.yandex-team.ru/ui/#/services/catalog/taxi_robowarehouse-frontend_stable/)
* телеграм-бот - [тестинг](https://t.me/oxfygtixmv_bot) / [прод](https://t.me/RobowarehouseBot)

PS. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Установка и разработка

* ставим nodejs 14 через nvm
* `cd services/newbiz-robowarehouse-frontend/` - переходим в папку с проектом
* `npm i` - ставим зависимости
* Заказываем личный серификат через [Сертификатор](https://crt.yandex-team.ru/certificates?cr-form=1)
    * **CA name** - InternalCA
    * **Certificate type** - For web-сервера
    * **Hosts** - *.localhost.yandex.net
    * **ABC service** - Робосклад
* Скачиваем сертифкат и разделяем на два:
    * `server.key` - все что в блоке

      ```plain
      -----BEGIN PRIVATE KEY-----
      ...
      -----END PRIVATE KEY-----
      ```

    * `server.crt` - все остальное
* Кладем оба файла сертификата в `services/newbiz-robowarehouse-frontend/dev`
* Скачать в секретнице [.tvm.json](https://yav.yandex-team.ru/secret/sec-01fnecwbk2vmck2k4e8ws1n13h/explore/versions) и положить в корень проекта `services/newbiz-robowarehouse-frontdev/dev`
* В файле `/etc/hosts` добавляем строки

  ```plain
  127.0.0.1  robowarehouse-frontend.localhost.yandex.net
  127.0.0.1  robowarehouse-frontend.localhost.yandex.ru
  ```

* `npm run dev`
* В браузере переходим на [локальный хост](https://robowarehouse-frontend.localhost.yandex.net:3000/)
* для разработки бота нужно создать своего бота через [@BotFather](https://t.me/BotFather) и положить его токен в файл `.env`

## Сборка

* `npm run build:{ENV}` — ENV: stable | testing | unstable

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

Global Market B2C API

# Install [WIP]

1. [Начальная настройка](https://a.yandex-team.ru/arc_vcs/market/front/monomarket/wiki/start.md)
2. Идём в https://crt.yandex-team.ru/certificates. Жмём "Заказать сертификат". Во всплывающем окне
указываем:
  * CA name - InternalCA
  * Тип сертификата - Для web-сервера 
  * Хосты - *.local.yandex.com
  * ABC-сервис - Международный Маркет

  Сохраняем файл как `.dev/cert.pem`
3. `cp .dev/.env.example .dev/.env` и вставляем [TVM_SECRET, ELASTIC_SEARCH_PASSWORD, TRUST_CLIENT_SERVICE_TOKEN](https://yav.yandex-team.ru/secret/sec-01ff3cgxs8yd28z0v42aqbqd64)

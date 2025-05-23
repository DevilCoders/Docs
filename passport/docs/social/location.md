# Хосты Социализма

В каждом домене, в котором доступен Паспорт, поддерживаются несколько экземпляров Социализма. Экземпляры различаются тем, какие базы данных Паспорта и Социализма используются.

Все перечисленные хосты поддерживают как IPv4-, так и IPv6-соединения. Брокер, Прокси и Хранилище следует вызывать только по протоколу HTTPS.

[Боевой Социализм](#production)

[Релиз-кандидат Социализма](#production_1)

[Тестовый Социализм](#production_2)

## Боевой Социализм {#production}

Используется боевыми серверами сервисов. Разделен на два хоста:

* `social.yandex.*` — хост внешнего API Брокера;

* `api.social.yandex.ru` — хост Прокси, Хранилища и внутреннего API Брокера.

Подключенные базы данных:

* боевая база Паспорта (принимаются авторизационные куки, выставленные для домена `passport.yandex.*` в том же национальном сегменте);

* боевая база Социализма.

## Релиз-кандидат Социализма {#production_1}

Используется для тестирования нового кода на боевых данных. Доступен по адресам `social-rc.yandex.*`.

{% include [location-db](./_includes/concepts/location/id-location/db.md) %}

* {% include [location-prod-pass](./_includes/concepts/location/id-location/prod-pass.md) %}

* {% include [location-prod-soc](./_includes/concepts/location/id-location/prod-soc.md) %}

## Тестовый Социализм {#production_2}

Используется для разработки и функционального тестирования сервисов. Доступен по адресам `social-test.yandex.*`. Разделен на два хоста:

* `social-test.yandex.*` — хост внешнего API Брокера.

* `api.social-test.yandex.ru` — хост Прокси, Хранилища и внутреннего API Брокера.

{% include [location-db](./_includes/concepts/location/id-location/db.md) %}

* тестовая база Паспорта (принимаются авторизационные куки, выставленные для домена `passport-test.yandex.*` в том же национальном сегменте);

* тестовая база Социализма.

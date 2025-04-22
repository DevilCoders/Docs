# SSL-сертификат

Для локальной разработки используем защищенный домен (`https://local.vertis.yandex-team.ru`), чтобы работали куки.
SSL-сертификат лежит в [секретнице](https://yav.yandex-team.ru/secret/sec-01fe1hk6v4h23atkp0v9c55w95/explore/versions).

Если его нужно обновить, то
- заходим в [crt](https://crt.yandex-team.ru/certificates/?cr-form=1&cr-form-type=host&cr-form-ca_name=InternalCA&cr-form-abc_service=119)
- указываем домен `local.vertis.yandex-team.ru`
- жмякаем "Заказать"
- скачиваем `.pem` сертификат и кладем его содержимое в секретницу.
  [Как работать с секретницей](https://wiki.yandex-team.ru/passport/yav-usage/).
  При этом в новой версии секрета должен быть только один ключ с названием `cert`.


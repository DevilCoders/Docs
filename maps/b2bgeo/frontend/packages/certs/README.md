### @b2bgeo/certs

Certs for local dev

#### How to generate certs

1. [Заказываем сертификат](https://crt.yandex-team.ru/certificates)

%%
CA name: InternalCA
Тип сертификата: Для web-сервера
Хосты: localhost.msup.yandex.com.tr, localhost.msup.yandex.com, localhost.msup.yandex.ru
ABC-сервис: yandexcourier
Желаемый TTL (в днях): 365
Common name: localhost.msup.yandex.ru
%%

[Пример](https://crt.yandex-team.ru/certificates/5009463?serial_number=7F001DEB3EC0AEC722323D816E0002001DEB3E)

2. Скачиваем сертификат `localhost.msup.yandex.ru.pem`

3. Открываем этот сертификат `localhost.msup.yandex.ru.pem`, копируем первый блок

%%
-----BEGIN PRIVATE KEY-----
<base64>
-----END PRIVATE KEY-----
%%

4. Создаем из скопированного блока отдельный файл `localhost.msup.yandex.ru.key`

## Заказ сертификата для development
* Заходим на https://golem.yandex-team.ru/certs
* Заказываем InternalCA сертификат для нужных доменов, например  *.maya.yandex.ru, *.maya.yandex.com, *.maya.yandex-team.ru
* Скачиваем в формате pfx
* Распаковываем
```
openssl pkcs12 -in <name>.pfx -nocerts -out key.pem -nodes  -passin pass:"7777777"
openssl pkcs12 -in <name>.pfx -nokeys -out maya.crt  -passin pass:"7777777"
openssl rsa -in key.pem -out maya.key
rm key.pem
```
* Кладем на машинку сертификат и ключ в  /etc/nginx/ssl
* Перезапускам nginx

## Заказ сертификата для production и intranet-production
* Заходим на https://crt.yandex-team.ru/certificates
* Заказываем CertumProductionCA для нужных доменов
* Ждем подтверждение от СИБ и письмо с сертификатом
* Скачиваем сертификат и меняем содержимое секрета [maya-public-ssl](https://platform.yandex-team.ru/secrets/secret.maya-public-ssl) или [maya-corp-ssl](https://platform.yandex-team.ru/secrets/secret.maya-corp-ssl)
* В письме будет ссылка на новый секрет в серетнице, ему нужно добавить понятное имя и описание
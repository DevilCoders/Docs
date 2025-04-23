
# Arcadia API

Библиотека для запросов в `api.arc-vcs.yandex-team.ru`.

**NOTE**: Для работы библиотеки **необходимо** указать путь к сертификату [YandexInternalRootCA.crt](https://crls.yandex.net/YandexInternalRootCA.crt), переведенному в формат pem, в `library.yaml` или через переменную окружения `CUSTOM_CA_ROOT_CERTIFICATE_PATH`. Этот сертификат должен быть доступен на машине с сервисом, куда ставится библиотека как зависимость. По-умолчанию, путь к сертификату `/etc/ssl/certs/YandexInternalRootCA.pem`, поэтому если файл на машине отсутствует нужно обратиться к админам.

Чтобы делать реальные запросы в grpc api с разработческой машины, нужно (рецепт частично взят [отсюда](https://wiki.yandex-team.ru/security/ssl/sslclientfix/#vpythonnamacosx)):
1. Скачать самоподписанный сертификат [YandexInternalRootCA.crt](https://crls.yandex.net/YandexInternalRootCA.crt) и сконвертировать его в pem:

```bash
$ openssl x509 -in YandexInternalRootCA.crt -out YandexInternalRootCA.pem -outform PEM
```

2. Положить `YandexInternalRootCA.pem` в папку `/etc/ssl/certs/YandexInternalRootCA.pem` или поменять путь к сертификату в `library.yaml`.
3. Получить свой [oauth токен](https://doc.yandex-team.ru/arc/setup/arc/install.html#oauth-token) и прописать его в `library.yaml`. 

grpc-python пока что не поддерживает работу с сертификатами, подробнее [здесь](https://www.sandtable.com/using-ssl-with-grpc-in-python/).

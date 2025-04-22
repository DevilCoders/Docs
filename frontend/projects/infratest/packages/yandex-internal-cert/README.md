# Yandex Internal Cert

[![oko health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/yandex-internal-cert)](https://oko.yandex-team.ru/pkg/@yandex-int/yandex-internal-cert)

HTTPS-сертификаты многих внутренних сервисов подписаны не публичным Certificate Authority, а [внутренним](https://wiki.yandex-team.ru/security/ssl/sslclientfix/). Если в запросах из вашего nodejs-приложения вы видите ошибку:

```
RequestError: self signed certificate in certificate chain
```

То у вас, скорее всего, как раз такой случай. Посмотрите, каким CA подписан https-сертификат сервиса, к которому вы обращаетесь. Если в цепочке сертификатов вы видите YandexRootCA или YandexInternalRootCA, то наш пакет вам поможет.


В этом пакете поставляется корневой сертификат.

## Установка

```
npm install --save-exact @yandex-int/yandex-internal-cert
```

## Использование

### Использование с нативным модулем https

```
import { getCert } from "@yandex-int/yandex-internal-cert";

https.get('https://example.yandex-team.ru', { ca: getCert() });
```

### Использование с got

```
import { getCert } from "@yandex-int/yandex-internal-cert";

got('https://example.yandex-team.ru', {
    https: {
        certificateAuthority: getCert()
    }
});
```

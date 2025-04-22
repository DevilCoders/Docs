## Цель скрипта

Скрипт пробежится по окружениям из конфига и подготовит новые версии в Qloud
с нужными обновлениями ресурсов.

Применим для web-api, u2709, quinn, mobile-api.

## Использование

Добавить пакет `@ps-int/ps-deploy` в `devDependencies`.

```bash
npm i -D @ps-int/ps-deploy
```

Добавить в `scripts`

```json
{
  "scripts": {
    "deploy": "ps-deploy"
  }
}
```

Добавить конфиг .config/ps-deploy.yaml:

```yaml
api: v1
componentName: web-api
resourceType: MAILFRONT_WEB_API
resourceLocalName: web-api.tar.gz
docker: registry.yandex.net/mail/webmail/web-api-container:202002201130 # необязательный
sandboxResources: # необязательный (будут сохранены ресурсы из предыдущей версии)
  - dynamic: false
    extract: true
    id: 801415440
    localName: tzdata.tar.gz
    symlink: /var/cache/geobase/tzdata
  - dynamic: false
    extract: false
    id: 814692441
    localName: geodata5.bin
    symlink: /var/cache/geobase/geodata5.bin
environments:
  mail.web-api.production:
    components:
      - web-api-iva
      - web-api-myt
      - web-api-sas
      - web-api-vla
    targetState: COMMITTED # необязательный, несли не указан, будет запрошен
    tvm: # необязательная секция
      secretName: mobile-api-production
      name: mobile-api
      destinations:
        aceventura: 2014088
  mail.webmail.prestable:
    components:
      - web-api
  mail.verstka-qa.ub-template:
    components:
      - web-api
```

Получить `QLOUD_OAUTH_TOKEN` https://oauth.yandex-team.ru/authorize?response_type=token&client_id=072224ad7c864b158601e49b25497eac

Запускать

```bash
QLOUD_OAUTH_TOKEN=... npm run deploy 1.2.3 TICKET-123
```

Можно использовать кастомный конфиг, например, для канарейки:

```json
{
  "scripts": {
    "deploy-canary": "ps-deploy .config/ps-deploy-canary.yaml"
  }
}
```

```bash
QLOUD_OAUTH_TOKEN=... npm run deploy-canary 1.2.3 TICKET-123
```

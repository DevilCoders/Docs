# webmail-deploy

L7 почты для деплоя.

https://yd.yandex-team.ru/projects/mail_web

```bash
make mailfront-config
# edit specs/front-app.j2, base.yaml, etc
```

## Deploy

Для релиза надо поменять в файле `specs/front-app.j2` ссылку на [ресурс конфига](https://sandbox.yandex-team.ru/resources?type=MAILFRONT_CONFIG&limit=3&attrs=%7B%22component%22%3A%22webmail%22%7D)
в формате `sbr:NNN`, собрать спеку для нужного стейджа (например `make corp`) и задеплоить её через `ya dctl ...` или `make put-<XXX>`.

Описаны стейджи `production` и `corp`.

Доступные цели в Makefile:

* `production`, `corp` — сборка соответствующих спек.
* `put-production`, `put-corp` — публикация черновик (draft).

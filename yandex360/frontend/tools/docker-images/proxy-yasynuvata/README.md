# proxy-yasynuvata

Прокси для QA-стендов почты

https://deploy.yandex-team.ru/stages/mail_proxy_yasynuvata

```bash
# build new image
make build
make deploy
```

## Что делает

Проксирует адреса вида:

* `pr-NNN.qa.mail.yandex.TLD` в деплой стейджи `mail_frontend_pr-NNN`

* `pr-NNN.qa.mail.yandex-team.ru` в деплой стейджи `mail_frontend_pr-NNN-corp`

* `ANY-LETTER-OR-NUMBER.qa.mail.yandex.TLD` в деплой стейджи `mail_frontend_ANY-LETTER-OR-NUMBER`

* `ANY-LETTER-OR-NUMBER.qa.mail.yandex-team.ru` в деплой стейджи `mail_frontend_ANY-LETTER-OR-NUMBER`


## Почему "Ясынувата"

Это такая большая сортировочная станция.

![image](https://media.github.yandex-team.ru/user/5103/files/f5eb5f00-8e6f-11ec-9031-11511083007c)


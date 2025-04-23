## Масштабировать фронтбект
 Проще всего через UI деплоя путем увеличения кол-ва подов (поле `Pods quantity`) – https://deploy.yandex-team.ru/stages/tavern_prod/edit/du-tavern . После чего новые настроки стоит зафиксировать в специфиеации [tools/specs.prod.j2](../../tools/specs/prod.j2)

## Масштабировать L7 балансеры
 - жмем на ссылку "Service ID" на балансере https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/tavern.production.mail.yandex.net/show
 - далее по инструкции https://wiki.yandex-team.ru/awacs/nanny-services/#kakdobavitpodyvbalanceer

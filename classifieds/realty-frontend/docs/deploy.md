# Деплой

Деплой состоит из 4 стадий:<br>
`Build -> Test -> [Canary] -> Prod`

Для деплоя можно использовать
- [web-ui](https://admin.vertis.yandex-team.ru/services);
- [telegram-bot](https://wiki.yandex-team.ru/vertis-admin/deploy/bot/).

[Документация админов](https://wiki.yandex-team.ru/vertis-admin/deploy/).

## Настройка telegram-bot

Даже если хочется использовать только web-ui, следует настроить telegram-bot, так как через него можно получать нотификации.

Шаги:
- поставить [@vertis_shiva_bot](https://t.me/vertis_shiva_bot);
- [подписаться](https://wiki.yandex-team.ru/vertis-admin/deploy/bot/#m-/sub) на обновления наших сервисов в `test` и `prod`, можно начать с `realty-front-desktop`, `realty-front-mobile`, `realty-front-lk`.

## Стадии

### Build

На данном этапе происходит сборка docker-образа с nodejs приложением и загрузка собранной статики на CDN.

Шаги:
- зайти в [Arcanum CI](https://a.yandex-team.ru/projects/realty/ci/);
- найти нужный джоб `Release: <project-name>` в колонке `Releases`
- нажать `Run relese`, чтобы просто собрать релиз с текущим `trunk`
или выбрать `Realty frontend deploy branch [manual]` в колонке `Actions`, чтобы собрать другую ветку.

### Test

На данном этапе происходит выкатка собранного на предыдущем этапе docker-образа в тестинг.

Если docker-образ был собран через `Run relese`, то он автоматически выкатывается в тестинг,
иначе, он автоматически выкатывается на отдельную ветку в тестинге. [Про ветки](https://docs.yandex-team.ru/classifieds-infra/deploy/specification/branch).

### Canary

Делится на два этапа - `Canary 1%` и `Canary`. Подробнее [тут](https://docs.yandex-team.ru/classifieds-infra/deploy/specification/canary).<br>
Канареечные инстансы живут только до момента перехода к стадии `Prod`.<br>

> Не у всех проектов есть эта стадия, смотри [манифест деплоя](https://docs.yandex-team.ru/classifieds-infra/service-preparation/manifest) конкретного проекта.

Шаги для telegram-bot:
- найти нотификацию о выкатке приложения в `test`, нажать кнопку `promote`.

Шаги для web-ui:
- найти приложение в [web-ui](https://admin.vertis.yandex-team.ru/services);
- найти сниппет с названием `test`;
- нажать у него кнопку `promote` (желтая кнопка).

После выкатки нужно убедиться:
- на [графиках приложения](https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?orgId=1&refresh=5s)
все хорошо, выбрав в фильтре `job` значение `<job_name>-canary`;
- на [графиках nginx](https://grafana.vertis.yandex-team.ru/d/0EUnD67Zk/realty-codes-new?orgId=1&refresh=5s) все хорошо.

### Prod

На данном этапе происходит выкатка в прод.

Шаги для telegram-bot:
- найти нотификацию о выкатке приложения в `test` или `canary`, если у приложения есть стадия `canary`, нажать кнопку `promote`.

Шаги для web-ui:
- найти приложение в [web-ui](https://admin.vertis.yandex-team.ru/services);
- найти сниппет с названием `prod` и лейблом `canary`, если у приложения есть стадия `canary`, иначе просто сниппет `test`;
- нажать у него кнопку `promote` (желтая кнопка).

После выкатки нужно убедиться:
- на [графиках приложения](https://grafana.vertis.yandex-team.ru/d/yQvo5o6iz/realty-nodejs-frontends?orgId=1&refresh=5s)
все хорошо, выбрав в фильтре `job` значение `<job_name>`.
- на [графиках nginx](https://grafana.vertis.yandex-team.ru/d/0EUnD67Zk/realty-codes-new?orgId=1&refresh=5s) все хорошо.

## На что обращать внимание на графиках

Любые изменения по сравнению с моментом до выкатки. В первую очередь на количество `4хх` и `5хх`.
Также, стоит посмотреть на графики `AskerError` и `Other events and error` на графиках приложения.

## Как откатить версию

Если что-то пошло не так, можно вернуться к предыдущей версии приложения.

Шаги для telegram-bot:
- найти нотификацию о выкатке приложения в `prod`, нажать кнопку `cancel`.

Шаги для web-ui:
- найти приложение в [web-ui](https://admin.vertis.yandex-team.ru/services);
- найти сниппет с названием `prod`;
- нажать у него кнопку `Откатить`.

## Как вручную выкатить версию в test или prod

Шаги для telegram-bot:
- узнать версию, её можно найти в [Arcanum CI](https://a.yandex-team.ru/projects/realty/ci/)
- ввести `/run -l test|prod -v <version> <app-name>`.

[Более подробно про команду run](https://docs.yandex-team.ru/classifieds-infra/deploy/integration/telegram-bot).

Шаги для web-ui:
- узнать версию, её можно найти в [Arcanum CI](https://a.yandex-team.ru/projects/realty/ci/);
- найти приложение в [web-ui](https://admin.vertis.yandex-team.ru/services);
- рядом с названием приложения нажать на кнопку с ракетой;
- в форме:
    - `layer` - выбрать `test` или `prod`;
    - `version` - вставить найденную версию в Arcanum CI;
    - `branch` - если оставить пустым, то выкатится в `test` или `prod`, если указать что-то, то выкатится на отдельную ветку, причем в `prod` эта ветка будет закрыта от реального трафика, но можно добавить 1% трафика с помощью поля `trafficShare`;
    - нажать `Запустить`.

## Как зайти на ветку в prod

Для этого нужно добавить в запрос куку `_branch=<branch-name>` или GET-параметр [_branch](./secret-pages-and-params.md#_branchbranch_name) 

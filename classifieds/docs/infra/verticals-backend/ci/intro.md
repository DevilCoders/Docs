# CI

CI в verticals-backend реализован с помощью [одноименного сервиса](https://docs.yandex-team.ru/ci/).
В корне репозитория лежит файл `a.yaml` с описанием всех задач/релизов.
Данный файл не нужно редактировать руками.
Вместо этого необходимо поправить `a_template.yaml` и вызвать команду `make gen/yaml`.

Ниже перечислены основные экшены/релизы.
Их можно найти в [интерфейсе](https://a.yandex-team.ru/projects/verticals?autoSelect=true)(рекомендуется добавить проект `Vertical Services` в избранное, чтобы не искать каждый раз заново).

## Actions

На каждый PR запускается несколько проверок:

1) [Check a.yaml consistency](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=yaml-check) – проверяет согласованность `a.yaml`, `a_template.yaml` и bazel-таргетов, влияющих на CI.

2) [Check formatting](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=format) – проверяет форматирование кода согласно конфигурации scalastyle. При падении стоит запустить команду `make format` и запушить изменения.

3) [CI Build](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=bazel-ci) – запускает сборку всех таргетов и прогоняет тесты, не отмеченные тегами `manual` и `integration`.

4) [Integration CI Build](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=bazel-integration-ci) - запускает интеграционные тесты, помеченные тегом `integration`.

Помимо этого на каждый мерж в транк вызывается экшен [Generate alerts](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=bazel-alert), который создает/удаляет изменившиеся алерты.

Призыв в PR на изменения своих файлов можно настроить через [специальные таргеты](codeowners.md).

## Releases

### Релиз из trunk'a

Чтобы выкатить из транка, нужно:
1. выбрать Release `Release: <service-name>` для shiva-сервисов и `ReleaseNomad: <service-name>` для nomad-сервисов 
2. нажать `Run release`
3. убедиться что в релиз входят нужные коммиты и повторно нажать `Run release`. Запустится CI-флоу, который соберет сервис, запакует его в Docker и выкатит в тестинг.
4. докатить до прода либо со страницы с флоу, либо стандартными средствами Shiva – через [админку](https://admin.vertis.yandex-team.ru) или [бота](https://docs.yandex-team.ru/classifieds-infra/deploy/telegram-bot).

{% note warning %}

NB: для релиза в прод сервисов под SOX есть дополнительные ограничения, которые можно изучить в [доке](https://docs.yandex-team.ru/classifieds-infra/deploy/sox).

{% endnote %}

### Релиз из ветки

#### Способ 1. Через командную строку.
1. Собрать образ
```
./scripts/build_image.sh '//general/bonsai/internal-api:image' 'registry.yandex.net/vertis/bonsai-internal-api:lyubortk-01'
```
2. Запушить в docker-registry
```
docker push registry.yandex.net/vertis/bonsai-internal-api:lyubortk-01
```
3. Запустить доставку через бота
```
/run -l test -v lyubortk-01 -b lyubortk-test bonsai-internal-api
```

#### Способ 2. Через Arcanum.
Чтобы выкатить из ветки, нужно:
1. выбрать Action [Manual release](https://a.yandex-team.ru/projects/verticals/ci/actions/launches?dir=classifieds%2Fverticals-backend&id=service-manual-release)
2. нажать `Run action`
3. выбрать свою ветку (поиск по имени ветки довольно медленный, можно использовать вместо имени – `pr:your-pr-number`)
4. переключиться на вкладку `Custom parameters`
5. вбить имя сервиса
6. и shiva branch, в который нужно выкатить (можно оставить пустым)
7. нажать `Run action`

![](https://jing.yandex-team.ru/files/darl/2022-03-18T16:52:55Z.f7cf287.png)
![](https://jing.yandex-team.ru/files/darl/2022-03-18T16:54:13Z.198963e.png)

Дополнительную информацию о shiva branches можно посмотреть в [документации по Shiva][^shiva-deploy-branches].

[^shiva-deploy-branches]: https://docs.yandex-team.ru/classifieds-infra/deploy/specification/branch


#### Способ 3. Через коммент в пулл-реквесте [временно не работает [VSBAZEL-84](https://st.yandex-team.ru/VSBAZEL-84)]
В пулл-реквесте можно оставить комментарий вида `/deploy general-gateway wisp-api`, тогда за дело возьмется бот и по окончании отрапортует сообщением вида:
```
Deployed service general-gateway:530e3869 to branch pr-6235
Deployed service wisp-api:530e3869 to branch pr-6235
```
с этого момента можно будет ходить в сервисы по соответствующим адресам:
```
general-gateway-pr-6235-api.vrts-slb.test.vertis.yandex.net:80
wisp-api-pr-6235-grpc.vrts-slb.test.vertis.yandex.net:80
```

При необходимости можно задать имя ветки явно: `/deploy branch=my-branch general-gateway wisp-api`. Если имя ветки передать пустым `/deploy general-gateway wisp-api branch=`, то сервисы развернутся в тестинге вместо текущего мастера.

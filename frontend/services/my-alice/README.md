# Моя Алиса

## Релиз

Для релизов в сендбоксе собирается ресурс: [WebMyAliceMicroPackage](https://a.yandex-team.ru/arc/trunk/arcadia/sandbox/projects/sandbox_ci/resources/generated.py?rev=7163640#L27)

Чтобы иметь возможность вручную катать релизы нужно добавить себя в поле `releasers` в файл выше. Также нужно запросить роль `Разработчик` в сервисе [Report Renderer Alice](https://abc.yandex-team.ru/services/reportrendereralice/)

Для ручного релиза можно воспользоваться [формой отведения релизов](https://forms.yandex-team.ru/surveys/50569/) (или соответствующим [CLI](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/release-monorepo-cli)) или пакетом [nanny-workflow-cli](https://github.yandex-team.ru/search-interfaces/ci/tree/master/packages/nanny-workflow-cli), процесс описан [тут](#nanny-workflow-cli). Первый вариант более предпочтительный, т.к. создат релизную таску в очереди `SEAREL` либо допишет в существующую при хотфиксе.


### Процедура релиза

Для релиза нужно иметь [сендбокс ресурс `WEB_MY_ALICE_MICRO_PACKAGE`](#пакет-с-шаблонами).

Также есть сендбокс-таска `NANNY_RELEASE_RESOURCE` (интеграция с няней настроена для нее). Данная таска запускается ежедневно и собирает релизный пакет с данными из мастера (последнюю таску можно увидеть [тут](https://sandbox.yandex-team.ru/tasks?children=true&type=NANNY_RELEASE_RESOURCE&tags=my-alice&limit=20&created=14_days)).

1. Переходим на страничку таски (собранной вручную либо автоматикой), проверяем, что на ней стоит тег `testing`. Теперь нам нужно добавить тег `stable`, чтобы релизный ресурс подхватила няня. Для этого жмем кнопку с галочкой `Release`. По завершении можно переходить к пункту 2.

2. Переходим на [дэшборд рендерера](https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report-renderer-alice/). Справа видим блок с заголовком `NANNY_RELEASE_RESOURCE <номер таски в сендбоксе>`
3. Сверяем номер таски и продолжаем релиз с `пункта 5` [отсюда](https://wiki.yandex-team.ru/search-interfaces/infra/report-renderer/selfduty/#relizyvshared)

## Пакет с шаблонами

Все собранные пакеты можно просмотреть в [сендбоксе](https://sandbox.yandex-team.ru/resources?type=WEB_MY_ALICE_MICRO_PACKAGE&limit=20&created=14_days)

## Nanny

Апстрим: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/hamster.yandex.ru/upstreams/list/upstream_shared_hamster_my_alice/show/

Дэшборд рендерера: https://nanny.yandex-team.ru/ui/#/services/dashboards/catalog/report-renderer-alice/

Хамстер: https://nanny.yandex-team.ru/ui/#/services/catalog/renderer_alice_hamster/

Чтобы увидеть все сервисы алисиного рендерера, можно поискать [тут](https://nanny.yandex-team.ru/ui/#/services/) по запросу `renderer_alice`

## nanny-workflow-cli

Таску можно создать вручную с помощью команды

> nanny-workflow create-release --resource-id=[id ресурса пакета с шаблонами](#пакет-с-шаблонами) --nanny-service-id=renderer_alice_hamster --sandbox-owner=свой логин

Команда может повиснуть надолго. Можно не дожидаться окончания, перейти в [интерфейс сендбокса](https://sandbox.yandex-team.ru/tasks?children=true&author=san4eyz&type=NANNY_RELEASE_RESOURCE&limit=20&created=14_days) и найти нужную таску. Можно отфильтровать по своему логину, чтобы точно увидеть ее. Когда статус будет RELEASED, можно считать, что команда завершилась успешно.

[Пример релизной таски, созданной вручную](https://sandbox.yandex-team.ru/task/761540015/view)

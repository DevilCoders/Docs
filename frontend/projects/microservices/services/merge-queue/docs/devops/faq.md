# Merge Queue DevOps FAQ

* [Как остановить очередь?](#kak-ostanovitь-ocheredь?)
* [Как включить очередь?](#kak-vklyuchitь-ocheredь?)
* [Как влить пулл-реквест в обход MQ?](#kak-vlitь-pull-rekvest-v-obhod-mq?)
* [Как поднять приоритет пулл-реквесту в очереди?](#kak-podnyatь-prioritet-pull-rekvestu-v-ocheredi?)
* [Как понять, что пулл-реквест завис в очереди?](#kak-ponyatь,-chto-pull-rekvest-zavis-v-ocheredi?)
* [Как убрать зависший пулл-реквест из очереди?](#kak-ubratь-zavisshij-pull-rekvest-iz-ocheredi?)
* [Как найти Sandbox-семафор?](#kak-najti-sandbox-semafor?)

## Как остановить очередь?

Через MQ API: [POST /v2/api/queue/disable](../references/api.md#%60post-/v2/api/queue/disable%60).

После остановки MQ заведите [инцидент](https://wiki.yandex-team.ru/infraduty/alarm/).

## Как включить очередь?

Через MQ API: [POST /v2/api/queue/enable](../references/api.md#%60post-/v2/api/queue/enable%60).

Если включение через API не сработало, установите `enabled: true` для коллекции `services` в БД ([скрипт](https://a.yandex-team.ru/api/v2/repos/arc/downloads?at=trunk&path=frontend/projects/microservices/services/merge-queue/docs/devops/scripts/turn-on-queue.js)).

## Как влить пулл-реквест в обход MQ?

1. [Остановить](#kak-ostanovitь-ocheredь?) очередь для проекта.
1. Дождаться влития текущего пулл-реквеста (убедиться, что Sandbox-задача перешла в статус `SUCCESS`).
1. Влить пулл-реквест вручную.
1. [Включить](#kak-ostanovitь-ocheredь?) очередь для проекта.

## Как поднять приоритет пулл-реквесту в очереди?

Ссылка на поднятие пулл-реквеста в [UI](https://mqs.si.yandex-team.ru) находится на плашке пулл-реквеста, кнопка **Inc. Priority**.

> Подробности в [посте](https://clubs.at.yandex-team.ru/search-interfaces/2982) про [форму](https://forms.yandex-team.ru/surveys/9430/).

## Как понять, что пулл-реквест завис в очереди?

Возможны следующие случаи, когда пулл-реквест завис:

* SB-задача `SANDBOX_CI_MERGE_QUEUE` уже завершилась, но пулл-реквест ещё отображается в [UI].
* Запуск в CI (cсылка **build** в [UI]) уже завершился, но SB-задача `SANDBOX_CI_MERGE_QUEUE` не запустилась (нет ссылки в [UI]).

## Как убрать зависший пулл-реквест из очереди?

Напишите комментарий `/stop_merge` в пулл-реквесте.

Если `/stop_merge` не сработал, нужно поменять `state` для пулл-реквестов коллекции `jobs` в БД ([скрипт](https://a.yandex-team.ru/api/v2/repos/arc/downloads?at=trunk&path=frontend/projects/microservices/services/merge-queue/docs/devops/scripts/stop-pr.js)).

## Как найти Sandbox-семафор?

Все MQ-семафоры можно найти по [ссылке](https://sandbox.yandex-team.ru/admin/semaphores?name=mq_&type=list&limit=100).

[UI]: https://mqs.si.yandex-team.ru

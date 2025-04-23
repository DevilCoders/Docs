# Дополнение описания тикетов в Стартреке

Позволяет по запросу из Sandbox дополнять описание связанных с ревью-реквестом тикетов в соответствии с конфигурацией `st-description.(json|yml)`.
> ☝️ [Настройка st-description для Arcanum][arcanum-cfg].

Необходимо чтобы в `custom_fields` в теле запроса присутствовало поле `arcanum_review_request_id`.

Нужно отправить POST-запрос на URL (предполагается использование [WebHookManager]):

```
/v1/sandbox/update-st-description
```

Тело запроса должно содержать JSON-объект, характеризующий Sandbox-таск:

* `id` (`number`) — идентификатор таски;
* `status` (`string`) — статус таски;
* `type` (`string`) — тип таски;
* `custom_fields` (`{ name, value }[]`) — input-параметры таски;
* `output` (`{ name, value }[]`) — output-параметры таски.

Обязательные query-параметры:

* `queues` — список очередей (whitelist), тикеты в которых будут обновлены
* `prNumber` — идентификатор пулл-реквеста, описание связанных тикетов из которых будет обновлено

Шаблонизация осуществляется по аналогии с [обновлением описания тикета для Арканума][arcanum-cfg].

Так же в шаблоне можно использовать [`ejs@v1.0.0`][ejs] строку ([пример][ejs-example]).

[arcanum-cfg]: ./st-description.md
[WebHookManager]: https://a.yandex-team.ru/arc_vcs/sandbox/projects/sandbox_ci/managers/webhook.py?rev=c0a3d4bf883825e82a1f9550cd92daec72971122
[ejs]: https://github.com/tj/ejs
[ejs-example]: https://a.yandex-team.ru/arc_vcs/frontend/.config/st-description.yml?from_pr=1936357&rev=users%2Fnsobyanin%2Fprosperity-test-3

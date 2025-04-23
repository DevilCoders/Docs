# Обновление описания пулл-реквеста

Позволяет по запросу из Sandbox обновлять описание пулл-реквеста в соответствии с конфигурацией `pr-description.(json|yml)`.
> ☝️ [Настройка pr-description для Arcanum][arcanum-cfg].

Чтобы хук работал для описания ревью-реквеста в Arcanum, нужно, чтобы в `custom_fields`
в теле запроса присутствовало поле `arcanum_review_request_id`.

Нужно отправить POST-запрос на URL (предполагается использование [WebHookManager]):

```
/v1/sandbox/update-pull-request-description
```

Тело запроса должно содержать JSON-объект, характеризующий Sandbox-таск:

* `id` (`number`) — идентификатор таски;
* `status` (`string`) — статус таски;
* `type` (`string`) — тип таски;
* `custom_fields` (`{ name, value }[]`) — input-параметры таски;
* `output` (`{ name, value }[]`) — output-параметры таски.

Обязательные query-параметры:

* `configPath` — путь до конфига `pr-description`;
* `sectionId` — идентификатор секции в конфиге, которая должна обновиться. Может принимать множественные значения, например, `&sectionId=experiments&sectionId=custom`;
* `prNumber` — идентификатор пулл-реквеста, в котором требуется обновить описание.

Дополнительные query-параметры:

* `onlyStatuses` — обновлять секции только если таска находится в одном из указанных статусов;
* `ignoreStatuses` — не обновлять секции, если таска находится в одном из указанных статусов.

В отличие от оригинального `pr-description`, в шаблоне `customLinks` можно использовать
[`ejs@v1.0.0`][ejs] строку ([пример][ejs-example]), а также доступны дополнительные данные:

```json5
{
  // Объект пулл-реквеста, см. https://docs.github.com/en/rest/reference/pulls
  "github_pull_request_payload": {
    "number": 2,
    "state": "open"
  },

  // Тело POST-запроса, отправленного в сервис.
  "sandbox_payload": {
    "id": 6251,
    "status": "SUCCESS"
  },

  "extra": {
    // Объединённые input и output параметры таски,
    // трансформированные из { name: "foo", value: 42 }[]` в { foo: 42 }.
    "sandbox_params_obj": {
      "foo": 42,
      "bar": "baz"
    }
  }
}
```
[arcanum-cfg]: ./rr-description.md
[WebHookManager]: https://a.yandex-team.ru/arc_vcs/sandbox/projects/sandbox_ci/managers/webhook.py?rev=c0a3d4bf883825e82a1f9550cd92daec72971122
[ejs]: https://github.com/tj/ejs
[ejs-example]: https://a.yandex-team.ru/arc_vcs/frontend/.config/pr-description.yml?rev=fe917fd9262f2426b5e95e17c13fccc2076692c0

# Использование docker образа

Deploy позволяет развертывать docker образы, указав `name` и `tag`.

{% note warning %}

Предварительно в Docker Distribution необходимо выдать роль **Viewer** `@robot-qloud-client`

{% endnote %}

## Фичи {#features}

* Образ трансформируется в набор porto-слоев, которые образуют файловую систему box. Никаких других слоев по умолчанию добавлено не будет, поэтому образ должен содержать в том числе и базовую систему (вроде `libc.so`).
* Можно добавлять свои porto-слои поверх файловой системы образа. Под низ и в середину добавлять нельзя.
* Подставляются значения из `ENV`, `CMD`, `CWD`, `user:group` из `Dockerfile`. Принцип следующий - `CMD`, `CWD` и `user:group` подставляются, если пользователь явно их не указал. Подстановка работает только в том случае, если в `box` один пользовательский `workload`. Из `ENV` подставляются в box и workload те значения, которые пользователь явно не переопределил.
* Рекомендуется использовать в качестве базовых образов те, что доступны по [ссылке](https://rtc.yandex-team.ru/docs/containers/virtual-images#docker).

## Ограничения {#limits}

* В GUI отсутствует suggest для `name` и `tag`.
* UI не проверяет, доступен ли образ для скачивания. Сейчас это будет понятно только по ошибке вида:

    ```bash
      dctl get stage x0leg-test-stage --format=pb | grep docker_resolver -i -A1
            reason: "DOCKER_RESOLVER_ERROR"
            message: "Invalid response for docker_info request. Code 404"
    ```
  или аналогичной в UI.

## Конфигурирование docker-образа в UI {#config-ui}

Для указания docker образа необходимо в режиме редактирования `Stage` выбрать `Box` и в его конфигурации указать `name` и `tag` образа из `registry.yandex.net`.

Например: name `qe_quality/nirvana_nirvana_job_processor`, tag `1.3734`

## Особенности реализации

* Как уже сказано выше, образ трансформироуется в набор porto-слоёв.
* Начиная со [2ой Runtime Version](https://deploy.yandex-team.ru/docs/reference/patchers-revision#runtime-version-2), проверка на наличие изменений в образе, расположенном по указанному в спеке Box'а URL'у, будет происходить каждый раз при применении изменений в спеке [Deploy Unit'а](https://deploy.yandex-team.ru/docs/concepts/deploy-unit/deploy-unit), в котором данный образ обозначен. Таким образом информация об образе будет обновлена в следующих случаях:
  * Были произведены модификации в любом из нижестоящих объектов [Deploy Unit'а](https://deploy.yandex-team.ru/docs/concepts/deploy-unit/deploy-unit)(изменение спеки Box'а или Workload'а), при этом Box, в котором произошли изменения, может не использовать этот docker образ.
  * Были изменены версии [Sidecar'ов](https://deploy.yandex-team.ru/docs/concepts/pod/sidecars/sidecars)(в том числе и версия Pod Agent'а) в Deploy Unit'е
  * Была изменена [Runtime Version](https://deploy.yandex-team.ru/docs/reference/patchers-revision)
  * Было изменено количество подов или их [Resource Requests](https://deploy.yandex-team.ru/docs/concepts/pod/resource-requests)
* Соответственно, если docker образ по URL'у в Registry был изменён, а модификаций в [Deploy Unit'е](https://deploy.yandex-team.ru/docs/concepts/deploy-unit/deploy-unit) не производилось - в подах [Deploy Unit'а](https://deploy.yandex-team.ru/docs/concepts/deploy-unit/deploy-unit) будет использоваться старая версия docker образа.

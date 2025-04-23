# @yandex-int/frontend-changed-packages-artifact

Для параллельного влития ревью-реквестов по сервисам сборки пулреквестов публикуют ресурсы со списком изменённых сервисов. А MQ находит эти ресурсы и по ним определяет, какие сервисы были затронуты в пулреквесте, чтобы поставить пулреквест в правильную очередь.

Этот пакет предоставляет хелперы для работы с такими ресурсами:

- `buildAttributes(attributes: ChangedPackagesNormalizedAttributes): ChangedPackagesSandboxResourceAttributes`
  Возвращает атрибуты для публикации ресурса в sandbox. Использовать этот хелпер предполагается только в `packages/frontend-ci`
- `normalizeAttributes(attributes: ChangedPackagesSandboxResourceAttributes): ChangedPackagesNormalizedAttributes`
  Нормализует атрибуты ресурса, полученные из Sandbox API. Использовать этот хелпер предполагается во всех местах, которые будут тянуть ресурсы со списком измененных пакетов.
- константы со значениями типа ресурса и атрибута type, чтобы можно было искать эти ресурсы
    ```
    import { RESOURCE_TYPE, TYPE_ATTRIBUTE } from '@yandex-int/frontend-changed-packages-artifact';

    const resources = await sandboxer.resource.finder.find({
        type: [RESOURCE_TYPE],
        attrs: JSON.stringify({
          type: TYPE_ATTRIBUTE
        })
    });
    ```

Related links:
- [FEI-13757: frontend: параллельность в MQ по сервисам](https://st.yandex-team.ru/FEI-13757)
- [Ресурсы со списками изменённых сервисов](https://sandbox.yandex-team.ru/resources?type=SANDBOX_CI_ARTIFACT&owner=FRONTEND&attrs=%7B%22type%22%3A%22changed-packages%22%7D)

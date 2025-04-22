# CMS

CMS (aka Cluster Management System) - сервис, который следит за состоянием кластеров наших хостов.

Разделен на серверную часть (живет в [Шиве](https://a.yandex-team.ru/arcadia/classifieds/services/maps/cms.yml)) и агентов, которые ставятся на каждый хост в кластере.

## Общая информация

[Графики](https://grafana.vertis.yandex-team.ru/d/uGKf3bKnk/cms?orgId=1&refresh=30s)

[База данных в тестинге](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-postgresql/cluster/mdbgaq32umqnon8vpctu?section=overview), [База данных в проде](https://yc.yandex-team.ru/folders/foof1m2t24sjktbjo7ej/managed-postgresql/cluster/mdbtgdr5496mfe56fkvh?section=overview)

[CI в Тимсити](https://t.vertis.yandex-team.ru/project/VertisAdmin_CMS?mode=builds)

[Код лежит здесь](https://a.yandex-team.ru/arcadia/classifieds/infra/cms)

## Принцип работы

На каждом хосте из кластера стоит cms-agent. Агент периодически запускает проверки (либо свои, либо запускает `monrun` и проверяет вывод).

Сервер периодически опрашивает всех агентов и собирает список проверок в базе. После этого анализирует эти проверки, если набор зафейленных проверок попадает под фильтр - запускается определенный **пайплайн** (набор действий) для починки.
Если пайплайн не смог починить хост, то он помечается как требующий ручного вмешательства. Такие хосты отображаются в [Juggler](https://juggler.yandex-team.ru/dashboards/vertis_sre/).

## API

У сервера есть публичное **grpc API**, которое имеет следующие адреса:

**Testing:** `cms.test.vertis.yandex.net:443`

**Production:** `cms.vertis.yandex.net:443`

---

У агентов тоже есть **grpc API**, но оно предназначено только для использования сервером CMS.

### Авторизация
API на сервере требует указания OAuth-токена. [Получить токен](https://oauth.yandex-team.ru/authorize?response_type=token&client_id=e26f216469a4455a9c9f17678114d809)

API на агентах закрыто [TVM](https://wiki.yandex-team.ru/passport/tvm2/). [TVM-ресурсы выписаны](https://abc.yandex-team.ru/services/VSINFR/resources/?search=cms&view=consuming&layout=table) на ABC "Инфраструктура Вертикалей".

### Методы

Все API работает по GRPC протоколу. Protobuf-спецификация методов, параметров и возвращаемых параметров лежит [здесь](https://a.yandex-team.ru/arcadia/classifieds/infra/cms/schema-registry/proto/cms/api).

### Примеры

* Список методов:

  ```bash
  grpcurl -H 'authorization: Bearer <token>' cms.vertis.yandex.net:443 list cms.api.server.ServerService
  ```

* Получить список проверок для конкретного хоста:

  ```bash
  grpcurl -H 'authorization: Bearer <token>' -d '{"name": "docker-05-vla.prod.vertis.yandex.net"}' cms.vertis.yandex.net:443 cms.api.server.ServerService.GetHostStatus
  ```

### Ручка живости для Яндекс.Облака

Специально для Яндекс.Облака добавлена ручка, которая отдает код 503 пока хоть одна проверка не ОК. После этого всегда отдает код 200 (даже если после этого какая-то проверка зафейлится).
Сделано по [документации](https://cloud.yandex.ru/docs/compute/operations/instance-groups/enable-autohealing).



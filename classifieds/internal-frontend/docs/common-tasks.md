# Типовые задачи

### Посмотреть сервис с другими ролями
Увидеть сервис так, как видит другой пользователь? Не проблема! В локальной копии мы можем подменять список ролей пользователя.
Для этого [заходим сюда](https://github.com/YandexClassifieds/internal-frontend/blob/8dae0208620cbd052394279004abdd85e880bfc3/internal-core/server/middlewares/user.js#L19). И переопределяем набор ролей. Вот так:
![user roles](./images/common-tasks-user-roles.png)


### Где взять список ролей?
- Можно запросить по логину пользователя напрямую (в тестинге): http://idm-api-http.vrts-slb.test.vertis.yandex.net/get-user?userip=127.0.0.1&login=ЛОГИН_ПОЛЬЗОВАТЕЛЯ
- Можно подставить свой набор из ((https://github.com/YandexClassifieds/internal-frontend/tree/master/internal-core/common/permissions/manifests манифестов))


### Добавление и использование ролей (контроль доступа)
https://github.com/YandexClassifieds/internal-frontend/pull/796/commits/00ca9f4c81c7844657d721c6aa4326e2399d406a

Для управления доступами используется [IDM](https://idm.yandex-team.ru/).

Роли для каждого из сервисов описываются в [манифесте](https://github.com/YandexClassifieds/internal-frontend/tree/master/internal-core/common/permissions/manifests) с именем сервиса.

Сам IDM информацию о ролях конкретного сервиса получает из нашего [idm-api](https://github.com/YandexClassifieds/internal-frontend/tree/master/idm-api).

Для добавления новой роли в сервис нужно:

1. Добавить роль в соответствующий [манифест](https://github.com/YandexClassifieds/internal-frontend/tree/master/internal-core/common/permissions/manifests).
   > Скорее всего, нужно также добавить новую роль в манифест [user-groups.json](https://github.com/YandexClassifieds/internal-frontend/tree/master/internal-core/common/permissions/manifests/user-groups.json), для роли DEVELOPER/FULL и, возможно, DEVELOPER/READ, если роль на чтение. Эти роли выдаются разработчикам и нужны для отладки.

2. [Пересобрать](https://wiki.yandex-team.ru/users/dcversus/vertis/infra/#sborkavteamcityidemostendy) сервис [idm-api](https://github.com/YandexClassifieds/internal-frontend/tree/master/idm-api), чтобы он "узнал" о новой роли.

3. [Синхронизировать](https://idm.test.yandex-team.ru/system/vsif/sync) новую роль с [тестовым IDM](https://idm.test.yandex-team.ru/). Так новая роль в нужном сервисе станет известна общему тестовому IDM. После этого ее можно выдавать людям (пока только в тестинге).

4. Задеплоить [idm-api](https://github.com/YandexClassifieds/internal-frontend/tree/master/idm-api) в прод.

5. [Синхронизировать](https://idm.yandex-team.ru/system/vsif/sync) новую роль с [продовым IDM](https://idm.yandex-team.ru/). Теперь новая роль в нужном сервисе известна общему IDM в проде. Её можно выдавать людям и использовать в сервисе для контроля доступа.

Для проверки наличия ролей у пользователя используются хелперы из [internal-core/common/permissions](https://github.com/YandexClassifieds/internal-frontend/tree/master/internal-core/common/permissions).

Пример проверки на клиенте:
```javascript
import { rolesHasPermission, getByService } from 'internal-core/common/permissions';
const { OFFER } = getByService('MODERATIONWWW');

if (rolesHasPermission(window._store.user.roles, OFFER.READ)) {
/* your beautiful code */
}
```

Пример проверки на сервере (Node):
```javascript
const { getByService } = require('internal-core/common/permissions');
const { OFFER } = getByService('MODERATIONWWW');
const check = require('internal-core/server/middlewares/check-permission');

router.get('/', check(OFFER.READ), (req, res, next) => {
/* your beautiful code */
});
```

### Добавление фич-флага (admin-www)
Каждый раздел управления фич флагами состоит из изолированных компонентов: сниппет и ручки для обновления, даже не смотря на схожесть НЕЛЬЗЯ ОБОБЩАТЬ И НАСЛЕДОВАТЬ ИХ (в идеале и стили бы тоже разделить).

Общая часть раздела - фильтры с контейнером.

При добавлении нового раздела с фичами:
- реализуем ручки получения в `server/features/${serviceName}`, где отвечаем массивом features в котором лишь service обязателен (по нему рендерится сниппет), за пример можно брать тот же parsing
- реализуем сниппет в `client/pages/Features/feature${serviceName}`, ничего обязательного и строгого тут нет. Сниппет примет как аргумент feature экземпляр из массива features. Также снипет получит `props.onUpdate` - вызов которого лишь заново запросит список фич с сервера (удобно для stateless сниппетов). За основу можно брать тот же featureParsing
- в `client/pages/Features/index` нужно добавить новый элемент в snippetMapping (ключ - serviceName, значение - компонент для рендера), а также добавить новый сервис в список services, для фильтрации.

Хороший пример тут:
https://github.com/YandexClassifieds/internal-frontend/pull/935


### Добавление нового сервиса
1. Карта сервиса + манифест деплоя.
   Создать pull-request в репозиторий [YandexClassifieds/services](https://github.com/YandexClassifieds/services ), в котором добавить 2 файла - манифест деплоя и карту для нового сервиса.
   Пример ПРа:
   https://github.com/YandexClassifieds/services/pull/1113/files
   Документация:
   https://docs.yandex-team.ru/classifieds-infra/service-map
   https://docs.yandex-team.ru/classifieds-infra/deploy/manifest

2. Домен
   Сгенерить тикет в очередь [VASUP](https://st.yandex-team.ru/VASUP), указав имя сервиса, ссылку на ПР с картой и манифестом, а также упомянуть про необходимость создания доменов для бранчей.
   Пример тикета (был перемещен в очередь **VERTISADMIN** по неизвестной причине):
   https://st.yandex-team.ru/VERTISADMIN-24633

3. Boilerplate сервиса.
   Для создания boilerplate-а (каркаса) сервиса можно взять за основу, например, [admin-www](https://github.com/YandexClassifieds/internal-frontend/tree/master/admin-www).
   Пример коммита:
   https://github.com/YandexClassifieds/internal-frontend/pull/1200/commits/1d93902c3ee27318dc78d7130c557b851db2dc58

4. Сборка в TeamCity.
   Добавить в конфиги проекта конфиг для сборки нового сервиса. Самый простой способ - скопировать любой из существующих конфигов и поменять имена и относительные пути.
   Конфиги проекта:
   https://t.vertis.yandex-team.ru/admin/editProject.html?projectId=internal&cameFromUrl=%2Fproject.html%3FprojectId%3Dinternal
   > Не забыть обновить hubfile для автоматизации сборки:
  https://github.com/YandexClassifieds/internal-frontend/pull/1166/commits/59381b33182e2c4a3e32168e030f3c582dd7cfa1

5. Гранты TVM для Blackbox.
   При необходимости походов в Blackbox в новом сервисе нужно заказать соответствующие гранты. Как получить гранты описано [здесь](https://wiki.yandex-team.ru/users/avlyalin/how-to-get-grants-for-blackbox/)

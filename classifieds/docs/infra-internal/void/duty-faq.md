## FAQ

### Исправление/поиск часто встречающихся проблем

#### shiva-gh-app (arcadia validator)

{% cut "Ошибка обработки PR (залипает, паника) " %}

Чтобы исключить из обработки определенный PR нужен найти его в Аркадии по [фильтру](https://a.yandex-team.ru/reviews/incoming?filter=open%28true%29%3Bpublished%28true%29%3Bpath%28%252Fclassifieds%252Fservices%29&sort=-updated_at) и скопировать его номер в деплой ниже

```
/run -l prod -v $current_version -e SKIP:$pr_number shiva-gh-app
```

{% endcut %}

{% cut "Вручную проставить PR Success" %}

Так бывает когда нужно к примеру срочно проставить больше CPU или memory, или сменить овнера без владельца или что-то еще. В этом случае нужно:
1. Дважды перепроверить, что нет еще ошибок в ответе shiva в комментарии
2. [В TeamCity сборке](https://t.vertis.yandex-team.ru/buildConfiguration/VertisAdmin_ArcadiaPr_Validate?) в параметрах поставить [env.manual_success_ids](https://t.vertis.yandex-team.ru/admin/editBuildParams.html?id=buildType:VertisAdmin_ArcadiaPr_Validate) номер PR
3. Перезапустить сборку
4. Сразу смерджить, чтобы не пролезло что-то ломающее работу

{% endcut %}

#### После учений не смогли вернуть инстансы в ДЦ

{% cut "Поиск проблем и исправление" %}

**Алерт**
`handle bulk fail`, в Sentry будет bulk deployment ID  `br`. Как пример https://sentry.vertis.yandex.net/verticals/shiva/issues/63243/ 
**Запрос и поиск проблем**
```SQL
select name from bulk_restart_status
where bulk_restart_id = $br and state != 'Success'
```
**Исправление**
1. В чате [verticals-tech-warroom](https://t.me/joinchat/AjIsiRnjgfZXiNKgednCgQ) предупреждаем о проблеме и что сейчас будет до деплой для возращения инстансов
2. Запускам ручной [bulk deployment](https://docs.yandex-team.ru/classifieds-ops-internal/void/admin#bulkdeployment)
```
grpcurl -d '{"layer":$LAYER, "comment":"возращаю инстансы в ручную", "issue":$DRILSS_ISSUE, "services":["$SERVICE1", "$SERVICE2"], "actualConfiguration":false}' -H "authorization: $OAUTH_TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.BulkDeployment
```
Где, 
- `OAUTH_TOKEN` - личный токен для похода в шиву
- `DRILSS_ISSUE` - номер задачи об учениях
- `SERVICE1, SERVICE2` - имена сервисов из запроса
- `LAYER` - номер слоя (1 - Test, 2 - PROD)

{% endcut %}

#### Залип деплои при попытке раскатиться на два дц при учениях/работах/проблемах в одном ДЦ

{% cut "Поиск проблем и исправление" %}

Такой деплой сам не откатывается, так как не может поселиться. Нужно:
- Взять его ID (например из UI Nomad) и пометить как Fail.
  `nomad deployment fail -verbose -address=http://nomad-01-myt.test.vertis.yandex.net:4646 $ID`
- Далее он попробует откатиться, не сможет, так как ДЦ закрыт и поселиться снова не получится. Для этого повторяем команду выше, но для автоматически созданного реверта. При этом нужно дождаться, когда в доступном дц откат закончится, чтобы не было рассинхрона

При этих действиях Shiva сможет нормально все обработать и остаться в консистентном состоянии.

{% endcut %}

#### Залип деплой на одной из машинок

{% cut "Поиск проблем и исправление" %}

- Зайти на проблемную машинку по ssh
- Выполнить `nomad node drain -self -enable`, машинка исключится из шедулинга
- Написать дежурному админу
- После починки машинки админом, вновь зайти на неё по ssh и выполнить `nomad node drain -self -disable`, машинка вернется в шедулинг

{% endcut %}

#### Отключения проверки синхронизации с github при проблемах shiva-updater или самого github

{% cut "Поиск проблем и исправление" %}

```
grpcurl -d '{"list":[{"name":"ValidateGithubSyncOff", "reason":"тут я напишу причину"}]} -H "authorization: Bearer $TOKEN" shiva-admin.vertis.yandex.net:443 AdministrativeService.SetFlags
```

{% endcut %}

#### Поиск рассинхронизации **/status** (`current_state`) с `deployment` по версии

<details>
<summary>SQL</summary>
<code>
WITH ranked AS (
SELECT d.*, ROW_NUMBER() OVER (PARTITION BY layer, name, branch  ORDER BY id DESC) AS rn
FROM deployment AS d
    where type  in ('Run', 'Promote', 'Revert', 'Stop') and state = 'Success'
),
actual AS (
    SELECT id as deployment_id, layer, name, branch, version, author_id, service_maps_id, deploy_manifest_id, end_date FROM ranked WHERE rn = 1 and type != 'Stop'
),
problems AS (
    select
    status.id,
    status.updated_at,
    status.layer,
    status.name,
    status.branch,
    status.version,
    actual.version,
    actual.deployment_id,
    actual.service_maps_id,
    actual.deploy_manifest_id,
    actual.end_date
from
    current_state status
    inner join  actual on
    status.state = 'StateRunning' and
    status.layer = actual.layer and
    status.name = actual.name and
    status.branch = actual.branch
where
    status.version != actual.version
)
select * from problems
</code>
</details>

Исправление

<details>
<summary>SQL</summary>
<code>
WITH ranked AS (
SELECT d.*, ROW_NUMBER() OVER (PARTITION BY layer, name, branch  ORDER BY id DESC) AS rn
FROM deployment AS d
where type  in ('Run', 'Promote', 'Revert', 'Stop') and state = 'Success'
),
actual AS (
SELECT id as deployment_id, layer, name, branch, version, author_id, service_maps_id, deploy_manifest_id, end_date FROM ranked WHERE rn = 1 and type != 'Stop'
),
problems AS (
select
status.id,
status.updated_at,
status.layer,
status.name,
status.branch,
status.version,
actual.version,
actual.deployment_id,
actual.service_maps_id,
actual.deploy_manifest_id,
actual.end_date
from
current_state status
inner join  actual on
status.state = 'StateRunning' and
status.layer = actual.layer and
status.name = actual.name and
status.branch = actual.branch
where
status.version != actual.version
)
update current_state status set
version = actual.version,
user_id = actual.author_id,
service_map_id = actual.service_maps_id,
manifest_id = actual.deploy_manifest_id,
deployment_id = actual.deployment_id
from actual
where status.state = 'StateRunning' and
status.layer = actual.layer and
status.name = actual.name and
status.branch = actual.branch;
</code>
</details>

#### Добавление deployment GRPC hook

На данный момент добавить новый хук можно только вставкой в бд. Так как предполагается, что операция добавления/изменения будет достаточно редкая. Если часто приходится лазить в базу, то нужно вынесети функционала в API (https://st.yandex-team.ru/VOID-676)

{% cut "Пример добавления подписки на все" %}
```SQL
INSERT INTO setting (id, created_at, updated_at, address, branch, states, service_names, d_types)
VALUES (
        1,
        '2020-04-03 09:05:48.301016 +00:00',
        '2020-04-03 09:05:48.301016 +00:00',
        'shiva-ht-api.vrts-slb.prod.vertis.yandex.net:80',
        true,
        '',
        '',
        '');
```
{% endcut %}


{% cut "Пример добавления подписки на успешный деплой двух сервисов" %}
```SQL
INSERT INTO setting (id, created_at, updated_at, address, branch, states, service_names, d_types)
VALUES (
        1,
        '2020-04-03 09:05:48.301016 +00:00',
        '2020-04-03 09:05:48.301016 +00:00',
        'shiva-ht-api.vrts-slb.prod.vertis.yandex.net:80',
        false,
        'SUCCESS',
        'shiva-test-conf,shiva-test',
        'RUN,PROMOTE');
```
{% endcut %}

#### Перевыпуск TVM-ресурса
**Перевыпускать ресурс можно только при наличии соответствующего тикета. Если кто-то просит об этом в чате, то нужно попросить завести тикет.**

{% cut "Порядок действий" %}

- Проверить, что у вас есть роль "TVM-менеджер". Если она есть, то при открытии соотвествующего ресурса в ABC вверху будут кнопки "Пересоздать секрет", "Восстановить секрет" и "Удалить старый токен". Если роли нет, то нужно попросить [danevge@](https://staff.yandex-team.ru/danevge), чтобы он её выдал.
- Открываем в секретнице текущее значение токена (ссылка лежит в поле `vault_link`).
- Нажимаем на кнопку "Пересоздать секрет". В поле `old_client_secret` должно появиться старое значение токена. В секретнице должна появиться новая версия секрета от `robot-tvm-api`. Эта же новая версия должна быть указана в поле `version_uuid`.
- Ищем секрет в базе шивы с помощью запроса
```SQL
select *
from external_env
where key = '_DEPLOY_G_TVM_SECRET' and service = 'имя_сервиса' and layer = 'окружение'
```
- В колонке `value` меняем версию. 
- В тикете отписываемся, что перевыпустили секрет. В комменатриях к тикету указываем ссылки на старую и новую версии секрета.  
- Сразу после перевыпуска **удалять старый секрет не надо**. **Когда автор тикета попросит удалить старый секрет**, нажимаем на кнопку "Удалить старый секрет". Тогда значение в поле `old_client_secret` должно стать пустым. 

{% endcut %}

#### Очистка кластера jaeger

В качестве быстрого фикса, при подходе к лимиту кластера, можно удалить самую старую партицию в  базе jaeger_test или jaeger_prod

{% cut "Получение всех партиций" %}

```sql
SELECT
  count(*) AS num_parts,
  formatReadableSize(sum(bytes_on_disk)) AS sz,
  partition,
  disk_name,
  table
FROM system.parts
WHERE 1 AND (database = 'jaeger_prod') AND (active = 1) AND (bytes_on_disk > 0) AND (table = 'jaeger_spans_local')
GROUP BY
  partition,
  disk_name,
  table
ORDER BY partition ASC
```

{% endcut %}

{% cut "Удаление партиции" %}

```sql
alter table jaeger_prod.jaeger_spans_local on cluster 'mdb4qlduji821e39c100' drop partition '2022-05-01'
```
{% endcut %}

Уменьшение ttl крайне не рекомендуется, нужно получить апрув коллег!

{% cut "Уменьшение ttl для jaeger кластера" %}
```sql
kill mutation where database = 'jaeger_test' and table = 'jaeger_spans_local';
ALTER TABLE jaeger_test.jaeger_spans_local MODIFY TTL timestamp + toIntervalDay(4);
-- Выполняется порядка нескольких часов

```
{% endcut %}

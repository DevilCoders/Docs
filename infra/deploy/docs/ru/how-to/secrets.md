# Использование секретов в сервисах Деплоя

Я.Деплой позволяет безопасно конфигурировать и приносить в контейнеры данные из секретов, хранящихся в [Секретнице](https://yav.yandex-team.ru/) (документация по работе с Секретницей - [здесь](https://vault-api.passport.yandex.net/docs/)).

## Объявление секретов 
На текущий момент в деплое есть две схемы объявления секретов: рекомендуемая (новая) и устаревшая.
В этой статье рассказано про обе, а также про механизмы миграции на рекомендуемую схему.

В Деплое список секретов представлен следующей [proto схемой](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/data_model.proto?rev=r8706994#L1587-1600):

```C
// Reference to a secret from another object.
message TSecretRef
{
    // Object id of the secret (equals its vault id).
    optional string secret_id = 1;
    // Version to retrieve. If empty, retrieve the latest version.
    optional string secret_version = 2;
}
...

message TPodSpec
{
...
    message TSecret
    {
        required string secret_id = 1;
        required string secret_version = 2;
        required string delegation_token = 3;
    }
    // Defines secrets to be delivered to the pod.
    map<string, TSecret> secrets = 16
    [(NYT.NYson.NProto.yson_map) = true, deprecated = true];

    // References secrets to be delivered to the pod.
    map<string, TSecretRef> secret_refs = 27
    [(NYT.NYson.NProto.yson_map) = true, (NYP.NClient.NApi.NProto.etc) = true];
...
}
```

В данной части спеки указано два списка: `secret_refs` и `secrets`.
* `secret_refs` содержит секреты в **рекомендованном** формате списка объектов структуры `TSecretRef`
* `secrets` содержит секреты в **устаревшем** формате списка объектов структуры `TSecret`

В части спеки объекты `TSecretRef` и `TSecret` отличаются только тем, что в `TSecretRef` не хранятся delegation token'ы. Это позволяет не хранить sensitive данные в спеке сервиса и хранить настройки сервиса в открытом репозитории (например, Аркадии). При использовании рекомендуемой новой схемы YP самостоятельно выпишет и привяжет, а Деплой прокинет по всему стеку delegation token'ы прозрачно для пользователя. Больше технических деталей - в [посте в Этушке](https://clubs.at.yandex-team.ru/infra-cloud/2059).

{% note warning %}

При использовании старой схемы объявления секретов `delegation_token` тоже является секретной частью секрета, поэтому его нельзя в явном виде сохранять в репозитории.

Не делитесь ни с кем данными своих секретов или токенов в открытом виде и по возможности запланируйте миграцию секретов в своих сервисах на новую схему.

{% endnote %}

###  Объявление секретов в UI

Список секретов, объявленных в deploy unit'е, отображается на вкладке `Secrets` на странице настроек deploy unit'а. Там же доступны основные операции над секретами: добавление нового секрета или его версии, изменение алиаса (идентификатора, используемого при привязке секрета к ресурсу в поде) или удаление неиспользуемых секретов из списка.

В местах использования секрета он выбирается из списка уже используемых, но можно добавить новый секрет (под капотом он добавится в список).

Чуть подробнее о механизме работы с секретами в этом [посте](https://khoden.at.yandex-team.ru/2).

### Миграция со старой на новую схему

**UI**
Мигрировать секреты со старой схемы объявления но новую можно несколькими способами во владке `Secrets` на странице настроек deploy unit'а:
1. Миграция всех секретов сразу - кнопка **Migrate all secrets to the new format**
2. Миграция отдельного секрета (для постепенной миграции) - кнопка **Migrate to new storage** в выпадающем меню для конкретного секрета
![secrets migration](../_assets/how-to/secrets-migration.png) 

**dctl/API**
Для миграции секретов со старой схемы на новую при помощи dctl/API достаточно: 
1. Скачать спеку сервиса
2. Переименовать секцию `secrets` в `secret_refs` и удалить из неё delegation_token'ы
3. Сохранить спеку в YP

## Работа с секретами
В этом разделе будет описана работа с секретами только в новой схеме. Если вы используете устаревшую схему объявления секретов, запланируйте миграцию на новую схему.

Секреты, объявленные в спеке стейджа (в блоке `secret_refs`), могут приноситься в под в нескольких видах:
* как [переменная окружения](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r8809475#L651) - для бокса или ворклоада
* как файловый секрет в виде статического ресурса - доступен как выбор [отдельного ключа секрета](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r8809475#L327), так и сохранения [всех ключей секрета с возможностью выбора формата](https://a.yandex-team.ru/arc/trunk/arcadia/yp/yp_proto/yp/client/api/proto/pod_agent.proto?rev=r8809475#L331).

## Дополнение
{% cut "Как передать секрет в под при использовании старой схемы" %}
Чтобы доставить секрет в старом формате в под, надо сделать две вещи:
#### 1. Выписать `delegation_token` на секрет для yp
* Для этого надо зайти в [секретницу](https://yav.yandex-team.ru/), открыть ваш секрет, перейти в "токены"
* Нажать "новый токен", в качестве `TVM id` указать `2001151` (сервис `YP`), в качестве пароля указать `<stage_id>.<deploy_unit_id>`.

{% note warning %}

**Если пароль получится длиннее 30 букв**, интерфейс Секретницы его не примет. Выписывайте токен через консольный [`ya vault`](https://vault-api.passport.yandex.net/docs/#cli) (он же `yav`), пример см. чуть ниже.

Обращаем внимание, что секрет выписывается для пары `stage` и `deploy_unit`, т.е. при копировании stage или при создании еще одного `deploy_unit`, надо выписывать дополнительные `delegation_token`.

{% endnote %}

{% note info %}

Для работы с YP man-pre или sas-test, нужно использовать `TVM id`: 2024345.

{% endnote %}

В случае возникновения проблем с тем, что пароль для токена слишком длинный, его можно выписать про помощи `ya vault`:

```bash
$ ya vault create token sec-01djayv3qjn88kgw7efkj34bk7 -tvm 2001151 -s chegoryu-test-secrets.DU1
secret uuid: sec-01djayv3qjn88kgw7efkj34bk7
token: E_EpJ8QxWMjq9L_n3R19_rhtseR61qVLmZQ5xbemw_E.1.476448a3ea5b6799
```
#### 2. Указать секрет в спеке пода:

```yaml
secrets:
  sec-01djayv3qjn88kgw7efkj34bk7:ver-01dzrhz1tma6fjhvxwdjwggn9w:
    delegation_token: yx49LJTyWXvyZKmEB-7E1igiYMkKjVM44cYvGeGSPZc.1.3ca1a513683c70fb
    secret_id: sec-01djayv3qjn88kgw7efkj34bk7
    secret_version: ver-01dzrhz1tma6fjhvxwdjwggn9w
```

Можно заметить, что в данном случае ключом в `map<string, TSecret> secrets = 16` выбрано `sec-01djayv3qjn88kgw7efkj34bk7:ver-01dzrhz1tma6fjhvxwdjwggn9w`, на самом деле, такое наименование не обязательно, ключ может быть любым, но рекомендуется использовать такой же стиль именования, который используется в UI, а именно, `<SECRET_UUID>:<SECRET_VERSION>`.

{% endcut %}

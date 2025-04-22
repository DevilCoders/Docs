# Доступы
## Если нужны дырки к источнику { #puncher }
Если источник **облачный**, из внешнего интеренета, либо ранее уже подключался к репликации, то этот шаг можно пропустить.
Иначе, стоит получить доступы в панчере, для этого создайте новое правило и укажите в поле `Источник`:
* `_REPLICATION_TEST_NETS_` для [тестинга](https://puncher.yandex-team.ru/?create_protocol=tcp&create_sources=_REPLICATION_TEST_NETS_&create_until=persistent)
* `_REPLICATION_NETS_` для [прода](https://puncher.yandex-team.ru/?create_protocol=tcp&create_sources=_REPLICATION_NETS_&create_until=persistent)

В поле `Назначение` укажите новый добавляемый источник.

## Секреты { #secrets }

{% note tip %}

Сразу после добавления секрета вы можете [проверить](source_validation.md) его работоспособность до создания правила

{% endnote %}

**Секрет** в контексте сервиса репликации - это совокупность всех параметров,
необходимых для подключения к источнику. Такими параметрами могут являться
адреса хостов, на которых развернут источник, пользователь и пароль для
доступа к источнику, порт, имя БД и другие, в зависимости от типа источника.

Сейчас в сервисе используются три типа указания секретов:
* yav
* strongbox
* secdist (**deprecated**)

Для источника **mongo** yav/strongbox секреты пока не поддержаны.
[Инструкция по указанию секретов для mongo](../../sources/mongo/mongo.md)


## Какой способ выбрать { #which_secret_to_choose }
В общем случае схема такова:
* Если на руках есть только параметры подключения: **yav**
* Если уже есть секрет в strongbox: **strongbox**
* Если yav и strongbox еще не поддержаны для источника: **secdist**

## Как добавить секрет в репликацию { #how_to_add }
{% note warning %}

Новый секрет попадает в репликацию приблизительно через пять минут после
добавления.

{% endnote %}

{% note warning %}

Если секрет уже заведен - можно перейти сразу к [этапу использования](#how_to_use_secret).
Также для уже существующего секрета можно воспользоваться [генератором правил](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules/README.md#generaciya-pravil)

{% endnote %}

### yav { #how_to_add_yav }
[Секретница](https://yav.yandex-team.ru)

Для тестинга и для прода заводятся отдельные секреты.
Форматы ключей для источников:
* [postgres](#secret_keys_postgres)
* [oracle](#secret_keys_oracle)
* [mssql](#secret_keys_mssql)
* [mysql](#secret_keys_mysql)

После добавления секрета в yav необходимо добавить ему тэг 'replication',
а также выдать доступ для чтения одному из роботов репликации:
* testing: [robot-taxi-tst-repl](https://staff.yandex-team.ru/robot-taxi-tst-repl)
* production: [robot-taxi-repl](https://staff.yandex-team.ru/robot-taxi-repl)

Для указания секрета в правиле, необходимо указать его алиас и id в
config.yaml и в самом правиле. Алиас может быть произвольным.
#### Где взять id yav секрета { #where_to_get_yav_id }
Возможны два варианта:
* Скопировать id секрета со страницы просмотра секрета<br>
![yav secret id](_images/secrets_yav_secret_id.png "yav secret id")
* Из ссылки на секрет<br>
  Пример: https://yav.yandex-team.ru/secret/sec-01fzadwxwbwycj0nryge8fvkmh -
  часть после последнего слэша (`sec-01fzadwxwbwycj0nryge8fvkmh`)


#### Необходимые ключи для источников { #secret_keys_by_source }
{% note warning %}

Если используется несколько хостов, они должны быть указаны через запятую
**без пробелов**

{% endnote %}
#### postgres { #secret_keys_postgres }
* **shards.{номер_шарда}.user**: пользователь для подключения к БД
* **shards.{номер_шарда}.host**: хост (или хосты) БД
* **shards.{номер_шарда}.password**: пароль для подключения к БД
* **shards.{номер_шарда}.db_name**: имя БД на хосте
* **shards.{номер_шарда}.port**: порт для подключения к БД

<details>
    <summary>Пример полностью корректного секрета с двумя шардами:</summary>

```yaml
## в этом примере у первого шарда два хоста, у второго шарда - один хост
shards.0.host: shard0host0.yandex.net,shard0host1.yandex.net
shards.0.port: 1234
shards.0.db_name: db0
shards.0.user: user0
shards.0.password: password0
shards.1.host: shard1host0.yandex.net
shards.1.port: 1234
shards.1.db_name: db1
shards.1.user: user1
shards.1.password: password1
```
</details>



#### oracle { #secret_keys_oracle }
* **shards.{номер_шарда}.dsn**: корректный oracle dsn для подключения к БД
* **shards.{номер_шарда}.user**: пользователь БД
* **shards.{номер_шарда}.password**: пароль БД

<details>
    <summary>Пример полностью корректного секрета с двумя шардами:</summary>

```yaml
shards.0.dsn: (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=tst.host0.example.com)(PORT=1531))(CONNECT_DATA=(SERVICE_NAME=test)))
shards.0.user: user0
shards.0.password: password0
shards.1.dsn: (DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=tst.host1.example.com)(PORT=1531))(CONNECT_DATA=(SERVICE_NAME=test)))
shards.1.user: user1
shards.1.password: password1
```
</details>


#### mssql { #secret_keys_mssql }
* **shards.{номер_шарда}.database**: имя БД на хосте
* **shards.{номер_шарда}.host**: хост, на котором расположена БД
* **shards.{номер_шарда}.password**: пароль для подключения БД
* **shards.{номер_шарда}.port**: порт для подключения БД
* **shards.{номер_шарда}.user**: пользователь БД

<details>
<summary>Пример полностью корректного секрета с двумя шардами:</summary>

```yaml
shards.0.database: db0
shards.0.host: test0.yandex.net
shards.0.password: password0
shards.0.port: 1234
shards.0.user: user0
shards.1.database: db1
shards.1.host: test1.yandex.net
shards.1.password: password1
shards.1.port: 1234
shards.1.user: user1
```
</details>

#### mysql { #secret_keys_mysql }
* **shards.{номер_шарда}.database**: имя БД на хосте
* **shards.{номер_шарда}.host**: хост, на котором расположена БД
* **shards.{номер_шарда}.password**: пароль для подключения БД
* **shards.{номер_шарда}.port**: порт для подключения БД
* **shards.{номер_шарда}.user**: пользователь БД

<details>
    <summary>Пример полностью корректного секрета с двумя шардами:</summary>

```yaml
shards.0.database: db0
shards.0.host: test0.yandex.net
shards.0.password: password0
shards.0.port: 1234
shards.0.user: user0
shards.1.database: db1
shards.1.host: test1.yandex.net
shards.1.password: password1
shards.1.port: 1234
shards.1.user: user1
```
</details>


### strongbox { #how_to_add_strongbox }
Кнопка выдачи доступа:
![Кнопка выдачи доступа](_images/secrets_strongbox_tvm_access.png "Кнопка выдачи доступа")
<br>
[Strongbox секреты в админке](https://tariff-editor.taxi.yandex-team.ru/secrets)

{% note warning %}

Если секрет заведен как freeform — добавлять его нужно через [yav](#how_to_add_yav).

{% endnote %}

{% note warning %}

Если у вас нет прав нажать на кнопку, то стоит попросить это сделать админов
в чате [taxi-ito-helpline](https://wiki.yandex-team.ru/taxi/backend/chats/#jekspluatacijauchenijaireglamentnyeraboty).

{% endnote %}

Для того, чтобы секрет из strongbox попал в репликацию, достаточно выдать TVM
доступ к своему секрету сервису `replication` на странице секретов. В качестве
алиаса для секрета strongbox в config.yaml рекомендуется использовать
STRONGBOX_ID секрета, т.е.:
```yaml
secrets:
    STRONGBOX_ID:
        type: strongbox
        id: STRONGBOX_ID
```

При использовании yav/strongbox секрета, в правиле указывается его алиас,
а id секретов указываются в config.yaml.

## Как воспользоваться добавленным секретом { #how_to_use_secret }

### Как проверить добавленный секрет
Перед началом использования секрета,
его можно проверить с помощью
[драфта](source_validation.md).


### Формат id секретов в config.yaml { #secret_config_yaml }
```yaml
...
secrets:
    secret_yav_alias:
        type: yav
        id:
            testing: sec-1234
            production: sec-4321
    STRONGBOX_ID:
        type: strongbox
        id: STRONGBOX_ID
```
Здесь:
* **secret_yav_alias, STRONGBOX_ID** - алиасы секретов для указания в правиле
* **type**: тип секрета. Допустимые значения: yav, strongbox
* **id**: id секрета. Подробнее по типам рассмотрены в соответствующих секциях

В одном config.yaml может быть указано любое количество секретов. Секрет из
config.yaml может использоваться любым количеством правил.

В id yav секрета обязательно должны быть ключи `testing` и `production`.
Если production-секрета пока нет на руках и правило планируется деплоить
только в тестинг - допустимо в этом поле указать какую-нибудь заглушку
вроде `none-yet`.

### Указание секрета в правиле { #secret_in_rule }
Алиас секрета из config.yaml указывается в секции `connection` правила. Пример:
```yaml
connection:
    secret: secret_yav_alias  ## yav
```

```yaml
connection:
    secret: STRONGBOX_ID  ## strongbox
```
В правиле допустимо использовать только те алиасы, которые описаны в
config.yaml

### Примеры указания секретов { #secrets_live_examples }
* **yav**: <br>
[config.yaml](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules/replication_rules/market_lms/plugins/config.yaml) <br>
[Правило для этого config.yaml](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules/replication_rules/market_lms/partner.yaml)
* **strongbox**: <br>
[config.yaml](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules/replication_rules/agent/plugins/config.yaml) <br>
[Правило для этого config.yaml](https://a.yandex-team.ru/arc_vcs/taxi/dmp/dwh/replication_rules/replication_rules/agent/user.yaml)

### secdist { #secdist }
Если используется источник, для которого еще не поддержан yav/strongbox,
можно воспользоваться схемой с секдистом. В этом случае в ключе `connection`
нужно указать ключ `path`, в который нужно положить путь до секрета в
секдисте, например так:

```yaml
connection:
    path: settings_override.mysql.connections.tips
```

## Как устроена работа с секретами { #tech_details }
На хостах репликации работает демон, который с заданной частотой забирает все
секреты, на которые у него есть доступ, и кэширует их в файлах на хостах.
Сейчас он забирает их каждые три минуты, в будущем это значение может
измениться, такие изменения также будут отражены в документации.

* Для strongbox-секретов доступными секретами считаются те, на которые в
админке открыт TVM-доступ сервису replication.
* Для yav-секретов доступными секретами считаются те, на которых установлен тэг
`replication`, и на которые открыт доступ соответствующему роботу.

При запуске сервиса репликации все закэшированные в файлах секреты
вычитываются в кэш в памяти, который обновляется каждую минуту. При
возникновении необходимости доступа к тому или иному секрету происходит
обращение в этот кэш в памяти, откуда по id достается тело секрета. В целом
механизм чтения секрета аналогичен секдисту, различие только в том, что для
получения секретов из секдиста необходимо знать полный путь в секдисте, а для
получения yav/strongbox секрета достаточно знать только его id.

Исходя из описанной логики, на текущий момент секрет попадает в репликацию
приблизительно за три-пять минут после открытия к нему доступа.

Если в секрете отсуствуют какие-то обязательные поля, то крона с правилом не
запустится. Информацию об этом можно увидеть в логах:
* [testing](https://kibana.taxi.tst.yandex-team.ru/goto/b0a81650-af6b-11ec-b1f0-f7f9894a7779)
* [production](https://kibana.taxi.yandex-team.ru/goto/641de07218388f32bc1c09442e5f4b36)

Пример текста:

`Secret with alias tips is incomplete: missing '['shards.0.user']' keys.`

Означает, что в секрете с алиасом tips отсуствует обязательное поле user
(`shards.0.user`).

Если данные в секрете некорректные (неверный хост, не подходит пароль etc), то
крона упадет с ошибкой подключения, увидеть это можно в админке крон.

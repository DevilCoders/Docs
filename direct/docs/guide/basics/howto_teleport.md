# Тестовые данные: "телепорт" клиентов из одной базы в другую

{% note alert "Экспериментальная функциональность" %}

ВНИМАНИЕ: Эта функциональность экспериментальная и корректная работа не гарантируется.
Ресурсов на разбор возникающих проблем у оригинального автора (yukaba) нет. 

При возникновении проблем рекомендуется искать другие способы решения задачи. 

Участие продуктовой разработки в поддержке/усовершенствовании приветствуется.

{% endnote %}

{% note info  "Предупреждения" %}

1. Клиенты после телепорта могут оказаться на нескольких шардах: такие клиенты __Не__ будут работать в __DNA__. (предположительно при работе с группами)

1. При выполнении не скопировались ключевые слова. (при импорте использовался `--replace-existing`)

{% endnote %}


## Как скопировать данные из продакшена на devtest:

1. Создать директорию для промежуточных файлов (имя и расположение не важно, главное, чтобы можно было читать/писать)  
    `LOGIN=MyClientLogin`  
    `mkdir /tmp/client-data-$LOGIN`

1. Перейти в директорию с бетой
1. Проверить, что бета смотрит на нужную базу (=куда хотим перенести клиента)  
    `direct-mk | grep configuration `  
    _должно вывести что-то вроде "configuration: devtest"_

1. На бете запустить экспорт данных из продакшена  

    - для самостоятельного клиента достаточно указать только логин клиента  
          `SETTINGS_LOCAL_SUFFIX=ROProd ./protected/maintenance/export_client_data.pl --dir /tmp/client-data-$LOGIN --login $LOGIN`  

    - для менеджерских клиентов нужно указать также логин менеджера  
          `SETTINGS_LOCAL_SUFFIX=ROProd ./protected/maintenance/export_client_data.pl --dir /tmp/client-data-$LOGIN --login $LOGIN --login ManagerLogin`  

    - для агентских клиентов, кроме логина клиента, нужны логин агентства и менеджера агентства;   
       кроме этого, указать, что это менеджер этого агентства  
       `SETTINGS_LOCAL_SUFFIX=ROProd ./protected/maintenance/export_client_data.pl --dir /tmp/client-data-$LOGIN --login $LOGIN --login AgencyLogin --login AgencyManagerLogin`

    Логин менеджера можно получить командой
    
    ```shell
    dbs-sql -B pr:ppc:all "select login from users where uid = "$(dbs-sql -B pr:ppc:all "select cl.primary_manager_uid from users u inner join clients cl on cl.clientId = u.clientId where u.login='$LOGIN'")
    ```

    Логин агентства можно получить командой 
    ```shell 
    dbs-sql -B pr:ppc:all "select login from users where uid = "$(dbs-sql -B pr:ppc:all "select cl.agency_uid from users u inner join clients cl on cl.clientId = u.clientId where u.login='$LOGIN'")
    ```

    Что делать если экспорт падает с ошибками смотри [ниже](#error_table).

1. На бете запустить импорт в нужную базу  
    `./protected/maintenance/import_client_data.pl --dir /tmp/client-data-$LOGIN --move-existing-to-next-shard`
 
    если есть агентства, нужно указать их менеджеров  
    `./protected/maintenance/import_client_data.pl --dir /tmp/client-data-$LOGIN --move-existing-to-next-shard --manager-for-agency AgencyLogin=AgencyManagerLogin` 

    Параметр _`--move-existing-to-next-shard`_ означает, что если клиент уже есть, то его данные будут писаться в следующий шард
    (если есть в 9-м, то в 10-й, если есть в 21-м, то в 1-й), чтобы не затереть старые данные, если вдруг понадобятся.

    Лог импорта лежит в `protected/logs/import_client_data.log.<сегодняшнее число>`

    Что делать если импорт падает с ошибками смотри [ниже](#error_import)

## Как скопировать данные о кампании из продакшена GRuT на devtest/TS
1. Перейти в инструмент на DT/TS (в зависимости от того куда нужно скопировать): [из продакшена на TS](https://test-direct.yandex.ru/internal_tools/#campaign_teleporter_tool) или [на DT](https://8080.beta1.direct.yandex.ru/internal_tools/#campaign_teleporter_tool)
2. Ввести id кампании.
3. Если в тестовой базе GRuT'а уже есть данные о кампании то можно поставить соответствующую галочку для обновления заявки на DT/TS (по умолчанию выключено). При этом будет удалена заявка со всеми прикрепленными к ней ассетами и замещена новыми данными из продакшена.
4. Если после копирования нужно запустить джобу перегенерации UpdateAdsJob то так же можно поставить соответствующую галочку в окне инструмента (по умолчанию выключено). Но обычно этого не требуется, т.к. все данные из mysql уже должны были скопироваться директовым телепортом
5. Нажать 'выполнить'

Как и в случае с dna кампания может не открываться в интерфейсе, если после директового телепорта из mysql был повторно создан клиент на другом шарде.
Для обхода такой проблемы нужно:

Узнать какой клиент на заявке 
```bash
# Запрос для получения id клиента у заявки на DT
./grut-orm get --address=dev --selector=/meta/client_id --format=yson --no-tabular campaign 67558994 
# На TS
./grut-orm get --address=dev --selector=/meta/client_id --format=yson --no-tabular campaign 67558994 
```
Узнать шард кампании, с тем же id клиента
```mysql
direct-sql dt:ppc:all "select cid, clientId 
from campaigns 
where cid = 67558994
and clientid = 91084191"
```
Узнать шард клиента в ppcdict.shard_client_id
```mysql
direct-sql dt:ppcdict "select *
from shard_client_id
where ClientID = 91084191"
```
Если шард отличается - поменять
```mysql
direct-sql dt:ppcdict "update shard_client_id 
set shard = 1
where ClientID=91084191
limit 1"
```

## Падение экспорта "Table ppc. doesn't exist" { #error_table }

Если экспорт упадёт с ошибкой типа "Table ppc. doesn't exist", то мы пытаемся экспортировать данные из таблицы, про которую знает код, но которой нет в продакшене.   

Тогда нужно удалить запись о ней из protected/Direct/ReShard/Rules.pm, _(например для таблицы с именем added_phrases_cache)_, так:  
`sed -i '/added_phrases_cache/ d' ./protected/Direct/ReShard/Rules.pm`

После этого сделать на бете   
`svn diff ./protected/Direct/ReShard/Rules.pm`,   
должно получиться что-то вроде  

```diff
Index: protected/Direct/ReShard/Rules.pm
===================================================================
--- protected/Direct/ReShard/Rules.pm   (revision 137607)
+++ protected/Direct/ReShard/Rules.pm   (working copy)
@@ -129,7 +129,6 @@
                     mod_resync_media_queue
                     campaigns_experiments
-                    added_phrases_cache
                     /],
         key => 'cid',
     },
```

Смотреть надо на строки, начинающиеся c `-`, такая должна быть одна, с именем таблицы, которую хотим выкинуть.

Однако, если удаляемая таблица оказалась единственной в блоке `tables`, и дифф выглядит вот так:

```diff
Index: protected/Direct/ReShard/Rules.pm
===================================================================
--- protected/Direct/ReShard/Rules.pm	(revision 8971792)
+++ protected/Direct/ReShard/Rules.pm	(working copy)
@@ -830,7 +830,6 @@
         key => 'aic.ClientID',
     },
     {
-        tables => [qw/callout_moderation_versions/],
         from => "additions_item_callouts aic join %s t on t.callout_id = aic.additions_item_id",
         replace => 1,
         delete_key => 'callout_id',
```

Тогда нужно открыть файл protected/Direct/ReShard/Rules.pm в редакторе и целиком удалить весь объект, в котором была таблица.

![alt text](_assets/teleport-remove-block.png)

Diff после удаления должен выглядеть вот так:

```diff
Index: protected/Direct/ReShard/Rules.pm
===================================================================
--- protected/Direct/ReShard/Rules.pm	(revision 8971792)
+++ protected/Direct/ReShard/Rules.pm	(working copy)
@@ -830,13 +830,6 @@
         key => 'aic.ClientID',
     },
     {
-        tables => [qw/callout_moderation_versions/],
-        from => "additions_item_callouts aic join %s t on t.callout_id = aic.additions_item_id",
-        replace => 1,
-        delete_key => 'callout_id',
-        key => 'aic.ClientID',
-    },
-    {
         tables => [qw/additions_item_callouts additions_item_disclaimers additions_item_experiments/],
         key => 'ClientID',
     },
```

Вернуть всё назад (как в транке или ветке) можно командой  
`svn revert ./protected/Direct/ReShard/Rules.pm`


## Падения импорта { #error_import }

1. Если импорт не записал данные как положено в rbac или вообще упал, то можно повторить попытку без записи в ppcdata с опцией `--only-rbac`:  
    `./protected/maintenance/import_client_data.pl --dir /tmp/client-data-$LOGIN --only-rbac`

1. Если импорт падает с ошибками _Duplicate key_ ..., даже если указана опция `--move-existing-to-next-shard`, то с этим можно побороться, перезапустив с ключом `--replace-existing`.



# Алиасы

Большинство сервисов используют одинаковые версии {{ serviceName }} (например, текущую стабильную), при этом релизы выпускаются на регулярной основе. Поэтому вручную менять номер версии Skynet в [правилах](skynet-version.md) для каждого сервиса нецелесообразно. Чтобы уменьшить время, требуемое на поддержку связи сервисов с требуемыми версиями {{ serviceName }}, используются алиасы. Алиас указывается вместо [версии Skynet](skynet-version.md#sandbox-resource) при регистрации правил. В дальнейшем при выпуске нового релиза Skynet, достаточно будет [указать новый номер версии в параметрах алиаса](#editing-alias), а не в каждом правиле.

[Создание алиаса](#alias-creation)

[Редактирование алиаса](#editing-alias)

[Удаление алиаса](#deleting-alias)

{% note warning %}

[Создать](#alias-creation) или [изменить](#editing-alias) алиас может только владелец секции (owner).

{% endnote %}

## Создание алиаса {#alias-creation}

Чтобы создать алиас:

1. Перейдите в секцию **skynet** → **versions** ([https://genisys.yandex-team.ru/sections/skynet.versions](https://genisys.yandex-team.ru/sections/skynet.versions)) и нажмите кнопку **Manage resource aliases**.
    
1. Нажмите кнопку **Add an alias** и заполните поля:
    
    {% cut "Описание полей" %}

    Поле | Описание | Признак обязательности
    :--- | :--- | :---
    **Alias name** | Алиас в свободной форме. | Обязательное.
    **Release** | Идентификатор задачи Sandbox, содержащей требуемые ресурсы `skynet.bin`.<br/><br/>Для выбора доступны задачи, у которых указан тип ресурса <q>SKYNET_BINARY</q>. | Обязательное.

    {% endcut %}

1. Сохраните изменения (кнопка **Save**).
    
В результате в {{ deploy-and-configService }} зарегистрирован новый алиас, который может быть использован при указании [версии {{ serviceName }}](skynet-version.md).

## Редактирование алиаса {#editing-alias}

Чтобы изменить ранее созданный алиас:

1. Перейдите в секцию **skynet** → **versions** ([https://genisys.yandex-team.ru/sections/skynet.versions](https://genisys.yandex-team.ru/sections/skynet.versions)) и нажмите кнопку **Manage resource aliases**.
    
1. Измените наименование алиаса (**Alias name"**) или указанный идентификатор ресурсов (**Release**). Для выбора доступны задачи, у которых указан тип ресурса <q>SKYNET_BINARY</q>.
    
1. Сохраните изменения (кнопка **Save**).
    

В результате в {{ deploy-and-configService }} алиасу ставится в соответствие новая версия дистрибутива `skynet.bin`.

На серверах сервисов, для которых алиас определяет требуемую версию {{ serviceName }}, обновление установленной версии выполняется после очередного запуска [gosky](gosky-install.md). Для Linux-серверов периодичность запуска определяется в `/etc/cron.d/skynetd`.

## Удаление алиаса {#deleting-alias}

{% note warning %}

Перед удалением алиаса [внесите необходимые изменения во все правила](skynet-version.md#editing-skynet-version), в которых используется данный алиас, например укажите версию дистрибутива `skynet.bin`. В противном случае возвращается ошибка:

```
Invalid Sandbox Task ID
```

{% endnote %}

Чтобы удалить алиас:

1. Перейдите в секцию **skynet** → **versions** ([https://genisys.yandex-team.ru/sections/skynet.versions](https://genisys.yandex-team.ru/sections/skynet.versions)) и нажмите кнопку **Manage resource aliases**.
    
1. Нажмите кнопку **Remove** в строке с удаляемым алиасом.
    
1. Сохраните изменения (кнопка **Save**).
    
В результате информация об алиасе удалится из {{ deploy-and-configService }}.

### Узнайте больше

* [Процедура обновления версии Skynet (Вики)](https://wiki.yandex-team.ru/Skynet/HowToUpdate/)

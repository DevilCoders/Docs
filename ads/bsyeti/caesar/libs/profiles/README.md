#### Инструкция по добавлению нового профиля
##### Схема данных - протобуф
Описываем схему данных в формате протобуф файла (в директори [proto](proto/)).
Для каждого поля верхнего уровня указывам дополнительную мета информацию:
- имя колонки в дин. таблице на YT (`FieldName`)
- мета-тип колонки (`FieldType`)

Колонка может иметь один из следующих мета-типов:
- `PFT_KEY` - это означает, что колонка является первичным ключем.
            в качестве ключевых можно выбрать несколько колонок, тогда ключ таблицы будет составной
- `PFT_PACKABLE` - это значит, что данное поле физически будет хранится в двух колонках: База и Патч.
                 - и внутрениий алгоритм бинарных диффов будет выбирать обновлять целиком всю колонку (базу)
                   или отправить только маленький дифф к базе, вместо обновления всей колонки.
                   Данный алгоритм позволяет уменьшать поток на запись, в случаях когда в колнке хранится большой
                   объем данных, но обновляется маленькими кусочками.
- `PFT_SIMPLE` - хранить поле в YT в отдельной колонке как есть. Обычно используется для хранения флагов.

Также указываем название таблицы через `option`, например, так:
```
option (NBigRT.YtTableName) = "Banners";
```
Таблицу стоит называть по множественном числе. Например, Banners, SomeServiceItems и т.д.

Примеры описания схем [banner](proto/banner.proto), [url](proto/url.proto).

##### Ограничения
Нельзя использовать тип map внутри профилей! Причина - не определён порядок данных в списке при сериализации (и получает большой поток на запись). По этой же причине рекомендуется сортировать списки объектов, если их порядок не определён и не важен.

##### Регистрация протобуф схемы
Для регистрации схемы и генерации трейтов для модели нужно добавить код в
файл [generated/ya.make](generated/ya.make)
```
RUN_PROGRAM(
    ads/bsyeti/caesar/libs/profiles/generated/codegen
        ...
        -p <protofilename>.<messageclass>
        ...

    OUTPUT_INCLUDES
        ...
        ${PROTO_DIR}/<protofilename>.pb.h
        ...

    OUT
        ...
        <protofilename>_traits.h
        ...
)
```

Настоятельно рекомендуется соблюдать лексикографический порядок.
Регистрация протобуфа нужна, чтобы сгенерировать много шаблонного кода для работы с моделью (загрузка/сохранение в YT, получение протобуфа для чтения и изменения) и не писать его руками.

##### Описание модели
Заводим файл `<protofilename>.h` и добавляем в него следующий код:
```c++

#pragma once

#include <ads/bsyeti/caesar/libs/profiles/proto/{protofilename}.pb.h>
#include <ads/bsyeti/caesar/libs/profiles/generated/{protofilename}_traits.h>
#include <ads/bsyeti/big_rt/lib/serializable_profile/serializable_profile.h>

namespace NCSR {
    class T{protofilename}Profile : public NBigRT::TSerializableProfile<{messageclass}Traits> {
        using TBase = TSerializableProfile<{messageclass}Traits>;
    public:
        using TBase::TBase;
        // вспомогательные методы и конструкторы

        // если ключ составной, указываем и для остальных колонок
        TString Get{{key_column_1}}() const {
            return std::get<0>(GetKey());
        }

        // метод, как парсить строковое представление ключа в TKey
        static TKey MakeKeyFromString(TStringBuf key) {
            return TKey{key};
        }
    };
}
```

Добавляем файл `<protofilename>.h` в `all.h`.


##### Синхронизация схем на YT и биндинги к python
Для работы с профилем в Python доступны следуюшие методы:
1. ```"extract_{{profilename}}_profile_proto"```
2. ```"extract_{{profilename}}_profile_proto_as_json"```
3. ```{{profilename}}_table_schema"```

и также через словарь `profiles_spec` по ключу `YtTableName` доступны следуюшие функции:
```
"extract_proto", "extract_proto_as_json", "get_table_schema"
``` 

Далее, добавляем описание схемы таблиц для YT в файле [yt_sync/settings.py](../../tools/yt_sync/settings/tables.py)
В большинстве случаев, будет достаточно воспользоваться функцией `_caesar_simple_table`. Название таблицы указываем такое же, как в протобуфе в `YtTableName`

Далее, в файле [yt_sync/settings.py](../../tools/yt_sync/settings/queues.py) добавляем очередь. В большинстве случаев подойдёт функция `_caesar_simple_queue`.
Очередь стоит стараться именовать так: `{{profilename}}ID`


#### Ограничения

Нельзя пользоваться одновременно serializable profile и ытевым удалением строчек по ttl. Из-за того, что удаление по ttl работает неатомарно, и может быть удалена только база, а патч оставаться, например. И при загрузке такого стейта в полуудаленном состоянии он будет невалидным.

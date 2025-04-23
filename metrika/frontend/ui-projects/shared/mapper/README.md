# mapper

Библиотека экспортирует наружу декоратор `MapRule` и функцию `mapEntity`.

```
mapEntity(entity[, data[, shouldMapFromSnakeCase]]);
```

`@MapRule` добавляет метаданные к классу для привидения типов, а `mapEntity`
инстанцирует класс и насыщает инстанс данными по правилам описанным через
`@MapRule`. Следовательно в `mapEntity` можно передавать сырые данные и получать
на выход типизированный инстанс.

## Использование

Размечаем класс метаданными:

```typescript
import { MapRule } from '@shared/mapper/decorators';
import { ScalarFieldType } from '@shared/mapper/meta';

class UserEntity {
    // поле у которого тип string
    @MapRule(ScalarFieldType.String)
    name!: string;

    // поле у которого тип integer
    @MapRule(ScalarFieldType.Int)
    age!: number;
}
```

Инстанцируем с привидением типов через `mapEntity`:

```typescript
import { mapEntity } from '@shared/mapper/mapper';

const user = mapEntity(UserEntity, { name: 'John', age: '23' });

typeof user.name; // string
typeof user.age; // number
user instanceof UserEntity; // true
```

## `@MapRule`

Кроме типа данных, в который преобразовать поле при вызове `mapEntity`
(`ScalarFieldType`) декоратор принимает объект описывающий поведение mapper'а,
имеет следующие поля:

-   `fromName` - alias для поля в сырых данных, например:

    ```typescript
    import { MapRule } from '@shared/mapper/decorators';
    import { mapEntity } from '@shared/mapper/mapper';

    class UserEntity {
        @MapRule({ type: ScalarFieldType.String, fromName: 'n' })
        name!: string;
    }

    const user = mapEntity(UserEntity, { n: 'John' });
    user.name === 'John'; // true
    ```

-   `isOptional` - является ли поле опциональным: в случае если поле не
    опциоанльное и данные в нем отсутствуют, `mapEntity` кидает исключение:

    ```typescript
    import { MapRule } from '@shared/mapper/decorators';
    import { mapEntity } from '@shared/mapper/mapper';

    class Entity {
        @MapRule(ScalarFieldType.String)
        required!: string;

        @MapRule({ type: ScalarFieldType.String, isOptional: true })
        optional?: string;
    }

    mapEntity(Entity, { required: '1' }); // OK
    mapEntity(Entity, {}); // error
    ```

    По дефолту все поля являются не опциональными

Кроме этого `@MapRule` принимает кастомный mapper:

```typescript
class Entity {
    @MapRule({
        mapper: value => value?.toString().split(','),
    })
    mapped!: string[];
}

const e = mapEntity(Entity, { mapped: '1,2,3' });
e.mapped; // ['1', '2', '3']
```

В значние поля инстанса будет присвоен результат, который вернет кастомный
mapper. В этом случае приведение типов выполнятся не будет (mapper должен
вернуть уже нужный тип данных).

На вход mapper принимает 2 аргумента: данные поля для которого он вызывается и
все данные переданные в `mapEntity`. В примере выше первый арумент - это
`'1,2,3'`, а второй - `{ mapped: '1,2,3' }`.

## Типы данных `ListFieldType`

mapper использует скалярые типы данных:

-   `ScalarFieldType.Boolean` - булевое значение `true` / `false`
-   `ScalarFieldType.Float` - floating point number (64 bit) `parseFloat(...)`
-   `ScalarFieldType.Int` - integer (JS 52 bit) `parseInt(...)`
-   `ScalarFieldType.String` - JS `UTF-16` string

либо массив скалярных данных, например:

```typescript
class Entity {
    @MapRule(ListFieldType.of(ScalarFieldType.Int))
    list!: number[];
}

const e = mapEntity(Entity, { list: ['1', '2', '3'] });
e.list; // [1, 2, 3]
```

В данном случае mapper будет знать, что нужно конвертировать каждый элемент
массива из поля `list` в `integer`.

## snake_case и camelCase

По дефолту `mapEntity` берет данные из полей в snake case и перекладывает в
camel case:

```typescript
class Entity {
    @MapRule(ScalarFieldType.Int)
    fieldName!: number;
}

mapEntity(Entity, { field_name: '1' }); // Entity { fieldName: 1 }
mapEntity(Entity, { fieldName: '1' }); // error: no data
```

Третим аргумнтом в `mapEntity` можно передать флаг, чтобы считывать данные из
полей в camel case:

```typescript
class Entity {
    @MapRule(ScalarFieldType.Int)
    fieldName!: number;
}

mapEntity(Entity, { fieldName: '1' }, false); // Entity { fieldName: 1 }
mapEntity(Entity, { field_name: '1' }, false); // error: no data
```

mapper также поддерживает вложенные entity:

```typescript
class NestedTestEntity {
    @MapRule(ScalarFieldType.Int)
    age!: number;
}

class TestEntity {
    @MapRule(NestedTestEntity)
    nestedTestEntity!: NestedTestEntity;
}

const e = mapEntity(TestEntity, {
    nested_test_entity: {
        age: '59',
    },
});

res.nestedTestEntity.age; // 59
```

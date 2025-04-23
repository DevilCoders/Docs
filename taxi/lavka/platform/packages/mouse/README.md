## Порт Mouse на Python

Основная задача: иметь возможность размечать структуру объектов, а так же
по этой структуре ходить.

```python

from mouse import Mouse, Has


class Foo(Mouse):
    foo = Has(types=(str, int), default=123, required=True)
    bar = Has(types=str, coerce=str)


object = Foo({'foo': 123, 'bar': 345})
object = Foo(foo=123, bar=345)
```

#### Декларация классов

Классы наследуем от `mouse.Mouse`, если необходимо с набором аргументов:


```
from mouse import Mouse

class Foo(Mouse, key='value'):
    ...
```

Все инстанцированные классы имеют заранее предопределённый атрибут `meta`,
через который можно:

1. Получить разметку атрибутов сформированных через `Has`
2. Получить аргументы `key='value'` описания класса

Например:

```
from mouse import Mouse, Has


class StorableUser(Mouse, database='main')
    user_id = Has(str, required=True, coerce=str)
    email = Has(str, required=False)
    nick = Has(str, required=True)


user = StorableUser(
    {
        'user_id': '02ad1542-6213-11eb-9444-43e0810719ac',
        'nick': 'Vasya'
    }
)

user = StorableUser(
    user_id='02ad1542-6213-11eb-9444-43e0810719ac',
    nick='Vasya',
)


for name in user.meta.fields:
    print(name, getattr(user, name))    # user_id ..., nick ...
    print(name, user[name])             # 

print(user.key)     # value
```

Преобразование типов `coerce`.

Если тип, сохраняемый в атрибут не совпадает с типом, указанным
в `Has(types=...)`, и при этом в `Has` определен `coerce`, то функция
`coerce` будет использована для попытки привести тип.

Это один из центральных механизмов зачем вся эта байда, поэтому:

##### Зачем это нужно.

Очень многие сериализуемые объекты при десериализации имеют другой тип,
чем при сериализации.

Например имеем недоработанный до ума драйвер БД (рядовая ситуация), который
пишем не мы. Сохраняет JSON в БД он принимая `dict`, а возвращает строку.

Тогда получается нельзя написать:

```
database.store(user_id=user.user_id, user_data=user.user_data)

...
user = User(database.load(user_id))
```

При записи в БД мы отправляем `dict`, при чтении получаем `str`
(сериализованный JSON), то в определении `user_data` можем просто
написать `coerce`:

```
from mouse import Mouse, Has
import json

class User(Mouse):
    ...

    user_data=Has(dict, coerce=json.loads)
```

И обратное преобразование будет выполнено прозрачно.

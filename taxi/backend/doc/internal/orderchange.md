### Изменение заказа во время выполнения


### Внимание: это общее описание orderchange методов, подробности см. [здесь](https://github.yandex-team.ru/aershov182/backend/tree/orderchange-wip/taxi/client_protocol/protocol_3_0/schema/docs)

### Новые методы

Название | Что делает?
-------- | -----------
[`/changeaction`](#changeaction) | Пользователь нажал на кнопку "Уже выхожу"
[`/changedestinations`](#changedestinations) | Меняет точку Б
[`/changecomment`](#changecomment) | Меняет комментарий к заказу
[`/changeporchnumber`](#changeporchnumber) | Меняет номер подъезда
[`/changepayment`](#changepayment) | Меняет способ оплаты
[`/changes`](#changes) | Возвращает статусы изменений, инициированных в /change* методах

При вызовах всех `/change*` (кроме `/changes`) методов надо передавать
поле `"created_time"`. Если текущее изменение уже было применено с более поздним
`"created_time"`, то бэкенд вернет 409.
`"created_time"` должно быть c timezone (+0000 или +0300 - неважно, главное, чтобы
была timezone).

Если с `"created_time"` все хорошо, то в ответе бэкенд вернет поля "change_id" и "status:
```json
{
    "change_id": "uuid4",
    "status": "success"
}
```
Если `"status": "pending"`, то сервер не смог применить изменение сразу (например,
нельзя сразу сменить способ оплаты). В этом случае по переданному `"change_id"`
можно следить за статусом этого изменения в методе `/changes`.


### Старые методы

Название | Что изменилось?
---------|----------------
[`/launch`](#launch) | Добавился список текущих изменений
[`/taxisearch`](#taxisearchontheway)| Добавились поле с текущими изменениями (`pending_changes`) и поле с возможными изменениями (`allowed_changes`)
[`/taxiontheway`](#taxisearchontheway)| Добавились поле с текущими изменениями (`pending_changes`) и поле с возможными изменениями (`allowed_changes`)


<a name="taxisearchontheway"></a>
##### Поле с текущими изменениями в `/taxisearch` и `/taxiontheway`
```json
{
    "...": "...",
    "pending_changes": [
        {
            "change_id": "7116f3e79bc843a09ef13756b04d19dc",
            "name": "payment",
            "value": "card-012345",
            "status": "pending"
        }
    ],
    "...": "..."
}
```

#### Поле с возможными изменениями в `/taxiontheway`:
В поле `allowed_changes` сервер передает массив возможных действий
по изменению заказа.
Возможные элементы массива и их интерпретации:
* `{"name": "user_ready"}` - можно применять действие "Уже выхожу"
* `{"name": "porchnumber"}` - можно менять номер подъезда
* `{"name": "comment"}` - можно менять комментарий.
* `{"name": "destinations"}` - можно менять пункт назначения
* `{"name": "payment"}` - можно менять способ оплаты.
Если в массиве `allowed_changes` встречается действие с неизвестным
клиенту именем, то это действие надо игнорировать.
Поле `"name"` - обязательное поле в элементе массива. Элемент может
содержать любые другие произвольные поля.
Например, элемент с `{"name": "payment"}` может содержать поле
`"available_methods"` со списком возможных методов оплаты:
```json
{
    "name": "payment",
    "available_methods": ["card"]
}
```

Возможные значения в массиве "available_methods": `"card"` и `"cash"`.

<a name="launch"></a>
#### Список текущих изменений в `/launch`
```json
{
    "...": "...",
    "orders": [
        {
            "orderid": "some_id",
            "due": "some_due",
            "status": "some_status",
            "pending_changes": [
                {
                    "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                    "name": "payment",
                    "value": "card-012345",
                    "status": "pending"
                }
            ]
        }
    ],
    "...": "..."
}
```


### Примеры

Создали заказ в методе `/order`.

<a name="changeporchnumber"></a>
Захотели поменять подъезд в `/changeporchnumber`:
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2013-03-13T09:30:00+0000",
    "porchnumber": "2"
}
```

Получили в ответ 200:
```json
{
    "change_id": "some unique_change_id",
    "status": "success"
}
```


Решили еще раз поменять номер подъезда и по ошибке указали очень старый "created_time":
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2001-03-13T09:30:00+0000",
    "porchnumber": "3"
}
```

Получили в ответ 409, потому что подъезд уже меняли с более новым `"created_time"`:
```json
{}
```



<a name="changecomment"></a>
Захотели поменять комментарий в `/changecomment`:
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2013-03-13T09:30:00+0000",
    "comment": "some comment"
}
```

Получили в ответ 200:
```json
{
    "change_id": "some unique_change_id",
    "status": "success"
}
```

<a name="changeaction"></a>
Передаем информацию, что клиент нажал на кнопку "Уже выхожу" в `/changeaction`:
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2013-03-13T09:30:00+0000",
    "action": "user_ready"
}
```

Получили в ответ 200:
```json
{
    "change_id": "some unique_change_id",
    "status": "success"
}
```


Поняли, что написали не такой комментарий, решили изменить комментарий в
`/changecomment`:
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2013-03-13T09:30:00+0000",
    "comment": "some comment"
}
```

Получили в ответ 406:
```json
{}
```
... потому что заказ перешел в состояние `'transporting'`, а комментарий можно
менять только в `'driving|waiting'` (тем временем в `/taxiontheway['allowed_changes']`
не будет `"name": "comment"`, потому что это изменение больше применять нельзя)


<a name="changedestinations"></a>
Поняли, что хотим уехать в другое место, и меняем точку Б в `/changedestinations`:
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2013-03-13T09:30:00+0000",
    "destinations": [
        {
            "country": "Россия",
            "fullname": "Россия, Москва, 8 Марта, 4",
            "geopoint": [
                33.1,
                52.1
            ],
            "locality": "Москва",
            "porchnumber": "",
            "premisenumber": "4",
            "thoroughfare": "8 Марта"
        }
    ]
}
```

Получили в ответ 200:
```json
{
    "change_id": "some unique_change_id",
    "status": "success"
}
```

<a name="changepayment"></a>
Поняли, что нет денег, и меняем способ оплаты в `/changepayment`:
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2013-03-13T09:30:00+0000",
    "payment_method_id": "card-123456"
}
```

Получили в ответ 200:
```json
{
    "id": "7116f3e79bc843a09ef13756b04d19dc",
    "status": "pending"
}
```

<a name="changes"></a>
Хотим узнать, в каком состоянии находится смена метода оплаты (т.к смена оплаты
процесс небыстрый - надо проверить карту и, если нужно, списать деньги по
алгоритму антифрода) в `/changes`:
```json
{
    "id": "1234567890abcdefghijkl0987654321",
    "orders": [
        {
            "orderid": "some orderid",
            "changes": [
                {
                    "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                }
            ]
        }
    ]
}
```

Получаем в ответ 200:
```json
{
    "orders": [
        {
            "orderid": "some orderid",
            "changes": [
                {
                    "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                    "name": "payment",
                    "value": "card-123456",
                    "status": "pending"
                }
            ]
        }
    ]
}
```

Нам вернулся `"status": "pending"`, значит изменение метода оплаты еще не
закончилось.

Хотим дождаться смены метода оплаты, вызываем `/changes` еще раз и в ответ
получаем 200:
```json
{
    "orders": [
        {
            "orderid": "1234567890abcdefghijkl0987654321",
            "changes": [
                {
                    "change_id": "7116f3e79bc843a09ef13756b04d19dc",
                    "name": "payment",
                    "value": "card-123456",
                    "status": "success"
                }
            ]
        }
    ]
}
```

Нам вернулся `"status": "success"`, значит изменение метода оплаты успешно
закончилось. (Если бы вернулся `"status": "failed"`, это бы значило, что
изменение метода оплаты завешилось не очень успешно)


Опять захотели поменять точку Б:
```json
{
    "id": "some userid",
    "orderid": "some orderid",
    "created_time": "2013-03-13T09:30:00+0000",
    "destinations": [
        {
            "country": "Россия",
            "fullname": "Россия, Москва, 8 Марта, 4",
            "geopoint": [
                33.1,
                52.1
            ],
            "locality": "Москва",
            "porchnumber": "",
            "premisenumber": "4",
            "thoroughfare": "8 Марта"
        }
    ]
}
```

и получили в ответ 406, потому что заказ завершился, а у завершенных заказов
менять параметры нельзя:
```json
{}
```


### Изменения в партнерском протоколе
Тут: https://wiki.yandex-team.ru/taxi/backend/updatepartnersproto-2015-12-01/

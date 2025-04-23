# Админка кэшбэка и кошелька пользователя
Из-за отсутствия истории списаний и пополнений в приложении пользователи часто обращаются с вопросами в поддержку. У поддержки нет инструментов диагностики кэшбэка, поэтому все вопросы прилетают к нам в duty.

Поддержке важно иметь доступ к 4 вещам:
1. Список кошельков пользователя с балансами
2. История операций по кошельку
3. Рассчитанный кэшбэк за конкретный заказ
4. Начисленный кэшбэк за конкретный заказ

## Список кошельков пользователя
```
# Кошельки

yandex_uid: 1234567 Валюты: RUB, EUR       [Find]
            -------         --------  

## Основные кошельки
+------------------------------+
|Wallet ID: wallet_id/1234567  |
|Баланс: 1234 ₽                |
|                              |
|[История операций]            |
+------------------------------+
+------------------------------+
|Wallet ID: wallet_id/1234567  |
|Баланс: 5 €                   |
|                              |
|[История операций]            |
+------------------------------+


## Связанные кошельки (не отображаются в приложении)
+------------------------------+
|Wallet ID: wallet_id/76541    |
|Баланс: 0 ₽                   |
|                              |
|[История операций]            |
+------------------------------+
+------------------------------+
|Wallet ID: wallet_id/54322    |
|Баланс: 0 ₽                   |
|                              |
|[История операций]            |
+------------------------------+

```

Поддержка обычно оперирует либо конкретным user_id, либо номером телефона пользователя. Поэтому точкой входа в интерфейс админки кошельков станет страница ["Пассажиры"](https://tariff-editor.taxi.yandex-team.ru/passengers) в админке, где к карточке добавится ссылка "Кошельки пользователя", ведущая на страницу админки кошельков с заполненным yandex_uid.  

![](https://jing.yandex-team.ru/files/danielkono/Data.25ab20c.png.b54a5f4.jpeg)

Фронт админки кошельков получает информацию о yandex_uid и связанных yandex_uid из ручки залогина [`/admin/uid-info`](https://github.yandex-team.ru/taxi/uservices/blob/758a164feed81f068225d9d698990d79228dd204/services/zalogin/docs/yaml/api/admin.yaml#L11) и отправляет в ручку сервиса `personal-wallet`

```
GET /v1/admin/wallets?
    yandex_uid=123456&
    currencies=RUB,EUR  // optional
```

Ручка работает аналогично ручкам /balances и /available-accounts — получает список кошельков из базы, запрашивает в биллинге балансы и возвращает результат клиенту.
Связанные uidы запрашиваются в ручке /internal/uid-info сервиса zalogin.


```yaml
{
    "wallets": {
        "main": [
            {
                "wallet_id": "wallet_id/123456",
                "balance": "1234",
                "currency": "RUB",
                "yandex_uid": "123456"
            },
            {
                "wallet_id": "wallet_id/123456",
                "balance": "1234",
                "currency": "EUR",
                "yandex_uid": "123456"
            },
        ],
        "bound": [ # optional
            {
                "wallet_id": "wallet_id/76541",
                "balance": "0",
                "currency": "RUB",
                "yandex_uid": "76541"
            },
            {
                "wallet_id": "wallet_id/54322",
                "balance": "0",
                "currency": "RUB",
                "yandex_uid": "54322"
            },
        ]
    }
}
```


## История операций по кошельку
```
+------------------------------+
|Wallet ID: wallet_id/1234567  |
|Баланс: 1234 ₽                |
+------------------------------+

С  2019.11.01 00:00  По  2020.03.25 23:59:59   по Москве
   ----------------      -------------------

2020.03.25 10:00
+124 ₽
Сервис: Такси
Заказ: 8a8fad05d21d279eafac82982f879b68

2020.03.25 10:00
-145 ₽
Сервис: Еда
Заказ: 7a8fad05d21d279eafac82982f879b68

2020.03.25 10:00
+155 ₽
Сервис: Афиша
Заказ: 1245321

```

```
GET /v1/admin/transactions?
    wallet_id=wallet_id/12345&
    yandex_uid=12345&
    begin_at=2019-11-01T00:00:00+03:00&
    end_at=2020-03-25T23:59:59+03:00&
    cursor=cursor0& // optional
    limit=3 // optional
```

```yaml
{
    "transactions": [
        {
            "event_at": "2020-03-25T10:00+03:00",
            "amount": "124",
            "type": "income",
            "currency": "RUB",
            "service": "taxi",
            "order_id": "8a8fad05d21d279eafac82982f879b68",
        },
        {
            "event_at": "2020-03-25T10:00+03:00",
            "amount": "145",
            "type": "expense",
            "currency": "RUB",
            "service": "eda",
            "order_id": "7a8fad05d21d279eafac82982f879b68",
        },
        {
            "event_at": "2020-03-25T10:00+03:00",
            "amount": "155",
            "type": "income",
            "currency": "RUB",
            "service": "afisha",
            "order_id": "1245321",
        }
    ],
    "cursor": "cursor1"
}
```

Ручка проксирует запрос в ручку [`/statement`](https://st.yandex-team.ru/TAXIBILLING-2772) сервиса `billing-wallet`


## Размер кэшбэка на странице заказа
На странице заказа нужно отображать:
1. Коэффициент кэшбэка за скидку по order_rate
2. Коэффициент кэшбэка за Плюс по order_rate
3. Рассчитанный кэшбэк по order_clear
4. Начисленный кэшбэк по данным биллинга

Информация о кэшбэке может лежать в архиве — это значит, что её получение может занять секунды.  
Чтобы не блокировать отображение основной информации о заказе, мы не будем добавлять информацию о кэшбэке в ответ ручки `/v1/order/get/{order_id}` сервиса `admin-orders`.  

Вместо этого в ответ ручки `/v1/order/get/{order_id}` добавится флаг `is_cashback`, который будет получаться из одноимённого флага в order_proc. 
```yaml
{
    ...
    "order_info": {
        ...
        "is_cashback": true  # optional
        ...
    }
    ...
}
```
Фронт при наличии этого флага будет делать запрос в ручку информации о кэшбэке:
```
GET /v1/admin/cashback?order_id={order_id}
```
```yaml
{
    "cashback": {
        "rates": { # optional
            "discount": "0.2",  # optional
            "ya_plus": "0.1",  # optional
        }
        "calculated": "20",  # optional
        "paid": "0",  # optional
        "cleared_value": "1000" # optional
    }
}
```
Если заказ без кэшбэка, вернётся пустой ответ:
```yaml
{
    "cashback": {}
}
```

Ручка будет использовать archive-api для получения `order_proc`.

### Коэффициенты кэшбэка
Ручка будет доставать коэффициенты кэшбэка из базы или архива и матчить их с переданным тарифом.
Если коэффициенты ещё не зарегистрировались, объект коэффициентов будет пустым.

### Рассчитанный кэшбэк
Размер рассчитанного кэшбэка будет вычисляться на основе значения колонки `cashback_sum` из таблицы `order_clears`.  
Если клиров нет в таблице, ручка будет пытаться восстановить их из архива.  
Если клира ещё не случилось, поля `"calculated"` и `"cleared_amount"` не придут в ответе.

### Начисленный кэшбэк
Надёжно узнать, сколько кэшбэка было начислено за заказ можно только в биллинге.   
Для этого в сервисе `billing-wallet` появится ручка `/order` для получения транзакций, связанных с заказом.   
[TAXIBILLING-3014](https://st.yandex-team.ru/TAXIBILLING-3014)  

Ручка требует в запросе order_id, service, yandex_uid и wallet_id.

order_id мы получим из запроса, service всегда будет равен сервису Яндекс Такси. 
Не хочется ради yandex_uid ходить в архив, поэтому в таблицу order_clears будет добавлено необязательное поле `yandex_uid`.  

Осталось получить wallet_id.
Мы не храним связь начисленного кэшбэка за заказ и кошелька, поэтому сервис кэшбэка будет 
1. Получать кошельки пользователя из ручки `/balances` сервиса `personal-wallet`
2. Определять подходящий кошелёк по валюте и использовать его id для запроса в billing-wallet
3. Получать транзакции из billing-wallet и суммировать их.

Если транзакций по заказу ещё не было, поле `"paid"` не придёт в ответе.  


Ограничения:  
Если у пользователя поменяется кошелёк с момента заказа, мы не сможем получить список транзакций.   
Таким образом, для заказов, сделанных до перехода на billing-wallet это не будет работать.
В order_clears старых заказов также не будет записываться yandex_uid, поэтому получить транзакции не получится.

## Sequence diagram
![](https://wf.yandex-team.ru/plantuml/hLJDYjim4BxhAGQVrmcz1jhkfVJOGdiFOrlDcbKSOJjnIrZ8p_O7kYtqJR8B8McoILv1UgEEf3YrMMzBeJOu8yqtCzyt8-Kyop7DXtq18MON0OQN_Y2DUEfBx77693dZC9QOv831PMrT1jGsFKp3YtZ4VPIn1vZ1SSqYp370Z9_2kh9NZvGypGO92hz08NXkesLHnmIn477IgqA2WZ56tC1_TihT0Szx-U8jj4TFsXZruwHTUfvRTTquUZekhIlFOwNR93aoxe0wgBtQwhd-hDPwfc_0HSXq4B8Zg5wqugych2X-D6cAESzO1TcKsO6IGSv1y7Sv0thKKa_LLgr1RTHUVzFN-feIVr9hjLGxFQDYTw1sX9g1iMxLGgtKyWnSi25pq1FwtXgaMbXAPEprbDuPeNVMuRXIrXKGQA8_aadmbar33EvjQAcfcOl-QWk2IKirr-IVCvv4O1JzSyT2mJ7zMySSwDGnUD0o-Y4gYwOM_PyEDGkKXJcYhr-zSMSqG859o3CwYRAewo2g1yezfHeRrzSlrCsjlZ6sklkjhVF861pyXuaspJUSQFsTc2zhb09BwK6pQ_LfPs85h-YxiPFzwTAMb-aCFc0IyVVTeR7TDRNR6Kz7SSX9OV0dXKqLgXhTBAZnSz9wRuTtcahz5WVsNs3ibPjU1yQjLklANFTp6af_ADWl)

# Этапы
1. Список кошельков
- Задача на фронтов
- Ручка списка кошельков для админки
2. История транзакций
- Задача на фронтов
- Ручка истории транзакций для админки
3. Кэшбэк на странице заказа
- Задача на фронтов
- Флаг is_cashback в ответе ручки /order сервиса admin-orders
- Записывать yandex_uid в order_clears и реплицировать его
- Ручка для информации о кэшбэке
- Дождаться ручки в billing-wallet для получения транзакций по заказу ([TAXIBILLING-3014](https://st.yandex-team.ru/TAXIBILLING-3014))

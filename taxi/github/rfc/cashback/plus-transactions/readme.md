# Начисление/рефанд баллов Плюса

## Введение
Сейчас логика начисления баллов/кэшбэка реализована как минимум в 3-х сервисах: cashback-int-api, personal-goals, cashback, и требуется еще в одном новом сервисе cashback-levels.  

Для предоставления единого интерфейса начисления/рефанда баллов Плюса планируется создать новый сервис plus-transactions, который можно будет переиспользовать везде, где это нужно, включая сервисы, упомянутые выше.

## Алгоритм начисления/рефанда
Добавляем 2 ручки и одну stq-таску:
1. /cashback/status - ручка получения статуса начисления кэшбэка
2. cashback_processing - stq-таска начисления/возврата кэшбэка
3. /cashback/update - ручка, которая вызывает stq-таску cashback_processing

### Ручка ___/cashback/status___:
- Нужна для получения статуса начисления кэшбэка по ключу идемпотентности (id заказа, цели, компенсации, whatever) и namespace ключа (personal-goals, cashback-int-api, etc.), который передается в transactions
- Возвращает сколько уже начислено баллов, есть ли операции в прогрессе, список операций, версию (вероятно, респонс будет меняться в процессе)
- Версия нужна для разрешения гонок и передается в ручку ___/cashback/update___

#### Флоу работы ручки ___/cashback/status___:
- Ручка ходит в сервис transactions-ng в ручку ___/v2/invoice/retrieve___ для получения инвойса, используя ключ идемпотентности в качества invoice_id и namespace
- Если ручка ___/v2/invoice/retrieve___ ответила кодом 404, значит инвойса не создавали по данному ключу идемпотентности, и в ручке ___/cashback/status___ вернем:
```json5
// 200 OK
{
    "status": "done", 
    "amount": "0", // начисленный кэшбэк
    
    // статус в разбивке по операциям
    "operations": [], 
    
    // версия для разрешения гонок
    "version": 1 
}
```
- Если ручка ___/v2/invoice/retrieve___ вернула инвойс, сможем получить из него информацию о том, сколько баллов уже зачислено, в каком статусе находится инвойс, список операций и версию инвойса для разрешения гонок
- Возвращает эту информацию в ручке

#### На подумать
Возможно, стоит добавить в запрос возможность уточнить, какие данные инвойса нужны, что-то типа фильтров, чтобы разные потребители могли сами задавать в запросе то, что им нужно. 

#### Request ручки __/cashback/status__:
```json5
// body
{
    "ext_ref_id": "какой-то уник id (заказа, цели, компенсации, whatever)",
    "namespace": "namespace ключа (personal-goals, cashback-int-api, etc.)"
}
```

#### Response ручки __/cashback/status__:
```json5
{
    "status": "processing", // статус последней операции
    "amount": "100", // начисленный кэшбэк
    
    // статус в разбивке по операциям
    "operations": [
      {
        "operation_id": "<topup_id>",
        "status": "done",
      },
      {
        "operation_id": "<refand_id>",
        "status": "failed",
      },
      {
        "operation_id": "<refand_id>",
        "status": "processing",
      }], 
    
    // версия для разрешения гонок
    "version": 3
}
```

### stq-таска cashback_processing
- Нужна для начисления/рефанда баллов на кошелек пользователя

#### Флоу работы таски:
1. Идем в сервис plus-wallet с yandex_uid и currency за кошельком пользователя. Если у пользователя еще нет кошелька, создаем новый
2. Проверяем, не создан ли уже инвойс с id=<ext_ref_id> и id_namespace=<namespace из запроса> (/v2/invoice/retrieve)
3. Если инвойса нет, создаем новый инвойс (/v2/invoice/create).
Если в ответе получили статус 409 (Invoice exists and does not match current request), значит, произошла гонка и инвойс был создан в другом месте (вероятно, в параллельной stq-таске, а может и нет). В таком случае делаем reschedule таски.
4. Проверяем, что никакая другая операция по найденному инвойсу не выполняется. Если выполняется, делаем reschedule таски
5. Если сумма баллов меньше, чем в инвойсе, значит это рефанд
6. Дальше нужно запустить операцию начисления или рефанда через ручку ___/v2/cashback/update___

#### На подумать
Может стоит в самом сервисе проверять, есть ли у пользователя подписка Плюса (has_plus)

#### Схема stq-таски (аргументы)
```json5
{
    "ext_ref_id": "какой-то уник id (заказа, цели, компенсации, whatever)",
    "namespace": "namespace ключа (personal-goals, cashback-int-api, etc.)",
    "billing_service": "billing service to pass to transactions on invoice creation",
    "service_id": "id сервиса, который начисляет",
    "yandex_uid": "id пользователя, которому начисляем",
    "currency": "валюта кошелька начисления",
    "version": 0,  // версия для обхода гонок, которую возвращает ручка /cashback/status
    "amount_by_source": {
      "<source>": {
        "amount": "100",
        "payload": {
          "cashback_service": "yataxi",
          "cashback_type": "transaction",
          "product_id": "levels_goal_reward",
          "service_id": "billing service id",
          "issuer": "taxi",
          "campaign_name": "levels",
          "ticket": "NEWSERVICE-1234",
          "has_plus": "true",
          // optional params
          "order_id": "order id for taxi cashback",  // assume not applicable by default
          "base_amount": "order base amount for taxi cashback"  // assume not applicable by default
        }        
      }
    },
  
    // optional args
    "user_ip": "user ip address if exists"
}
```

### Ручка ___/cashback/update___:
- Нужна для вызова stq-таски начисления/рефанда баллов Плюса на кошелек пользователя

#### Флоу работы ручки:
- Ставим stq-таску начисления баллов с task_id=<ext_ref_id>_{version} (для обеспечения уникальности task_id)

#### На подумать
Может можно было бы сделать биллинговую инфу и payload optional аргументами и добавить их в конфиг для каждого сервиса.  
Это могло бы быть удобно для сервисов, которые делают все свои начисления с одной и той же биллниговой инфой и payload-ом, например personal-goals.  

#### Request ручки ___/cashback/update___:

```json5
// body
{
    "ext_ref_id": "какой-то уник id (заказа, цели, компенсации, whatever)",
    "namespace": "namespace ключа (personal-goals, cashback-int-api, etc.)",
    "billing_service": "billing service to pass to transactions on invoice creation",
    "service_id": "id сервиса, который начисляет",
    "yandex_uid": "id пользователя, которому начисляем",
    "currency": "валюта кошелька начисления",
    "version": 0,  // версия для обхода гонок, которую возвращает ручка /cashback/status
    "amount_by_source": {
      "<source>": {
        "amount": "100",
        "payload": {
          "cashback_service": "yataxi",
          "cashback_type": "transaction",
          "product_id": "levels_goal_reward",
          "service_id": "billing service id",
          "issuer": "taxi",
          "campaign_name": "levels",
          "ticket": "NEWSERVICE-1234",
          "has_plus": "true",
          // optional params
          "order_id": "order id for taxi cashback",  // assume not applicable by default
          "base_amount": "order base amount for taxi cashback"  // assume not applicable by default
        }        
      }
    },
  
    // optional args
    "user_ip": "user ip address if exists"
}
```

Response ручки ___/cashback/update___:
```json5
// 200 OK
{}

// 500
{ 
  "code": "500",
  "description": "Internal Server Error"
}

```

## Заметки по переводу существующих сервисов

### personal-goals
Кажется, что простой перевод, так как логика начисления почти полностью совпадает.  
Надо будет просто заменить в stq-таске вызовы plus-wallet и transactions-ng вызовами ручек нового сервиса.

### cashback-int-api
Кажется, что перевод ручки /cashback-int-api/cashback/retrieve должен быть простым.  
Насчет ручки /cashback-int-api/cashback/update не так очевидно, так как сейчас начисление выполняется синхронно в ручке, которая возвращает разные коды ответа в зависимости от статуса.  

В новом сервисе начисление происходит асинхронно в stq-таске, поэтому надо подумать/узнать, можно ли перевести потребителей cashback-int-api на новое асинхронное API.   
Еще желательно будет добавить возможность задавать нужные поля ответа для ручки **/cashback/status**, потому что cashback-int-api в ответе возвращает статусы начислений в разбивке по операциям, а это нужно не всем потребителям.

### cashback (cashback_charge_processing)
Нужно будет:
1. Добавить в ручку **/cashback/update** аргументы:
   - инстанс transactions, который использовать для начислений (eda, taxi, ng)
   - payment_methods_blacklist
   - cashback_item_ids
2. Добавить в респонс ручки **/cashback/status** дополнительные поля, которые можно задавать в запросе:
   - flattened held and cleared, payment_types и еще некоторые
3. Кажется, что логику ретраев и stq callback-ов потребителей можно будет в 1й итерации оставить в cashback-е
4. TODO что-то еще?

Не обязательно сразу, но было бы хорошо перенести, чтобы было доступно всем потребителям:
1. Логику ретраев
2. stq callback-и потребителей

## Предварительная оценка по времени

### MVP для Уровней:
[1-2d] Заведение нового сервиса plus_transactions (арх-сек-ревью + заведение окружения). Планируется заводить сервис в uservices

[1-2d] Реализация ручки ___/cashback/status___

[1d] Реализация ручки ___/cashback/update___

[3d] Реализация stq-таски ___cashback_processing___

Итого, ориентировочно: 6-8 дней

### 2-я итерация (перевод cashback-а):
TODO
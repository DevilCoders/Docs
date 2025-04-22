# Выдача промокодов от лица ресторанов

## Проблемы:
Рестораны должны уметь сами выдавать промокоды пользователям.
Для выдачи ресторанами промокодов нужно иметь дополнительную информацию в сервисе eats-coupons. При этом будет одна серия промокодов для всех ресторанов.

1. Нужно иметь данные о том, какой ресторан выдал промокод. Данные нужны в виде списка `place_id`, в которых можно применить промокод.
2. Нужно уметь валидировать промокод по списку `place_id`, которые были указаны при генерации промокода
3. Нужно уметь переопределять описание промокода для каждого генерируемого промокода (пока не сделано)
4. В списке промокодов нужно уметь возвращать данные о том, был ли этот промокод выписан рестораном

## Решение

Можно разработать общее решение для типовых задач с валидацией промокода по информации, которая передается при генерации промокода. Общий флоу будет такой:
1. В ручку генерации передаются данные, которые будут использоваться для валидации в ручке чека.
2. Мы сохраняем эти данные в монге. Для этого используем поле `promocode_meta`, в котором будут храниться данные в формате, аналогичном `series_meta` из серии промокода.
3. В `series_meta` серии будет флаг, например, `db_validation`, который будет показывать, что данные для валидации конкретного промокода нужно взять из базы.
4. В ручке валидации мы смотрим, возведен ли флаг, и, если да, то донасыщаем поле `series_meta` данными из базы.
5. Так как мы донасытили данные `series_meta`, то валидаторы будут автоматически подхватывать их и валидировать по нужным данным в `payload`.

### База данных для хранения информации для валидации промокода



```yaml
description: Данные о промокодах, выданных рестораном
settings:
    collection: sample
    connection: sample
    database: sample
indexes:
  - key: promocode
    unique: true
  - key: updated_at
  - key: expire_at  # для архивации документов
jsonschema:
    properties:
        _id:
            description: Генерируется Mongo, в коде не используется
            type: object_id
        promocode: 
            description: Промокод
            type: string
        promocode_meta:
            description: |
                Данные для валидации промокода. Имеют тот же формат, что и в серии.
            type: object
            additionalProperties: true
        updated_at:
            type: datetime
        expire_at:
            description: |
                Время протухания промокода.
            type: datetime
    required:
      - _id
      - promocode
      - updated_at
      - promocode_meta        
```            

Нужно настроить архивацию по полю `expired_at`. Архивацию можно проводить раз в неделю, ttl можно выставить в 1 день.

### Изменения в ручке генерации

Нужно добавить в ручку информацию, которая будет содержать дополнительные данные для валидации:
```yaml
        PromocodeMeta:            
            additionalProperties: true
            type: object
```

Этот объект кладем в боди запроса на генерацию:
```yaml
        GenerateRequest:
            additionalProperties: false
            type: object
            required:
              - token
              - promocode_type
              - conditions
            properties:
                personal_phone_id:
                    type: string
                    description: |
                        id номера телефона пользователя, опциональное.
                        Если пришло, то ограничиваем использование промокода
                        только пользователем с этим personal_phone_id.
                        Нужно для поддержки выдачи промокода по номеру
                        телефона через админку.
                        Не ожидается, если пришел yandex_uid.
                yandex_uid:
                    type: string
                    description: |
                        id пользователя, кому выдаёт, опциональное.
                        Если пришло, то добавляем в список промокодов
                        пользователя.
                        Не ожидается, если пришел phone_id.
                application_name:
                    description: |
                        Название приложения пользователя iphone|uber_android|...
                        Если в запросе есть yandex_uid, то либо application_name,
                        либо brand_name должны быть указаны.
                    type: string
                brand_name:
                    type: string
                    description: |
                        Бренд приложения пользователя yataxi|yauber|yango|...
                        Если в запросе есть yandex_uid, то либо application_name,
                        либо brand_name должны быть указаны.
                token:
                    type: string
                    description: токен идемпотентности
                promocode_type:
                    type: string
                    description: тип промокода, например sorry, welcome, etc.
                value:
                    type: integer
                    description: |
                        Сумма скидки для серий с варьируемой стоимостью,
                        обязательный параметр для данных серий
                    minimum: 0
                reason:
                    description: Причина выдачи промокода пользователю
                    $ref: '../definitions.yaml#/components/schemas/LocalizableString'
                expire_at:
                    description: Время окончания действия промокода
                    type: string
                    format: date-time
                conditions:
                    $ref: '#/components/schemas/Conditions'
                promocode_meta:
                    description: |
                        Дополнительные данные для валидации. Сохраняются в базу, для использования нужен флаг в series_meta в чеке.
                    $ref: '#/components/schemas/PromocodeMeta'
```                    

В логику ручки нужно добавить функциональность, которая в случае успешной генерации промокода положит данные для валидации в монго коллекцию.

### Добавление логики валидации по данным, переданным при генерации

До валидации промокода:

Для того, чтобы понимать во время валидации промокода, что он нуждается в донасыщении данными из базы, нужно в мете серии промокода иметь такую галочку, например, `db_validation`.

Если возведен такой флаг, то идем в базу по промокоду и достаем оттуда поле `promocode_meta` и мерджим его в поле `series_meta`.

Далее при валидации будут учитываться дополнительные данные, которые мы достали из базы.

### Изменения в ручке списка промокодов

#### Переопредение описания промокода

?

#### Добавление информации о том, что промокод выписан рестораном

**Изменения в api ручки**

Объекту купона, список которых возвращается из ручки, добавляем поле `business_type`. Это поле задается при заведении серии промокодов. В сервисе уже есть функционал, который умеет доставать его для ручки чека и резерва из `series_meta`, нужно будет только начать доставать его теперь и в ручке списка.

```yaml
        UserPromocode:
            type: object
            additionalProperties: false
            properties:
                code:
                    type: string
                is_used:
                    type: boolean
                discount:
                    type: integer
                percentage:
                    type: boolean
                description:
                    type: string
                currency:
                    type: object
                    additionalProperties: false
                    properties:
                        code:
                            type: string
                        sign:
                            type: string
                    required:
                      - code
                      - sign
                expired_at:
                    type: string
                    format: date-time
                status:
                    type: string
                    description: Статус валидации промокода
                    enum:
                      - valid
                      - invalid
                      - restricted
                business_type:
                    description: |
                        Метка, которая семантичеки относится к бизнесу.
                    example: "place_discount"
                    type: string                    
            required:
              - code
              - is_used
              - discount
              - percentage
              - currency
              - status
```

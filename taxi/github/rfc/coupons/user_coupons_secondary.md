# coupons_list to secondary

### Проблема
Сейчас мы ходим только в мастер базу dbcoupons. Два инстанса(реплики) простаивают.

### Задача
На запросах чтения ходить в реплику, если это возможно.

### Мотивация
Улучшение работоспособности dbcoupons.

### Решение

Будет добавлено новое опциональное поле *version* в запросы и ответы ручек
1) */v1/coupons/activate*
2) */v1/coupons/deactivate*
3) */v1/coupons/list*

```
version:
    description: Строка версии
    type: string
```
Клиент должен будет хранить последнее значение *version* и посылать его при походах в ручки */v1/coupons/list*, */v1/coupons/deactivate*, */v1/coupons/activate*.

Само поле *version* - это закодированная с помощью crypto::base64::Base64Encode строка, которая содержит в себе пары yandex_uid-version. Эта пара означает, что запись в таблице dbcoupons.user_coupons с таким yandex_uid имеет версию version. Таким образом незакодиранное поле *version* будет иметь следующий вид:

`"<yandex_uid>:<version>,<yandex_uid>:<version>,..." `

### Алогритм работы на беке

В *list* при чтении из dbcoupons.user_coupons
1. Создаем квери, у которой для тех yandex_uid, которые пришли в *version*, версии документов >= версии в *version*, а для всех остальных yandex_uid версии документов >= 0 
2. Делаем запрос на чтение в реплику с такой кверей.
3. Если хотя бы для одного yandex_uid из *version* не пришел документ, то делаем аналогичный запрос в мастер
4. Отдаем новое поле *version*. Получаем его по документам, которые пришли из реплики и мастера.

В *activate*, *deactivate* при записи/обновлении dbcoupons.user_coupons надо обновить поле *version*. У yandex_uid, к которому была кверя записи/обновления, надо обновить версию. Для этого надо сделать дополнительный поход в мастер за документом с таким yandex_uid.

### API

- `/v1/coupons/activate`

    Поле *version* будет влиять на походы в реплику/master при получении промокодов пользователя. Основная логика ручки не меняется.

    В API запроса добавляем опционально поле *version*.
    
    ```
    ActivateRequest:
        allOf:
          - type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: |
                "additionalProperties" must be true for "allOf"
            properties:
                code:
                    type: string
                    description: промокод
                yandex_uids:
                    type: array
                    items:
                        type: string
                    description: список yandex_uid привязанный к данному аккаунту
    +           version:
    +               type: string
    +               description: строка версии user_coupons на клиенте
            required:
              - code
              - yandex_uids
          - $ref: 'coupons/definitions.yaml#/definitions/BaseCheckableRequest'
    ```
    В API ответа добавляем обязательное поле *version*. 
    
    ```
    ActivateResponse:
        type: object
        additionalProperties: false
        properties:
            coupon:
                $ref: 'coupons/definitions.yaml#/definitions/Coupon'
    +       version:
    +           type: string
    +           description: строка версии user_coupons после активации
        required:
          - coupon
    +     - version
    ```

- `/v1/coupons/deactivate`

    Поле *version* будет влиять на походы в реплику/master при получении промокодов пользователя. Основная логика ручки не меняется.

    В API запроса добавляем опционально поле *version*.
    
    ```
    name: body
    required: true
    description: тело запроса
    schema:
        type: object
        additionalProperties: false
        properties:
            code:
                description: Уникальный код промокода для удаления
                type: string
                yandex_uids:
                    description: Список из yandex_uid, у которых нужно деактивировать промокод
                    type: array
                    items:
                        description: yandex_uid
                        type: string
                application_name:
                    description: Название приложения
                    type: string
    +           version:
    +               type: string
    +               description: строка версии user_coupons на клиенте
        required:
            - code
            - yandex_uids
            - application_name
    ```
    В API ответа появляется обязательное поле *version*. 
    
    ```
            responses:
                '200':
                    description: OK
    +               schema:
    +                   $ref: '#/definitions/DeactivateResponse'
    ...
    definitions:
    +   DeactivateResponse:
    +   type: object
    +   additionalProperties: false
    +   properties:
    +       version:
    +           type: string
    +           description: обновленная строка версии user_coupons
    +   required:
    +     - version
    ```

- `/v1/coupons/list`

    Поле *version* будет влиять на походы в реплику/master при получении промокодов пользователя. Основная логика ручки не меняется.

    В API запроса добавляем опционально поле *version*.
    
    ```
        ListRequest:
        allOf:
          - type: object
            additionalProperties: true
            x-taxi-additional-properties-true-reason: |
                "additionalProperties" must be true for "allOf"
            properties:
                yandex_uids:
                    type: array
                    items:
                        type: string
                    description: список yandex_uid привязанный к данному аккаунту
                services:
                    type: array
                    minItems: 1
                    x-taxi-cpp-type: std::unordered_set
                    items:
                        type: string
                    description: Сервисы, хотя бы к одному из которых должен принадлежать
                        промокод, чтобы попасть в ответ. По умолчанию -  ['taxi']
                    example: ['taxi', 'lavka', 'eda']
        +       version:
        +           type: string
        +           description: строка версии user_coupons на клиенте
            required:
              - yandex_uids
          - $ref: 'coupons/definitions.yaml#/definitions/BaseCheckableRequest'
    ```
    В API ответа добавляем обязательное поле *version*. 

    ```
    ListResponse:
        type: object
        additionalProperties: false
        properties:
            coupons:
                type: array
                items:
                    $ref: 'coupons/definitions.yaml#/definitions/Coupon'
            ui:
                type: object
                additionalProperties: false
                properties:
                    splitters:
                        type: array
                        items:
                            $ref: 'coupons/definitions.yaml#/definitions/Splitter'
                        description: ui разделители промокодов разных сервисов
                required:
                  - splitters
    +       version:
    +           type: string
    +           description: обновленная строка версии user_coupons
        required:
          - coupons
    +     - version
    ```

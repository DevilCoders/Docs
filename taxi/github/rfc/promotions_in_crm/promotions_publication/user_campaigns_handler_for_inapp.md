## Проверка попадания пользователя в кампанию

Проверять, попадает ли пользователь в кампанию, будем в сервисе `inapp-communications`.
Для проверки будем вызывать новую ручку в сервисе `communications-audience`:

```
/communications-audience/v1/get_campaigns:
    post:
        description: |
            Ручка, получающая кампании, в которые попадает пользователь.
            Если кампании найдены по любому из идентификаторов пользователя - 
            ответ будет содержать список меток кампаний.
            Пользователь может не попадать ни в одну из кампаний.
            Тогда ответ будет содержать пустой список.
          - in: body
            name: body
            schema:
                type: object
                additionalProperties: false
                required:
                  - user
                properties:
                    user:
                        $ref: '#/definitions/User'
                        
        responses:
            '200':
                description: OK
                schema:
                    type: object
                    additionalProperties: false
                    properties:
                        campaigns:
                            type: array
                            description: список кампаний, в которые попадает пользователь
                            items: 
                                type: string
                    required:
                      - campaigns

definitions:
    User:
        type: object
        description: | 
            Объект для идентификаторов, определяющих пользователя.
            Все идентификаторы являются опциональными, 
            кампании могут храниться по любому из них.
        additionalProperties: false
        properties:
            yandex_uid:
                description: yandex uid пользователя
                type: string
            phone_ids:
                description: список phone id пользователя
                type: array
                items: 
                    type: string
            personal_phone_ids:
                description: список personal phone id пользователя
                type: array
                items: 
                    type: string
            device_ids:
                description: список device id пользователя
                type: array
                items: 
                    type: string
```

Для того, чтобы после получения ответа от `communications-audience` можно было получить коммуникации для пользователя, 
в кэше коммуникаций для коммуникаций должна храниться метка кампании (для тех коммуникаций, для которых она есть).

Сейчас кэш коммуникаций (`communications-cache`) периодически забирает фуллскрины из 
`/internal/promotions/list` сервиса `promotions`. 
На первый взгляд, фуллскрины хранятся и прокидываются дальше в том виде, 
в котором они вернулись в ответе `promotions`, поэтому достаточно будет добавить в этот ответ метку кампании.

```
Fullscreen:
        type: object
        properties:
            id:
                type: string
            ...
            campaign_id:
                type: string
                description: метка маркетинговой кампании, по которой раскатан фуллскрин
        required:
          - id
          - zones
          - screen
          - priority
          - pages
          - start_date
          - end_date
          - options
        additionalProperties: false
```

### Реализация

Ручка должна будет получить из базы `communications-audience` все кампании, в которые попадает пользователь.
Для этого надо будет извлечь из PA контекста все используемые CRM идентификаторы пользователя
(`yandex_uid`, `phone_id`, `personal_phone_id`, `device_id`) и сделать в базу запрос, извлекающий метки кампаний по идентификаторам. 

### Использование

На этапе MVP ручка будет использоваться только для поиска фуллскринов. 
Нужно вызвать её в `/4.0/promotions/v1/list` до поиска коммуникаций в кэше.
Поиск в кэше нужно доработать так, чтобы он умел извлекать фуллскрины и по меткам кампаний.

### Нагрузка и тайминги

На этапе MVP нагрузка будет соответствовать нагрузке на ручку `/4.0/promotions/v1/list` 
сервиса `inapp-communications`. Сейчас это обычно до 800 rps. 

Вся логика ручки - извлечение идентификаторов из PA и запрос или запросы в YDB. 
Долгих операций не ожидается. Пока ориентируюсь на ответ в пределах 50мс, но рассчитываю, что будет меньше.

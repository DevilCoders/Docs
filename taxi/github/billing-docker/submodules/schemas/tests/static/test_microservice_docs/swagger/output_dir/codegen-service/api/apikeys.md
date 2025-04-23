#[codegen-service](./../../../Index/#codegen-service) > api > apikeys
**TaxiFleet.API**


## /api/v1/apikeys/key
### Допустимые параметры запроса (post)




* _Header_:
    * __X-Park-Id__ <code style="color: Green">required</code> `type: string` 
* _Query_:
    * __id__ <code style="color: Green">required</code> `type: integer` key id

### Допустимые параметры ответа

* **200**: Key object
    *  <code style="color: Green">required</code> `type: object` key object
        * __client_id__  `type: string` client id (contains only latin letters, digits and hyphnes)
        * __comment__  `type: string` text comment
        * __created_at__  `type: string` date in ISO 8601O format
        * __id__  `type: integer` client or key db id
        * __permissions__  `type: array` granted permissions for the key
            * _Элементы массива:_
                *   `type: string` permissions id
        
        * __state__  `type: string` key state
        * __updated_at__  `type: string` date in ISO 8601O format
    

* **400**: Некорректные праметры
    *  <code style="color: Green">required</code> `type: object` Некорректные праметры
        * __code__  `type: string` Код ошибки
        * __message__  `type: string` Описание ошибки
    

* **401**: Не авторизован
    *  <code style="color: Green">required</code> `type: object` Не авторизован
        * __code__  `type: string` Код ошибки
        * __message__  `type: string` Описание ошибки
    

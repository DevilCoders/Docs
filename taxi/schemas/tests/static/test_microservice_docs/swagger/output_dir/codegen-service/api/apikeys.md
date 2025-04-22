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
    *   `type: object` key object
        * __client_id__ <code style="color: Green">required</code> `type: string` client id (contains only latin letters, digits and hyphnes)
        * __comment__ <code style="color: Green">required</code> `type: string` text comment
        * __created_at__ <code style="color: Green">required</code> `type: string` date in ISO 8601O format
        * __id__ <code style="color: Green">required</code> `type: integer` client or key db id
        * __permissions__ <code style="color: Green">required</code> `type: array` granted permissions for the key
            * _Элементы массива:_
                *   `type: string` permissions id
        
        * __state__ <code style="color: Green">required</code> `type: string` `one of [ active, inactive ]` key state
        * __updated_at__ <code style="color: Green">required</code> `type: string` date in ISO 8601O format
    

* **400**: Некорректные праметры
    *   `type: object` Некорректные праметры
        * __code__ <code style="color: Green">required</code> `type: string` Код ошибки
        * __message__ <code style="color: Green">required</code> `type: string` Описание ошибки
    

* **401**: Не авторизован
    *   `type: object` Не авторизован
        * __code__ <code style="color: Green">required</code> `type: string` Код ошибки
        * __message__ <code style="color: Green">required</code> `type: string` Описание ошибки
    

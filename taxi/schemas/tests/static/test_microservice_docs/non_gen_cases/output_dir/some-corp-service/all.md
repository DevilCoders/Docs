#[some-corp-service](./../../Index/#some-corp-service) > all
**Corporate Integration API**


## /v1/authproxy/corp_client_id
### Допустимые параметры запроса (post)
Получить corp_client_id по uid пользователя



* _Body_:
    *   `type: object` 
        * __uid__ <code style="color: Green">required</code> `type: string` UID пользователя в Паспорте
    

### Допустимые параметры ответа

* **200**: OK
    *   `type: object` 
        * __corp_client_id__ <code style="color: Green">required</code> `type: string` идентификатор корпоративного клиента
    

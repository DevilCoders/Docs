#[some-corp-service](./../../Index/#some-corp-service) > all
**Corporate Integration API**


## /v1/authproxy/corp_client_id
### Допустимые параметры запроса (post)
Получить corp_client_id по uid пользователя



* _Body_:
    *  <code style="color: Green">required</code> `type: object` 
        * __uid__  `type: string` UID пользователя в Паспорте
    

### Допустимые параметры ответа

* **200**: OK
    *  <code style="color: Green">required</code> `type: object` 
        * __corp_client_id__  `type: string` идентификатор корпоративного клиента
    

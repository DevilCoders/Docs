## notifications@1

Были созданы следующие структуры:

* **params**

    ```
    database.createObjectStore('params');
    ```
* ~~**tags (c индексом expiryDate)**~~

    ```
    database
        .createObjectStore('tags', { keyPath: ['name', 'value'] })
        .createIndex('expiryDate', 'expiryDate');
    ```
    
    В последующем от хранилища `tags` отказались, и оно было **удалено**. 
    Удалено только из кода, специально у клиентов хранилище не уничтожалось, -
    это означает, что у одной части пользователей **есть** `tags`,
    а у другой его **нет**.
    Удаление произведено без изменения версии хранилища для того чтобы не создать
    блокировки.

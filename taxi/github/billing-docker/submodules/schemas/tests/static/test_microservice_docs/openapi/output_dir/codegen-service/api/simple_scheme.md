#[codegen-service](./../../../Index/#codegen-service) > api > simple_scheme
**sample service**

testing openapi 3.0 schema, don't use it as a base for your service, it is ugly

## /openapi/binary
### Допустимые параметры запроса (post)




* _Query_:
    * __name__  `type: string` 
* _Body_:
    *   `type: string` 

### Допустимые параметры ответа

* **200**: common response
    *   `type: object` 
        * __data__  `type: string` 
        * __name__  `type: string` 
    

## /openapi/homogeneous-multiple-responses
### Допустимые параметры запроса (get)




* _Query_:
    * __ext__  `type: string` 

### Допустимые параметры ответа

* **200**: response with ref schema
    *   `type: ?` 
    

## /openapi/multiple-responses
### Допустимые параметры запроса (get)




* _Query_:
    * __name__  `type: string` 

### Допустимые параметры ответа

* **200**: response with ref schema
    *   `type: ?` 
    

## /openapi/ping
### Допустимые параметры запроса (get)
ping handler





### Допустимые параметры ответа

* **200**: service is ok
    *   `type: ?` 
    

## /openapi/simple
### Допустимые параметры запроса (get)
simple handler

Long description


* _Query_:
    * __movies__  `type: array` 
        * _Элементы массива:_
            *   `type: string` 
    
    * __name__  `type: string` 
    * __tobaccos__  `type: array` 
        * _Элементы массива:_
            *   `type: string` 
    

### Допустимые параметры ответа

* **200**: example response
    *   `type: object` 
        * __age__  `type: integer` 
        * __favorite_movies__  `type: array` 
            * _Элементы массива:_
                *   `type: string` 
        
        * __name__  `type: string` 
        * __tobaccos__  `type: array` 
            * _Элементы массива:_
                *   `type: string` 
        
    

### Допустимые параметры запроса (post)




* _Body_:
    *   `type: object` 
        * __age__  `type: integer` 
        * __name__  `type: string` 
    

### Допустимые параметры ответа

* **200**: OK
    *   `type: string` 

## /openapi/user
### Допустимые параметры запроса (get)




* _Query_:
    * __name__  `type: string` 

### Допустимые параметры ответа

* **200**: response with ref schema
    *  <code style="color: Green">required</code> `type: object` 
        * __age__  `type: integer` 
        * __likes__  `type: array` 
            * _Элементы массива:_
                *  <code style="color: Green">required</code> `type: object` 
                    * __from__  `type: string` 
                
        
        * __name__  `type: string` 
    

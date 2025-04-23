#[codegen-service](./../../../Index/#codegen-service) > api > composite_types
**Test cases for allOf/oneOf**


## /api/v1/all-of-nested-one-of
### Допустимые параметры запроса (get)
allOf schema with a nested oneOf schema





### Допустимые параметры ответа

* **200**: ОК
    * **allOf**  
        *   `type: object` 
            * __property1__ <code style="color: Green">required</code> `type: string` 
        
        * **oneOf**  
            *   `type: object` 
                * __foo__ <code style="color: Green">required</code> `type: string` 
            
            *   `type: object` 
                * __bar__  `type: integer` 
            
        
    

## /api/v1/all-of-with-definition
### Допустимые параметры запроса (get)
allOf schema with a nested oneOf schema





### Допустимые параметры ответа

* **200**: ОК
    * **allOf**  
        *   `type: object` 
            * __property1__ <code style="color: Green">required</code> `type: string` 
        
        *   `type: object` 
            * __text__ <code style="color: Green">required</code> `type: string` 
        
    

## /openapi/all-of-basic
### Допустимые параметры запроса (get)
Basic test with allOf schemas





### Допустимые параметры ответа

* **200**: ОК
    * **allOf**  
        *   `type: object` 
            * __property1__ <code style="color: Green">required</code> `type: string` 
        
        *   `type: object` 
            * __property2__ <code style="color: Green">required</code> `type: string` 
        
    

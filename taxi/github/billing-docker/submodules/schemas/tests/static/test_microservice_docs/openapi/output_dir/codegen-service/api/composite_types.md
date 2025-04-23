#[codegen-service](./../../../Index/#codegen-service) > api > composite_types
**Test cases for allOf/oneOf**


## /api/v1/all-of-nested-one-of
### Допустимые параметры запроса (get)
allOf schema with a nested oneOf schema





### Допустимые параметры ответа

* **200**: ОК
    * **allOf**  
        *  <code style="color: Green">required</code> `type: object` 
            * __property1__  `type: string` 
        
        * **oneOf**  
            *  <code style="color: Green">required</code> `type: object` 
                * __foo__  `type: string` 
            
            *   `type: object` 
                * __bar__  `type: integer` 
            
        
    

## /api/v1/all-of-with-definition
### Допустимые параметры запроса (get)
allOf schema with a nested oneOf schema





### Допустимые параметры ответа

* **200**: ОК
    * **allOf**  
        *  <code style="color: Green">required</code> `type: object` 
            * __property1__  `type: string` 
        
        *  <code style="color: Green">required</code> `type: object` 
            * __text__  `type: string` 
        
    

## /openapi/all-of-basic
### Допустимые параметры запроса (get)
Basic test with allOf schemas





### Допустимые параметры ответа

* **200**: ОК
    * **allOf**  
        *  <code style="color: Green">required</code> `type: object` 
            * __property1__  `type: string` 
        
        *  <code style="color: Green">required</code> `type: object` 
            * __property2__  `type: string` 
        
    

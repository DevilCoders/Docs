#[codegen-service](./../../../Index/#codegen-service) > api > report_payouts
**TaxiFleet.API**


## /api/v1/reports/payouts/categories
### Допустимые параметры запроса (post)
Category list



* _Header_:
    * __Accept-Language__ <code style="color: Green">required</code> `type: string` 
    * __X-Ya-User-Ticket__ <code style="color: Green">required</code> `type: string` Yandex user ticket
    * __X-Ya-User-Ticket-Provider__ <code style="color: Green">required</code> `type: string` Yandex user ticket provider

### Допустимые параметры ответа

* **200**: OK
    *  <code style="color: Green">required</code> `type: object` 
        * __categories__  `type: array` 
            * _Элементы массива:_
                *  <code style="color: Green">required</code> `type: object` 
                    * __id__  `type: string` 
                    * __name__  `type: string` 
                
        
    

* **401**: Unauthorized
    *  <code style="color: Green">required</code> `type: object` Не авторизован
        * __code__  `type: string` Код ошибки
        * __message__  `type: string` Описание ошибки
    

## /api/v1/reports/payouts/details
### Допустимые параметры запроса (post)
Details for a selected payout



* _Body_:
    *  <code style="color: Green">required</code> `type: object` 
        * __category_id__  `type: string` 
        * __contract_id__  `type: string` 
        * __cursor__  `type: string` 
        * __driver_id__  `type: string` 
        * __limit__  `type: integer` 
        * __order_id__  `type: string` 
        * __payment_id__  `type: string` 
    
* _Header_:
    * __X-Ya-User-Ticket__ <code style="color: Green">required</code> `type: string` Yandex user ticket
    * __X-Ya-User-Ticket-Provider__ <code style="color: Green">required</code> `type: string` Yandex user ticket provider

### Допустимые параметры ответа

* **200**: OK
    *  <code style="color: Green">required</code> `type: object` 
        * __cursor__  `type: string` 
        * __transactions__  `type: array` 
            * _Элементы массива:_
                *  <code style="color: Green">required</code> `type: object` 
                    * __amount__  `type: string` Payment amount
                    * __contract_id__  `type: string` The contract the transaction is associated with
                    * __currency__  `type: string` Payment currency
                    * __driver_id__  `type: string` Driver id
                    * __driver_name__  `type: string` Driver name
                    * __order_id__  `type: string` Order id
                    * __transaction_id__  `type: string` Transaction id
                    * __transaction_type__  `type: string` Transaction type (product)
                
        
    

* **400**: Validation Error
    *  <code style="color: Green">required</code> `type: object` Некорректные праметры
        * __code__  `type: string` Код ошибки
        * __message__  `type: string` Описание ошибки
    

* **401**: Unauthorized
    *  <code style="color: Green">required</code> `type: object` Не авторизован
        * __code__  `type: string` Код ошибки
        * __message__  `type: string` Описание ошибки
    

## /api/v1/reports/payouts/list
### Допустимые параметры запроса (post)
List of payouts



* _Body_:
    *  <code style="color: Green">required</code> `type: object` 
        * __payment_at__ <code style="color: Green">required</code> `type: object` 
            * __from__  `type: string` 
            * __to__  `type: string` 
        
        * __cursor__  `type: object` Cursor object with offset information when searching
        
        * __limit__  `type: integer` 
        * __status__  `type: array` 
            * _Элементы массива:_
                *   `type: string` 
        
    
* _Header_:
    * __X-Ya-User-Ticket__ <code style="color: Green">required</code> `type: string` Yandex user ticket
    * __X-Ya-User-Ticket-Provider__ <code style="color: Green">required</code> `type: string` Yandex user ticket provider

### Допустимые параметры ответа

* **200**: ОК
    *  <code style="color: Green">required</code> `type: object` 
        * __cursor__  `type: object` 
        
        * __payments__  `type: array` 
            * _Элементы массива:_
                *  <code style="color: Green">required</code> `type: object` 
                    * __amount__  `type: string` Payment amount
                    * __bank_account_number__  `type: string` Bank account
                    * __bank_name__  `type: string` Name of the bank to describe
                    * __creation_date__  `type: string` Date of payment
                    * __currency__  `type: string` Payment currency
                    * __id__  `type: string` Payment id
                    * __order_number__  `type: string` Payment order number
                    * __payee_name__  `type: string` payee name for description
                    * __payment_target__  `type: string` Additional description of the payment order
                    * __status__  `type: string` 
                    * __void_details__  `type: object` 
                        * __event_at__  `type: string` Date and time of cancellation of payment
                        * __reason__  `type: string` Reason for canceling payment
                    
                
        
    

* **400**: Validation Error
    *  <code style="color: Green">required</code> `type: object` Некорректные праметры
        * __code__  `type: string` Код ошибки
        * __message__  `type: string` Описание ошибки
    

#[codegen-service](./../../../Index/#codegen-service) > api > report_payouts
**TaxiFleet.API**


## /api/v1/reports/payouts/categories
### Допустимые параметры запроса (post)
Category list



* _Header_:
    * __Accept-Language__ <code style="color: Green">required</code> `type: string` 
    * __X-Ya-User-Ticket__ <code style="color: Green">required</code> `type: string` Yandex user ticket
    * __X-Ya-User-Ticket-Provider__ <code style="color: Green">required</code> `type: string` `one of [ yandex, yandex_team ]` Yandex user ticket provider

### Допустимые параметры ответа

* **200**: OK
    *   `type: object` 
        * __categories__ <code style="color: Green">required</code> `type: array` 
            * _Элементы массива:_
                *   `type: object` 
                    * __id__ <code style="color: Green">required</code> `type: string` 
                    * __name__ <code style="color: Green">required</code> `type: string` 
                
        
    

* **401**: Unauthorized
    *   `type: object` Не авторизован
        * __code__ <code style="color: Green">required</code> `type: string` Код ошибки
        * __message__ <code style="color: Green">required</code> `type: string` Описание ошибки
    

## /api/v1/reports/payouts/details
### Допустимые параметры запроса (post)
Details for a selected payout



* _Body_:
    *   `type: object` 
        * __limit__ <code style="color: Green">required</code> `type: integer` 
        * __payment_id__ <code style="color: Green">required</code> `type: string` 
        * __category_id__  `type: string` 
        * __contract_id__  `type: string` 
        * __cursor__  `type: string` 
        * __driver_id__  `type: string` 
        * __order_id__  `type: string` 
    
* _Header_:
    * __X-Ya-User-Ticket__ <code style="color: Green">required</code> `type: string` Yandex user ticket
    * __X-Ya-User-Ticket-Provider__ <code style="color: Green">required</code> `type: string` `one of [ yandex, yandex_team ]` Yandex user ticket provider

### Допустимые параметры ответа

* **200**: OK
    *   `type: object` 
        * __cursor__ <code style="color: Green">required</code> `type: string` 
        * __transactions__ <code style="color: Green">required</code> `type: array` 
            * _Элементы массива:_
                *   `type: object` 
                    * __amount__ <code style="color: Green">required</code> `type: string` Payment amount
                    * __contract_id__ <code style="color: Green">required</code> `type: string` The contract the transaction is associated with
                    * __currency__ <code style="color: Green">required</code> `type: string` Payment currency
                    * __transaction_id__ <code style="color: Green">required</code> `type: string` Transaction id
                    * __transaction_type__ <code style="color: Green">required</code> `type: string` Transaction type (product)
                    * __driver_id__  `type: string` Driver id
                    * __driver_name__  `type: string` Driver name
                    * __order_id__  `type: string` Order id
                
        
    

* **400**: Validation Error
    *   `type: object` Некорректные праметры
        * __code__ <code style="color: Green">required</code> `type: string` Код ошибки
        * __message__ <code style="color: Green">required</code> `type: string` Описание ошибки
    

* **401**: Unauthorized
    *   `type: object` Не авторизован
        * __code__ <code style="color: Green">required</code> `type: string` Код ошибки
        * __message__ <code style="color: Green">required</code> `type: string` Описание ошибки
    

## /api/v1/reports/payouts/list
### Допустимые параметры запроса (post)
List of payouts



* _Body_:
    *   `type: object` 
        * __limit__ <code style="color: Green">required</code> `type: integer` 
        * __payment_at__ <code style="color: Green">required</code> `type: object` 
            * __from__ <code style="color: Green">required</code> `type: string` 
            * __to__ <code style="color: Green">required</code> `type: string` 
        
        * __status__ <code style="color: Green">required</code> `type: array` 
            * _Элементы массива:_
                *   `type: string` `one of [ processing, paid, canceled ]` 
        
        * __cursor__  `type: object` Cursor object with offset information when searching
        
    
* _Header_:
    * __X-Ya-User-Ticket__ <code style="color: Green">required</code> `type: string` Yandex user ticket
    * __X-Ya-User-Ticket-Provider__ <code style="color: Green">required</code> `type: string` `one of [ yandex, yandex_team ]` Yandex user ticket provider

### Допустимые параметры ответа

* **200**: ОК
    *   `type: object` 
        * __cursor__ <code style="color: Green">required</code> `type: object` 
        
        * __payments__ <code style="color: Green">required</code> `type: array` 
            * _Элементы массива:_
                *   `type: object` 
                    * __amount__ <code style="color: Green">required</code> `type: string` Payment amount
                    * __bank_account_number__ <code style="color: Green">required</code> `type: string` Bank account
                    * __creation_date__ <code style="color: Green">required</code> `type: string` Date of payment
                    * __currency__ <code style="color: Green">required</code> `type: string` Payment currency
                    * __id__ <code style="color: Green">required</code> `type: string` Payment id
                    * __order_number__ <code style="color: Green">required</code> `type: string` Payment order number
                    * __payment_target__ <code style="color: Green">required</code> `type: string` Additional description of the payment order
                    * __status__ <code style="color: Green">required</code> `type: string` `one of [ processing, paid, canceled ]` 
                    * __bank_name__  `type: string` Name of the bank to describe
                    * __payee_name__  `type: string` payee name for description
                    * __void_details__  `type: object` 
                        * __event_at__  `type: string` Date and time of cancellation of payment
                        * __reason__  `type: string` Reason for canceling payment
                    
                
        
    

* **400**: Validation Error
    *   `type: object` Некорректные праметры
        * __code__ <code style="color: Green">required</code> `type: string` Код ошибки
        * __message__ <code style="color: Green">required</code> `type: string` Описание ошибки
    

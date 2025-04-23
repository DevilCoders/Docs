# Issue

1. Integration in Israel is our goal number one and this includes:
   - user can order Wind scooters via Yango app. 
   - user can pay with Yango payment methods. 
 
   It means that we should execute payment transactions via Yandex backend (because of PCI DSS requirements and other safety requirements) - this is only necessary for Yango App, not for Wind App (Wind App can use Tranzila as before). 
   
   For this task we have time until May 1, 2022.
 
2. The secondary goal: to be ready to GAAP and SOAX audits. Most likely this means:
   - execute all payments transactions via Yandex backend (including payments via Wind App)
   - register all payment transactions (perhaps we can register these automatically if we execute transactions via Yandex backend) and user wallet transactions (debit/credit) via Yandex backend  
   - all wind production changes should be approved (this RFC is not about it)
 
   For this goal we have deadline: September 1, 2022. 
   And we can start prepare for this.



# Solution proposal 

Our primary task is integration yango_app->wind_backend. To do this, we should do:  
1. Use only yandex payment methods (in Yango App)
2. Use yandex backend to execute payment transactions. For this we should do:
   1. Yandex backend transmits payment method id in requests to wind (in wallet recharging requests, etc) 
   2. Wind backend uses Yandex API to execute payment transactions with Yandex payment method id. At the moment we need it only for yango_app->wind_backend integration but it also can help us in future when we begin use it for the Wind App.
3. Transfer of all user cards from wind/tranzila to yandex:
   1. Yandex backend received card_token/exp_date/card_holder from wind backend
   2. Then Yandex backend received CCNO (PAN) from Tranzila
  
Our secondary task is preparing for audit. For payments this means:
1. Register all user wallet transactions via Yandex API (will consider this later).
2. Wind backend use Yandex backend to execute payment transaction - that is to use the same API as in yango_app->wind_backend integration.

You can see sequence diagram in `payments_sequence_diagram.plantuml`  

## Payments

### Yandex API

#### POST /yandex/payments/create

Starts execution of payment transaction

Request body:
```json
{
  "payment_id": "operation_id", // idempotency key
  "user_id": "user_id",         // Wind user id    
  "yandex_uid": "yandex_user_id", // Yandex user id.
  "user_ip": "::ffff:31.173.85.154" // user ip address
  "payment_method": {
    "method_id":  "method_id",          // Yandex payment method id
    "type": "card|applepay|googlepay"   // Yandex payment method type
  },
  "currency": "EUR",
  "items": [ // Probably at the moment we need only 1 item, but it can be useful if we need to detail payment in receipt
    {
      "id": "charge_pay20_get30",   // any unique id
      "receipt_title": "pay 20 get 30",  // describes item in user receipt
      "amount": "20.00"  // decimal
    },
  ]
}
```

#### GET /yandex/payments/retrieve?payment_id=operation_id

Returns payment info. This endpoint can be used to get the current status of the payment transaction.

response body:
```json
{
  "status": "pending|success|failed",
  "reason": { // optional (exists only with status=failed)
    "code": "reason_code",
    "description": "human readable description (internal)"
  },
  "payment_method": {
    "method_id":  "method_id",          // Yandex payment method id
    "type": "card|applepay|googlepay"   // Yandex payment method type
  },
  "currency": "EUR",
  "items": [ 
    {
      "id": "charge_pay20_get30",   // any unique id
      "receipt_title": "pay 20 get 30",  // describes item in user receipt
      "amount": "20.00"  // decimal
    },
  ]
}
```

#### POST /yandex/payments/update

(I am not sure that we need it at the moment)
Updates payment data and start new transaction or refund. First of all it can be used to refund a payment (including partial refund). 

Request body:
```json
{
  "payment_id": "operation_id", // idempotency key
  "items": [ 
    {
      "id": "charge_pay10_get30",
      "receipt_description": "pay 10 get 30",
      "amount": "10.00"  // new amount 
    }
  ]
}
```


### Wind API (Top-Up)

#### POST /wind/wallet/topups:

Starts wallet charging. It is assumed that this endpoint uses `/yandex/payments/create`.

Request body:
```json
{
  "topup_id": "charge_pay20_get30",
  "operation_id": "operation_id", // idempotency key 
                                  // (perhaps the same as payment_id in /payments/create)
  "user_id": "user_id",           // Wind user id
  "yandex_uid": "yandex_user_id", // Yandex user id
  "user_ip": "::ffff:31.173.85.154" // user ip address
  "payment_method": {
    "method_id":  "method_id",          // Yandex payment method id
    "type": "card|applepay|googlepay"   // Yandex payment method type
  },
}
```

#### GET /wind/wallet/topups/status?operation_id=operation_id

Returns charging operation status.

Response body:
```json
{
  "status": "pending|success|failed",
  "reason": { // optional (exists only with status=failed)
    "code": "reason_code",
    "description": "human readable description (internal)"
  }
}
```

#### POST  /wind/freepasses

Starts free pass charging. 

Request body:
```json
{
  "free_pass_type": "DAY_PASS",
  "pass_id": "operation_id", // idempotency key 
  "user_id": "user_id",           // Wind user id
  "yandex_uid": "yandex_user_id", // Yandex user id
  "user_ip": "::ffff:31.173.85.154" // user ip address
  "payment_method": {
    "method_id":  "method_id",          // Yandex payment method id
    "type": "card|applepay|googlepay"   // Yandex payment method type
  },
}
```

#### GET /wind/freepasses/payment-status?pass_id=operation_id

Returns free pass payment status.

Request body:
```json
{
  "status": "pending|success|failed",
  "reason": { // optional (exists only with status=failed)
    "code": "reason_code",
    "description": "human readable description (internal)"
  }
}
```

#### POST /wind/payment-callback

This callback is called after payment transaction is performed.

Request body:
```json
{
  "operation_id": "operation_id",
  "status": "success|failed",
  "reason": { // optional (exists only with status=failed)
    "code": "reason_code",
    "description": "human readable description (internal)"
  }
}
```

Yandex backend repeats call to this endpoint until it returns 200 or 404 response (404 means that operation not found)


## User cards migration

###  Wind API

#### POST /wind/get-payment-cards

Request body:
```json
{
  "user_ids": [ // Wind user ids
    "id1",
    "id2"
  ]
}
```

Response body:
```json
{
  "users": [
    {
      "user_id": "id1", 
      "cards": [
        {
          "tranzila_token": "token",
          "expiration_date": {
            "year": "22", 
            "month": "12"
          },
          "cardholder": "James Bond"
        }
      ]
    }
  ]
}
```

### Tranzila API

#### GET /tranzila/get-card?supplier=wind&TranzilaPW=pw&TranzilaTK=tk

Returns CCNO (PAN). As far as I know we have already asked them to develop this endpoint (?)

Request query:
- supplier - Wind&Yandex identifier
- TranzilaPW - Wind&Yandex password
- TranzilaTK - user card token

Response body:
```json
{
  "ccno" : "***" // asymmetrically encrypted full credit card number (PAN)
}
```


Or if possible, they could create a bulk method (more convenient):
```
POST /tranzila/get-cards
```
Request body: 
```json
{
  "supplier" : "wind",
  "tranzila_pw": "password",
  "tranzila_tks": [
    "token1",
    "token2"
  ]
}
```
Response body:
```json
{
  "cards": [
    {
      "tranzila_tk": "token1",
       "ccno" : "***"
    },
  ]
}
```

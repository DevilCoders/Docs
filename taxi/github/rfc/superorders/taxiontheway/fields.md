## Поля taxiontheway

### typed_experiments
```
builder.UpdateApplicationInformation(app_vars)
builder.UpdateZoneAndCountry(data);
builder.UpdatePaymentOption(data); -> payment_type
builder.UpdateTariffClass(GetTariffClassFromOrder(data));
builder.UpdatePhoneId(data);
builder.UpdateUserId(input);
builder.UpdateYandexUuid(data);
builder.UpdateYandexUid(data);
builder.UpdatePaymentType(data.GetOrder().current_payment_type); -> payment_type
builder.UpdateSurge(data); order.request.surge_params.surge
builder.UpdatePaidSupply(IsPaidSupplyOrder(data.GetOrder())); 
builder.UpdateCurrency(rdata.currency); -> computing currency
builder.UpdateFixedPrice(data); -> order.is_fixed_price
builder.UpdateRoute(data.GetOrder().request.route);
builder.UpdatePlates(data); -> driver_id
```

список используемых kwarg-ов для данного consumer https://paste.yandex-team.ru/4385331

### brandings - удалить + удалить поход в experiments2

### cancel_rules - в процессе переноса в order-parts

### routeinfo - вероятно, уже подменяется на уровне api-proxy

### allowed_changes - order-parts
### pending_changes - order-parts

### payment - order-parts
### payment_changes - order-parts

### status_info - order-parts
### tariff - order-parts
### autoreorder - order-parts какой-то текст, возможно, можно обобщить с нотификациями

### driver - orderperformerinfo
### park - куда-то к orderperformerinfo

### route_sharing_url - order-parts

### notifications - зависит от мультизаказа, вынос заблокирован сервисом мультизаказа

### tips_suggestions - сервис tips
### tips - сервис tips

### feedback - уже на уровне api-proxy
### supported_feedback_choices - комбинация feedback и информации о заказе, вероятно, можно унести в feedbacks


оставляем в протоколе

Флоу отмены
### cancelled_by
### cancel_reason_description


## Вопросы
1. Зачем в ответе taxiontheway столько различных способов передавать цену поездки. Возможно, нужно унифицировать.
2. `max_waiting_time`, `departure_time` - почему лежит прямо в корне?
3. `granted_promotions` - вероятно можно выпилить
4. `request` - нужен ли, и возможно, его можно улучшить
5. `coupon` - вероятно, нужно куда-то перенести
6. `button_modifiers` нужно совсем выпилить и сделать спец кнопку?
7. `force_destination` - что-то про глухого водителя, нужно понять как работает
8. `reorder` - dialogs об апгрейде суржем и апгрейде тарифа `surge` - выглядит как тоже диалог но для суржа
9. `higher_class_dialog` ещё диалог 


## Поля для обобщение в объекты
1. `loyal`
2. `free_cancel_for_reason` - cancel_rules?
3. `source` - ?
4. `cancel_disabled`, `user_ready`, `dont_call`, `dont_sms` - actions
5. `reorder`, `surge`, `higher_class_dialog` - диалоги

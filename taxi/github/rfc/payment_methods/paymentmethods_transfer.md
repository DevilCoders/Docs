## Вынос ``integration-api/v1/paymentmethods`` из протокола

Ручка слишком сложна для того, чтобы написать ее полностью на api-proxy. Поэтому предлагается частично вынести в микросервис. На данный момент нет подходящего кандидата, поэтому рассматриваются 2 варианта создания нового сервиса:
1) Создание сервиса ``payment-methods``:
- Позволяет ограничить скоуп сервиса только методами оплаты
- В него можно будет вынести ручку [/v1/available-payment-types](https://github.yandex-team.ru/taxi/uservices/blob/f7814d5a0805c5c84c1dda5c1834dc60b15eb8c8/services/superapp-misc/docs/yaml/api/api.yaml#L53) из ``superapp-misc``
- Можно объединить с сервисом ``card-filter``

2) ~~Создание сервиса ``integration-api``:~~
- ~~Позволяет держать все ручки скоупа ``int-api`` рядом~~
- ~~Получается не совсем микросервис, а небольшой монолит~~

После обсуждения был выбран вариант 1.

### Новая ручка api-proxy ``/integration/paymentmethods``:
- ходит в ``user-api/users/get`` c ``user_id`` за документом пользователя из ``dbusers``
- ходит в ``user-api/v2/user_phones/get`` c ``phone_id`` для получения ``user_phone`` с ``lpm``
- ходит в ``corp-integration`` за ``corp_paymentmethods``
- ходит в ``cardstorage`` / ``card-filter`` за ``cards``
- ходит в ``payment-methods`` для получения данных, которые нельзя получить из api-proxy

#### Фоллбеки:
- при неудачном запросе в ``user-api/users/get`` ручка вернет 500
- при неудачном запросе в ``user-api/v2/user_phones/get`` ручка не вернет последний метод оплаты
- при неудачном запросе в ``corp-integration`` ручка не вернет корпоративные методы оплаты
- при неудачном запросе в ``card-filter`` ручка пойдет за картами в ``cardstorage``
- при неудачном запросе в ``cardstorage`` (при условии неудачного похода в ``card-filter`` или без него вовсе) ручка не вернет карты
- при неудачном запросе в ``payment-methods`` ручка не вернет карточные методы оплаты

![Схема](https://jing.yandex-team.ru/files/detinin/schema-v5.jpg)  

Поход в ``user-api/users/get`` блокирует все остальные

### Ручка ``v1/integration-availability`` сервиса ``payment-methods``:

``POST /availability {}``

``Response``
```json
{
  "service_token": {},
  "availability_map": {},
  "localized_cash_label": {}
}
```
### План на текущую техноквоту:
- [ ] Создать сервис ``payment-methods``: [3-4d]
    - [ ] Пройти архревью и секревью [2d]
    - [ ] Создать сервис [1d]
    - [ ] Написать ручку ``v1/integration-availability`` [1d]
- [ ] Написать api-proxy ручку (с оставлением возможности проксирования в протокол по эксперименту) [2d]
- [ ] Переключить ``call-center`` на нее как основного потребителя [1d]

### План доработок
- [ ] Переключить остальных потребилетей [4d]
- [ ] Удалить код из монолита [2d]
- [ ] Объединить ``card-filter`` и ``payment-methods`` [2d]
- [ ] Перевезти ``/v1/available-payment-types`` из ``superapp-misc`` в ``payment-methods`` [1d]

Для переключения потребителей нужно знать, кто сейчас пользуется ручкой и как им переехать. На данный момент известны:
- КЦ - план переезда понятен
- ППЯ - см ya-authproxy, можно уточнить у [e-usov@](https://staff.yandex-team.ru/e-usov)
- Алиса - [ezarubkin@](https://staff.yandex-team.ru/ezarubkin) / [olegator@](https://staff.yandex-team.ru/olegator)
- lightbusiness (доставка) - [fmobster@](https://staff.yandex-team.ru/fmobster)
- Корпоративный кабинет - [plurye@](https://staff.yandex-team.ru/plurye)
- ...
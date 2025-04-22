# Ручка таргетированных коммуникаций в int-api

## Задача
Новые ручки в int-api отдающие информацию о новичках и скидках, будут использоваться для таргетированных коммуникаций турбоаппа такси в ППЯ/Ябро (баннеры, бейдж со скидкой на иконке)
https://st.yandex-team.ru/TAXIBACKEND-33709

## Дополнительные требования
- int-api живёт в монолите, в монолит мы сейчас стараемся не коммитить
- Нагрузка на ручку ~2к рпс
- Желаемый тайминг 100мс (насколько реально?)
- В запросе будет доступен только yandex_uid (неточно)

## Откуда брать данные
Для определения новый пользователь или нет можно использовать сервис [user-statistics](https://github.yandex-team.ru/taxi/uservices/blob/6a612aee2a8e3b26724873681cc909920938ae46/services/user-statistics/docs/yaml/api/api.yaml#L14)

_*TBD*_ Для получения информации о скидках можно использовать сервис discounts. (Как именно - обсуждается. Сейчас для получения информации о скидке нужны почти все [параметры](https://github.yandex-team.ru/taxi/uservices/blob/93502fd4f7530b058d49ba04da051a929a0e38b7/services/discounts/docs/yaml/definitions.yaml#L853), которые используются для совершения заказа, а у нас только yandex_uid)


<details>
  <summary>Для истории (если бы запрос делался с клиентов)</summary>
  ## Как сейчас турбоапп ходит в int-api
  Запросы идут на http://ya-authproxy.taxi.yandex.ru/, оттуда по правилам проксирования из [конфига](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/YA_AUTHPROXY_ROUTER_RULES_2) перенаправляются на [api-proxy](https://tariff-editor.taxi.yandex-team.ru/control-api-proxy/endpoints?search=integration), оттуда уже в int-api (монолит)

  Необходимые авторизационные хедеры: Authorization (Bearer {oauth token}), X-YaTaxi-UserId

  Ручки будут вызываться до захода в турбоапп, соответственно user_id отсутствует. В качестве альтернативы можно использовать прокси-сервис [passport-authproxy](https://wiki.yandex-team.ru/taxi/backend/client-product/teams/discovery/services/passport-authproxy/) со своим [конфигом правил](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/PASSPORT_AUTHPROXY_ROUTE_RULES?name=PASSPORT_AUTHPROXY_ROUTE_RULES)  

  url - https://passport-authproxy.taxi.yandex.ru  
  Необходимо будет добавить скоуп, с которым ппя получает токен, в [конфиг](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/PASSPORT_AUTHPROXY_PASSPORT_SCOPES_BY_ALIAS?name=PASSPORT_AUTHPROXY_PASSPORT_SCOPES_BY_ALIAS)   
  У ya-authproxy есть функционал позволяющий добавлять хедер с bound_uids (необходимы, что не считать новым старого пользователья с новым uid). У passport-authproxy такого функционала нет, необходимо будет его добавить
    
  Таким образом со стороны ппя в запросе нужен только хедер Authorization, по нему passport-authproxy получит yandex_uid и проксирует запрос дальше
</details>

Запрос будет идти с бэка ппя, нужно будет настроить соответствующие доступы и TVM правила

## Нагрузка
2k rps  
- passenger-authproxy: Обсудил с Егором Панфиловым, сервис к такой нагрузке готов, но желательно подавать её постепенно и написать ему перед запуском  
- api-proxy: Обсудил с Игорем Березняком, скорее всего норма, точнее посчитает дежурный после заведения тикета на создания новой ручки api-proxy  
- user-statistics: Обсудил с Лёшей Быковым, сервису нужно будет добавить мощностей, на учениях с нагрузкой справляться не будет

## Предлагаемое решение
Чтобы не трогать код монолита, создать ручки в api-proxy и добавить их в конфиг правил проксирования passport-authproxy

Ручка отвечающая новый пользователь или нет - integration/newbie: будет ходить за количеством поездок в user-statistics  
При недоступности user-statistics - фолбек на is_new_user: false в api-proxy

Ручка с информацией о скидках - _*TBD*_

```yaml
paths:
  4.0/integration/newbie:
    post:
      parameters:
      - name: X-Yandex-UID
        in: header
        required: true
        schema:
          type: string
      requestBody:
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/NewbieRequest'
      responses:
        200:
          description: OK
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/NewbieResponse'

components:
  schemas:
    NewbieRequest:
      type: object
      properties: []

    NewbieResponse:
      type: object
      properties:
          is_new_user:
              type: boolean
```

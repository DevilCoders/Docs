
## Бизнесовая задача

### Описание

Нужно подсказывать пользователю Алисы о том, что при залогине в приложении Такси он сможет пользоваться кроссдевайсом.

### Гипотеза

При заказе такси через колонку люди часто открывают приложение и не видят там своего заказа. Основная причина — внутри Такси они авторизованы фонишем. Предполагается, что колонка может сообщить пользователю о необходимости залогина для кроссдевайса.

### Продуктовые ограничения

Мы не можем однозначно определить какой user в dbusers отвечает за приложение Такси у владельца колонки, возможные сценарии:

* В колонке один портальный аккаунт, а в приложении Такси — другой.
* У пользователя несколько телефонов, как следствие — несколько юзеров в такси
* Определить "актуального" пользователя со стопроцентной гарантией невозможно

## Решение

По phone_id из колонки найти "акутуального" пользователя Такси, и
* Если для такого phone_id нет портального пользователя
* Если для такого phone_id "актуальным" является фониш

Сообщить колонке о возможности подсказки о залогине.

### Как искать "актуального" пользователя

Алиса в запросе /profile присылает нам номер телефона, по которому определяется (или создается) phone_id. По этому phone_id ищем пользователей в Такси (включая фонишей), и сортируем их по полю "updated". Этот подход в теории имеет недостатки, см. продуктовые ограничения.

### API

#### Изменения в  `integration-api`

Ручка `/profile`:

В ответ ручки добавляется поле "suggest_portal_signin". При наличии такой структуры и флага клиент может подсказать пользователю о необходимости залогина в приложении Такси.

```json
// Request
{
  "name": "Bob",
  "sourceid": "alice",
  "user": {
    "phone": "+79217854691",
    "yandex_uid": "4023520426"
  }
}

// Response
{
  "suggest_portal_signin": true, // new
  "dont_ask_name": false,
  "experiments": [...],
  "name": "Bob",
  "user_id": "2161408f5b0992868fd52f085fec818f",
}
```


### Детали реализации


#### zalogin

В сервис zalogin добавляем новую ручку /internal/suggest_portal_signin.
```
POST zalogin/internal/suggest_portal_signin
X-Yandex-UID: yandex_uid
X-YaTaxi-PhoneId: phone_id

Response:
{
    "suggest_portal_signin": true|false
}
```

По переданному уиду ручка должна сходить с phone_id в user-api/users/search https://github.yandex-team.ru/taxi/uservices/blob/c405db99adee96f4cc35f55d6090dd1999ac0114/services/user-api/docs/yaml/api/users.yaml#L39, отсортировать полученных пользователей по полю `updated`(1) и отфильтровать по `application`(2). Если выполняется любое из условий:

* пользователи не найдены
* наиболее "свежий" пользователь — фониш
* наиболее "свежий" пользователь — портал с yandex_uid != request.yandex_uid

вернуть "suggest_portal_signin": true

Если инвертировать — самый свежий пользователь должен быть порталом с yandex_uid=request.yandex_uid

(1) Почему сортировка по `updated`? Поле обновляется при клиентских вызовах /launch, /auth и /authconfirm (также в старых promotions), и сейчас это самый надежный способ узнать "акутальное" устройство

(2) Искать "актуальное" устройство нужно только среди мобильных приложений. Простой способ сделать это — ограничить список `user.application`, участвующих в фильтрации. Для этого предлагается создать конфиг `SUGGEST_PORTAL_SIGNIN_APPLICATIONS`, в котором по дефолту будет только `iphone` и `android` (мобильные приложения ЯТакси для айфона и андроида)

На псевдокоде итоговая функция выглядит так:
```
def should_suggest():
  users = [
    user
    for user in user_api.search(phone_id=request.phone_id)
    if user.application in config.SUGGEST_PORTAL_SIGNIN_APPLICATIONS
  ]
  if not users:
      return True

  users.sort(key=lambda u: -u.updated)
  uid_match = users[0].yandex_uid == request.yandex_uid
  if not uid_match:
     return True

  is_portal = users[0].yandex_uid_type == 'portal'
  if not is_portal:
     return True
  return False
```

#### integration-api

При запросе `/profile` c sourceid=alice (в будущем можно расхардкодить) сделать запрос к сервису zalogin, добавить ответ в корень.
При не-200 ничего не добавлять.
Поход в ручку закрыть экспериментом SUGGEST_PORTAL_SIGNIN_IN_PROFILE

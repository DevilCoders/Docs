На данный момент по словам Марии Плотниковой генерация промокодов занимает около 2-3 часов.
Скрипт Саши Накапкина по запуску выдачи промокодов работает сумарно тоже около 3-х часов, даже при запуске задач батчами.
Из чего могу сделать вывод, что ручка, которая работает 2-3 часа не самое выгодное решение.

Хочу сделать батч-stq, где в каждой stq будет генерироваться и выдаваться пользователю 250 промокодов. На каждую таску будет назначаться 250 задач по генерации, а затем выдаче. Делаем 6 worker-ов, которые будут по окончании свой работы брать следующи 250 задач из общего числа на генерацию и выдачу.

Для генерации промокодов можно переиспользовать generate_promocodes в сервисе couponse. А для выдачи промокодов пользователю переиспользовать ручку internal_generate.

```
name: generate_and_distribute_promocodes
arguments:
  - name: gen_id
    required: true
    schema:
        type: string
  - name: yandex_uid
    required: true
    schema:
        type: string
        description: |
            id пользователя, кому выдаёт, опциональное.
            Если пришло, то добавляем в список промокодов
            пользователя.
            Не ожидается, если пришел phone_id.
  - name: application_name
    required: false
    schema:
        type: string
        description: |
            Название приложения пользователя iphone|uber_android|...
            Если в запросе есть yandex_uid, то либо application_name,
            либо brand_name должны быть указаны.
  - name: brand_name
    required: false
    schema:
        type: string
        description: |
            Бренд приложения пользователя yataxi|yauber|yango|...
            Если в запросе есть yandex_uid, то либо application_name,
            либо brand_name должны быть указаны.
  - name: token
    required: true
    schema:
        type: string
        description: токен идемпотентности
  - name: series_id
    required: false
    schema:
        type: string
        description: id серии промокода
  - name: service:
    required: false
    schema:
        type: string
        description: сервис из которого сгенерирован промокод (eats)
```

В качестве токена иденпотентности будет браться номер заказа, чтобы отслеживать число применения промокодов.
Если серия промокодов уже существует, то необходимо указать id промокода для генерации, если серии нет, то необходимо ее указать и сделать проверку в коде на существование серии, если нет то добавить новую.

######
Продолжение от gadelzakirov
Судя по вики https://wiki.yandex-team.ru/taxi/backend/client-product/teams/5/services/coupons/tech/#vydachacherezruchkugenerate
Генерацию и выдачу можно произвести через ручку /internal/generate, которая генерирует и выдает пользователю промокод через генератор https://a.yandex-team.ru/arcadia/taxi/uservices/services/coupons/src/views/internal/generate/post/generation/generator.hpp?rev=r9549488

Для генерации генератор строит запрос в монгу https://a.yandex-team.ru/arcadia/taxi/uservices/services/coupons/src/views/internal/generate/post/generation/generator.cpp?rev=r9563443#L217 и вызовом promocodes.InsertOne(doc); добавляет запись.

Для выдачи генератор использует функцию https://a.yandex-team.ru/arcadia/taxi/uservices/services/coupons/src/utils/user_coupons.hpp?rev=r9563408#L79. Эта же функция используется и в ручке /internal/activate_bulk (кстати в балковой ручке активация промоода производится по одному, а не одним запросом в монгу). Те новой stq можно прокинуть в профиль как уникальные так и неуникальне промокоды, заранее определив тип промокода.

Для определения типа промокода (уникальный/неуникальный) уже существует ручка /internal/series/info, которая использует функцию https://a.yandex-team.ru/arcadia/taxi/uservices/services/coupons/src/models/promocode_series.hpp?rev=r9563463#L115. По уникальности и неуникальности можно определить необходимость генерации промокода.


Я предлагаю реализовать stq coupons_bulk_generate_and_activate_promocodes

Схема работы:
1) В настройках очереди задаем, число одновременно работающих тасок и число воркеров, для ограничения числа запросов в монгу.
2) Таски будет ставить сервис crm-hub, на стороне которого будет законфижен размер чанков пользователей, которым нужно прокинуть промокод. Это позволит управлять нагрузкой на одну таску.
3) В новой stq переиспользовать существующие классы/функции, некоторые реализовать балково и не insert-ить по одной доке в монгу, а сразу несколько вызовом promocodes.InsertMany(vector_of_docs);

Апи stq:

users_list:
  type: array
  items:
    $ref: '#/definitions/User'
token:
    type: string
    description: токен идемпотентности (можно вынести в task_id) генерируется на стороне сервиса, который ставит таску
series_id:
    type: string
    description: id серии промокода
value:
    type: integer
    description: |
        Сумма скидки для серий с варьируемой стоимостью,
        обязательный параметр для данных серий
    minimum: 0
expire_at:
    description: Время окончания действия промокода (необязательно для неуникальных)
    type: string
    format: date-time
service:
    type: string
    description: сервис из которого сгенерирован промокод (taxi | grocery
        | eats)
value_numeric:
    $ref: '#/definitions/NumericValue'
    description: |
        Нецелочисленная сумма скидки для серий с варьируемой стоимостью,
        при наличии будет использована вместо value
required:
  - token
  - series_id
  - users_list

definitions:
    User:
        additionalProperties: false
        type: object
        properties:
            phone_id:
                type: string
                description: |
                    id номера телефона пользователя, опциональное.
                    Если пришло, то ограничиваем использование промокода
                    только пользователем с этим phone_id.
                    Нужно для поддержки выдачи промокода по номеру
                    телефона через админку.
                    Не ожидается, если пришел yandex_uid.
            yandex_uid:
                type: string
                description: |
                    id пользователя, кому выдаёт, опциональное.
                    Если пришло, то добавляем в список промокодов
                    пользователя.
                    Не ожидается, если пришел phone_id.
            application_name:
                description: |
                    Название приложения пользователя iphone|uber_android|...
                    Если в запросе есть yandex_uid, то либо application_name,
                    либо brand_name должны быть указаны.
                type: string
            brand_name:
                type: string
                description: |
                    Бренд приложения пользователя yataxi|yauber|yango|...
                    Если в запросе есть yandex_uid, то либо application_name,
                    либо brand_name должны быть указаны.

Токены для генерации будут строится из общего токена идемпотентности - token_{yandex_uid+application_name(brand_name) / phone_id}. На стороне crm-hub токены будут генерироваться не случайным образом, а по какому то правилу из настроек кампании (нпример id кампании + id группы + series_id + )
В случае рестарта таски можно найти те промокоды, которые уже существуют, запросом promocodes.FindOne и добавить только те, которых нет (Не знаю насколько чтение тяжелое для монги). 
С активацией промиков аналогично, можно сначала отсеить пользователей, у которых есть промокод и у которых лимит на число промокодов, после чего активировать промокоды в профилях.
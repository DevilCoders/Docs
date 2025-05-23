# Изменения в protocol для фичи "Платные Дороги" (Toll Roads)

Проект описан [здесь](https://st.yandex-team.ru/PARTNERSPROJECT-575)

Задача: научиться определять, была ли предложена пассажиру платная дорога, была ли выбрана платная дорога в качестве маршрута,
кто будет оплачивать проезд по платной дороге: водитель или пассажир.

## Изменения в запросе к estimate

Партнеры через integration-api будут передавать в запросах к estimate новый параметр `use_toll_roads`. Значение этого флага будет использоваться бэкендом при построении маршрута через router'ы. При первом запросе в routestats передается значение `use_toll_roads = false`, что соответствует попытке построить маршрут, избегая платных дорог (дефолтное поведение).

Если есть возможность проехать по маршруту с платным участком, то у пользователя будет возможность выбрать платный вариант. 
_Важно:_ платный вариант необязательно должен быть быстрее, так как нужно давать возможность пользователю заказать платный вариант, который на момент совершения заказа медленнее, если пользователь считает, что риск возникновения пробки на бесплатной дороге выше. Если пользователь выбрал платный маршрут ([детально](different_payers.md#заказ-такси)), то партнер делает запрос в estimate с `use_toll_roads = true`.

Если в запросе не пришел флаг `use_toll_roads`, то это значит, что бэкенд в таком случае реализует текущее поведение, а именно передает в роутеры флаг `avoid=tolls` в зависимости от эксперимента. 

## Изменения в ответе estimate

В ответ estimate предлагается добавить объект `toll_roads`, который будет содержать информацию о платных участках на маршруте. Если пассажир делает заказ, не дождавшись ответа routestats, то создается заказ без оффера; в таком случае срабатывает фоллбэк (estimate не ответил), см. детали [ниже](#сценарии-работы-при-различных-комбинациях-флагов-use_toll_roadshas_tolls).

## Изменения в запросе к orderdraft

При вызове orderdraft начнем передавать в объекте `toll_roads` поля `user_had_choice` и `user_chose_toll_road` и сохранять его в toll_roads (поля `user_had_choice` и `user_chose_toll_road` уже поддержаны).
Кроме того, здесь будет рассчитываться `auto_payment` (источник заказа order_proc.order.agent.agent_id (== "gepard")) и отправляться в toll-roads и сохраняться в order_proc.

## Изменения в ответе orderdraft

Ordedraft будет сохранять в toll_roads поля `auto_payment`, `user_had_choice` и `user_chose_toll_road`, передавая их в STQ-таску toll_roads_order_save.

## Изменения в новом процессинге

[Тык](https://a.yandex-team.ru/arc/trunk/arcadia/taxi/uservices/services/processing/agl-modules/taxi/orders/extensions/platform/toll_roads_order_save.yaml?rev=r8195617#L3)

Нам нужно понимать, что выполнен партнерский заказ. Для таких заказов платная дорога оплачивается водителем. 
Поэтому в новом процессинге будем прокидывать в stq таску `toll_roads_order_save` флаг `auto_payment`.

### Содержит ли построенный на бэкенде маршрут платные участки

В данный момент при построении маршрута в роутеры можно передать флаг использования платных дорог скорее как пожелание, а не требование. То есть на запрос с `use_toll_roads = true` может прийти бесплатная дорога, и наоборот, см. [ниже](#сценарии-работы-при-различных-комбинациях-флагов-use_toll_roadshas_tolls). Для того, чтобы понимать, какой в итоге маршрут построен - платный или бесплатный - в ответе будет флаг `has_tolls` в объекте `toll_roads`.

### Информация о том, как будет происходить оплата

Клиент при выборе платной дороги указывает, кто будет платить за дорогу, данная информация будет приходить в поле `toll_roads.auto_payment`. 

Для того, чтобы отличать автоматическое списание средств от ручной оплаты клиентом, в ответ estimate в объект `toll_roads` будет флаг `auto_payment`. 

### Тексты через клиентские эксперименты

Тексты отдаются на клиент с помощью клиентских экспериментов в ручке suggest/pin_drop, которая точно будет дернута до запроса в routestats. Эксперимент `toll_roads` для платных дорог в тестинге - по [ссылке](https://tariff-editor.taxi.tst.yandex-team.ru/experiments3/edit/toll_roads?type=experiments&name=toll_roads). Если ручка suggest/pin_drop не отвечает - всё Такси не работает, так как в этой ручке приходит зона, а без зоны мы не знаем, работает ли здесь сервис вообще.

### Изменения схемы ручки

```yaml
definitions:
  EstimateRequest:
    properties:
      ...
      toll_roads:
        type: object
        description: информация о платных участках на построенном маршруте
        properties:
          use_toll_roads:
            type: boolean
            description: не избегать платных дорог при построении маршрута
    
  EstimateResponse:
    properties:
      ...
      toll_roads:
        type: object
        description: информация о платных участках на построенном маршруте
        properties:
          has_tolls:
            type: boolean
            description: содержит ли построенный маршрут платные участки
          
        required:
        - auto_payment
```

## Сценарии работы при различных комбинациях флагов `use_toll_roads/has_tolls`

Довольно подробно описано [здесь](routestats.md#сценарии-работы-при-различных-комбинациях-флагов-use_toll_roadshas_tolls)

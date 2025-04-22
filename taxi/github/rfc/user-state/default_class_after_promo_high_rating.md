# Изменение тарифа по умолчанию после высокой оценки поездки с промотированным тарифом

## Что хотим сделать
Сейчас в проде работает логика апгрейда тарифа. 
Мы хотим дополнить сценарий работы апгрейда: если пользователь оценил поездку после апгрейда на 5 звезд, изменить дефолтный тариф на тариф апгрейда: «Комфорт» / «Комфорт+» для следующего заказа
https://st.yandex-team.ru/TAXIPROJECTS-1975

## Участвующие компоненты
1. Изначально выбранный тариф находится в order.request.class
1. Понять, что приехал тариф лучше заказанного можно по order_proc.candidates[performer_index].driver_classes, какой именно был выбран никуда не сохраняется
1. Баннер с поздравлением по поводу апгрейда тарифа собирается в taxiontheway [тут](https://github.yandex-team.ru/taxi/backend-cpp/blob/eaa093af50ed67e3d2ce7f31f5b9b881e02e8a36/protocol/lib/src/views/taxiontheway.cpp#L2613)  
Сейчас по эксперименту [higher_class_congratulation_settings](https://tariff-editor.taxi.yandex-team.ru/experiments3/experiments/show/higher_class_congratulation_settings?name=higher_class_congratulation_settings) определяется показывать баннер или нет. Эксперимент посчитали успешным и собираются включать показ поздравления вообще всегда ([тикет](https://st.yandex-team.ru/TAXIPROJECTS-1878)), точная дата неизвестна
1. Сохранение фидбека происходит в ручке /passenger-feedback/v1/feedback, запрос в которую проксируется из  3.0/feedback (протокольная, планиурется переход на api-porxy).  
feedback может дёргаться с фронта во время поездки, при нажатии на звёзды оценки + после поездки появляется экран оценки. С этого экрана feedback вызывается один раз по нажатии кнопки готово. Экран доступен в течении суток после окончания поездки
1. Тариф по умолчанию берётся из ответа 3.0/personalstate из поля selected_class. В сервисе user-state выбранный пользователем тариф хранится в mongo в коллекции [personal_state](https://github.yandex-team.ru/taxi/uservices/blob/e671b621df25513d18c20d7906ce73aa8991584d/schemas/mongo/personal_state.yaml#L26)

Необходимо для пользователей, у которых:
- приехала машина с классом выше, чем в заказе
- был показан баннер с поздравлениями
- поездка оценена в 5 звёзд

сохранять повышенный тариф как тариф по умолчанию

## Важно
Если пользователь ставит 5* и сразу делает заказ, заказ уже должен быть с обновлённым дефолтным тарифом.  
Поэтому тут не подойдёт асинхронная обработка (stq)

## Предлагаемое решение

Заводим в user-state postresql табличку user_state.upgraded_class_orders

```sql
CREATE SCHEMA user_state;

CREATE TABLE user_state.upgraded_class_orders (
    order_id TEXT NOT NULL,
    upgraded_to TEXT NOT NULL,
    yandex_uid TEXT NOT NULL,
    zone_name TEXT NOT NULL,
    brand TEXT NOT NULL,
    rating INTEGER,
    is_order_complete BOOLEAN NOT NULL DEFAULT FALSE,
    was_processed BOOLEAN NOT NULL DEFAULT FALSE,
    updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    
    PRIMARY KEY (order_id)
);
```

Заводим в user-state stq user_state_handle_class_upgraded
```yaml
name: user_state_handle_class_upgraded
arguments:
  - name: order_id
    required: true
    schema:
        type: string
  - name: upgraded_to
    required: true
    schema:
        type: string
  - name: yandex_uid
    required: true
    schema:
        type: string
  - name: zone_name
    required: true
    schema:
        type: string
  - name: brand
    required: true
    schema:
        type: string
```

Заводим в user-state stq user_state_handle_order_complete
```yaml
name: user_state_handle_order_complete
arguments:
  - name: order_id
    required: true
    schema:
        type: string
```

И ручку /internal/user-state/v1/update-order-rating
```yaml
/internal/user-state/v1/update-order-rating:
    post:
        parameters:
          - in: body
            name: body
            required: true
            schema:
                type: object
                properties:
                    order_id:
                        type: string
                    rating:     
                        maximum: 5
                        minimum: 1
                        type: integer
                    is_order_completed:
                        type: boolean
                required:
                  - order_id
                  - rating
                  - is_order_completed

        responses:
            '200':
                description: OK
                content:
                    application/json:
                        schema:
                            $ref: '#/definitions/EmptyResponse'
```

В totw при формировании поздравления пользователю ставить user_state_handle_class_upgraded  
В passenger_feedback при получении фидбека вызывать /internal/user-state/v1/update-order-rating в is_order_completed передавать флаг с флагом [order_finished_for_client=true](https://github.yandex-team.ru/taxi/uservices/blob/84e2a919a338cb261dac795a471cc25874c8af64/services/passenger-feedback/docs/yaml/api/save.yaml#L118). Флаг обязательный ставится в протоколе на основе статуса заказа [линк](https://github.yandex-team.ru/taxi/backend-cpp/blob/39021d68f9ae750e1d835d1ea61e33fa66e8c9c7/protocol/lib/src/views/feedback.cpp#L252). В случае ответа ошибкой/недоступности ручки остальная функциональность не должна быть затронута, поэтому фейлы игнорируются.  
В processing при завершении заказа ставить user_state_handle_order_complete.  

### user_state_handle_class_upgraded
Создаёт в таблице user_state.upgraded_class_orders запись и заполняет у неё поля order_id, upgraded_to, yandex_uid, zone_name, brand

### user_state_handle_order_complete
Проверяем, что заказ есть в базе. Если нет, значит для этого заказа апгрейда не было и таска завершается. Если есть - продолжаем.  
Записываем is_order_completed=true и выполняем логику изменения selected_class

### /internal/user-state/v1/update-order-rating
Проверяем, что заказ есть в базе. Если нет, значит для этого заказа апгрейда не было и ручка завершает работу. Если есть - продолжаем. 
Если is_order_comleted=false, то просто обновляем рейтинг и завершаемся.  
Если true, то записываем рейтинг, is_completed и выполняем логику изменения selected_class

### Логика изменения selected_class
Проверяем was_processed, если true - завершаемся, иначе - продолжаем.  
Если is_completed=false или rating!=5 - завершаемся, иначе - продолжаем.  
Обновляем selected_class, помечаем was_processed=true.  

### extra
Дополнительно нужно настроить чистку базы от записей, которые старше суток (можно через сервис архивации)

## Альтернативы
В качестве алтернативного решения, кажется, можно использовать Processing As A Service. Вместо постановки stq мы отправляем события в свой собственный процессинг. В нём следим за выполнением необходимых усовий и ставим stq на изменение selected_class. Если честно, не могу оценить насколько это подходящее решение для данной задачи

## Оценка нагрузки
Сейчас в пике /passenger-feedback/v1/feedback принимает ~300k запросов в час (~85rps)
https://kibana.taxi.yandex-team.ru/goto/95a0b76325d6ca81d564b75df5a69ce2  
Из processing будут ставится завершённые заказы, это ~100rps (смотрел по [этой очереди](https://grafana.yandex-team.ru/d/Wgn1XozWk/taxi_stq_tasks?orgId=1&refresh=30s&var-queues=support_proactivity_enqueue_chat&from=now-24h&to=now), которая ставится только на [handle_finish](https://github.yandex-team.ru/taxi/uservices/blob/a233473ed4e6b30976931615d895a15a3caa4583/services/processing/configs/config.user.yaml#L3247))
В totw баннер о поздравлении составляется на каждый вызов с назначения водителя и до конца поездки.
В день ~7кк запрсов, в среднем - ~81rps. Посчитано [тут](https://yql.yandex-team.ru/Operations/X79joRpqvxbBahAzxLZG3uCgEEu2HS7ck6qO-UlckM0=)  
Для уменьшения rps из totw, можно исопльзовать редис - кешировать факт показа поздравления об апгрейде тарифа и ставить stq только один раз. В этом случае rps должен быть по порядку схож с процессингом


## Оценка
1. Создать, мигрировать таблицу в pg - 4h
1. user_state_handle_class_upgraded - 1d
1. user_state_handle_order_complete - 1d
1. Вызывать ручку из passenger_feedback - 4h
1. Поставить stq из processing - 4h
1. Поставить stq из totw - 6h
1. Настроить очистку базы от старых записей - 2d

Итого ~6d

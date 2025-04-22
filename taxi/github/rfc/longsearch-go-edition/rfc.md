# RFC v.0.1.3

Хотим перенести опыт Uber в Go и Yango, добавив дополнительную ценность в анимацию и учитывая опыт конкурентов в международке (Bolt).

[Epic](https://st.yandex-team.ru/TAXIPROJECTS-3414)

[Figma](https://www.figma.com/file/1t7F660FW0QcVNXS9zirpf/%F0%9F%A4%8C-Core-Taxi-Quality?node-id=1455%3A30519)

[Miro](https://miro.com/app/board/uXjVOvOzHBE=/?share_link_id=684008049964) & [Сценарии поиска](https://st.yandex-team.ru/TAXIPROJECTS-3448)

[Uber experience](https://st.yandex-team.ru/TAXIPROJECTS-2830)

[Delta](https://delta.yandex-team.ru/page/epad/page/48gnufxqer6tw5rc)

[totw response](https://paste.yandex-team.ru/b5dff118-2452-4e0d-9b50-1de1ad77bf73)

## Description

Бизнесово задача выделяет разделение на этапе поиска водителя на 4 разные категории(ветки развития событий), тип категории, экран которой необходимо показать на клиенте будет приходить в totw в поле long_seach_info.search_type.

Текущий документ подразумевает проработку 1 конкретного случая (**обычный поиск 15-60 сек.**)

*000 Информация о поиске хранится в `Redis`, обновляется через `stx-tasks`

*001 Рисунок(граф) перехода между состояниями поиска

Клиент и бэкэнд обмениваются текущими статусами поиска, клиент отправляет последний полученный статус поиска + timestamp (AnimationSearch/state_ts,state_ts). Все решения по смене статусов, резолву конфликтов принимается и настраивается на бэкенде, задача клиента отобразить необходимое состояние, которые было получено последним.

При проблемах с сетью показываем панель, честно глясящую, что с соеденинем возникли проблемы.

Склонять тексты не будем, решили выбрать нейтральные, которые подойдут всем: в тайтле пишем "водитель". В том числе не будет проблем со сложными и длинными именами.

![figma image](screenshot/flow/default/name_desc.png)

---
    - *000 Больше деталей реализации на бэкенде?
    - *001 Граф переходов между стейтами

## Implementation:

Клиент должен учитывать, что-бы пришедший кандидат + маршрут до него + оффсет для анимации с баблами всегда вписывался в экран пользователя(focus rect). Если зума недостаточно, необходимо отзумить, что бы все объекты вписались на карту. Зумить к кандидату *НЕ* нужно.

### Long search DTO model, powered by totw btw:
---
#### Model:

##### Header

- X-Yataxi-Polling-Interval : (5_000) if null

##### Body

- long_seach_info
    - search type
    - eta
    - details card title << *локализовано by backend* уже тут
    - details card subtitle << *локализовано by backend*
    - candidate
        - id
        - coordinates [] 1+ length
        - view model
            - rating: str (trim up to .2)
            - photo url
            - driver name

---

### 0. Initiate long search

- После создания заказа на summary осуществляется переход на экран поиска (**Обычный поиск**).
- Плавный переход без дерганий и резких изменений масштаба от точки А на экран поиска `#p1`.

```html
paths:
    /totw:
        post:
            requestBody:
                required: true
                content:
                    application/json:
                        schema:
                            $ref: '#/components/schemas/TotwRequest'
            responses:
                200:
                    headers:
                        X-Yataxi-Polling-Interval:
                            schema:
                                description: |
                                    Интервал поллинга для клиента.
                                    Если отсутствует, то клиент считает его равным 5 секунд
                                type: integer
                                x-taxi-cpp-type: std::chrono::milliseconds
                    content:
                        application/json:
                            schema:
                                $ref: '#/schemas/TotwResponse'

schemas:
    TotwRequest:
        # первый уровень вложенности
        #...
        search_info:
            type: object
            description: |
              Текущее состояние анимации поиска.
              Если состояния нет, то весь объект не передается.
            properties:
                state:
                    description: Состояние
                    type: string
                    enum:
                      - search
                      - waiting_response
                      - rejected
                state_tp:
                    description: |
                        Временная метка текущего состояния.
                        Берется из предыдущего вызова totw.
                    type: string
                    format: date-time
            required:
              - state
              - state_tp

        #...

    StatusInfo:
        type: object
        description: Информация для карточки заказа
        additionalProperties: false
        properties:
            translations:
                type: object
                additionalProperties: false
                properties:
                    card:
                        type: object
                        additionalProperties: false
                        properties:
                            title_template:
                                description: Локализованный заголовок
                                type: string
                            subtitle_template:
                                description: Локализованный подзаголовок (опциональный)
                                type: string
                        required:
                          - title_template
                required:
                  - card
        required:
          - translations

    DriverPosition:
        description: |
            Информация о позиции водителя на карте
        additionalProperties: false
        type: object
        required:
          - lon
          - lat
          - direction
          - timestamp
        properties:
            lon:
                type: number
            lat:
                type: number
            speed:
                type: number
            direction:
                type: number
            timestamp:
                type: string

    PerformerInfoResponse:
        additionalProperties: false
        type: object
        properties:
            id:
                description: |
                    Идентификатор кандидата, зависит от `display_tariff` (см ниже). Бэк попробует сделать как из nearestdrivers.
                    Если для одного и того же водителя придут разные id из nearestdrivers и из totw, то клиент отрисовывает нового кандидата
                type: string
            display_tariff:
                description: Отображаемый тариф. От него зависит цвет машинки
                type: string
                example: 'econom'
            coordinates:
                description: Последние позиции водителя на карте. Пока что размер массива == 1.
                type: array
                items:
                    $ref: '#/schemas/DriverPosition'
            driver_name:
                description: Локализованное имя (first name) водителя. Опционально, тк при обращении ко внешним источникам может не прийти ответ
                type: str
                example: 'Иван'
            rating:
                description: |
                    Рейтинг как из totw (trim up to .2). Опционально, тк при обращении ко внешним источникам может не прийти ответ
                type: str
                example: '4.98'
            photo_url:
                description: URL на аватарницу. Опционально, тк при обращении ко внешним источникам может не прийти ответ
                type: str
                example: 'http://avatars.mdst.yandex.net/get-driver-photos/603/5b52ca28-cca0-4920-be83-283072a9ed3c/orig'
        required:
          - id
          - state
          - display_tariff
          - coordinates
          - driver_name

    SearchInfo:
        description: Информация для отображения анимации на клиенте во время поиска
        additionalProperties: false
        type: object
        properties:
            search_type:
                description: Тип поиска
                type: string
                enum:
                  - ordinary
            state:
                description: Состояние поиска
                type: string
                enum:
                  - waiting_response
                  - rejected
                  - search
            state_tp:
                description: Временная метка текущего состояния.
                type: string
                format: date-time
            has_previous_candidates:
                description: Предлагался ли уже заказ какому-нибудь кандидату
                type: boolean
            eta:
                description: |
                    Текущий eta для отображения на экране поиска.
                    Если отсутствует (в самом начале), то клиент показывает eta известный на момент пина
                type: integer
                minimum: 1
                x-taxi-cpp-type: std::chrono::seconds
            performer:
                description: |
                    Информация о текущем кандидате на заказ.
                    Если пустое, то кандидат еще не найден, либо предыдущий кандидат отказался
                $ref: '#/schemas/PerformerInfoResponse'
        required:
            - search_type
            - state
            - state_tp
            - has_previous_candidates

    TotwResponse:
        # первый уровень вложенности
        # ...
        status_info:
            description: Переопределение title и subtitle на карточке заказа
            $ref: '#/schemas/StatusInfo'
        #...
        search_info:
            $ref: '#/schemas/SearchInfo'
        #...


# Пример ответа, когда нет кандидата:
# Headers:
#     X-Yataxi-Polling-Interval: 3000
# Body:
# ...
# status_info: {
#     translations: {
#         card: {
#             title_template: 'Рядом с вами 12 машин',
#             subtitle_template: 'Ищем свободных водителей'
#         }
#     }
# }
# ...
# search_info: {
#     search_type: ordinary,
#     state: 'search',
#     state_tp: '2021-01-01T01:00:00+00:00',
# }
# ...


# Пример ответа, когда есть кандидат:
# Headers:
#     X-Yataxi-Polling-Interval: 3000
# Body:
# ...
# status_info: {
#     translations: {
#         card: {
#             title_template: 'Ждем ответа водителя',
#             subtitle_template: 'Обычно это занимает пару секунд'
#         }
#     }
# }
# ...
# search_info: {
#     search_type: ordinary,
#     state: 'waiting',
#     state_tp: '2021-01-01T01:00:00+00:00'
#     eta: 300,
#     performer: {
#         id: '1234556abcdef',
#         display_tariff: 'econom',
#         coordinates: [
#             {
#                 lon: 123.123,
#                 lat: 123.123,
#                 speed: 123,
#                 direction: 123,
#                 timestamp: '654321'
#             }
#         ],
#         driver_name: 'Иван'
#         rating: '5.00',
#         photo_url: 'http://avatars.mdst.yandex.net/get-driver-photos/603/5b52ca28-cca0-4920-be83-283072a9ed3c/orig',
#     }
# }
# ...
```


### 1. Старт поиска

![search started](screenshot/flow/default/search_started.png)

- Shadow overlay on top `#p9.0`. Только при старте поиска, любой последующий переход состояния отменяет наложение(больше наложение не появляется)
- Забираем машинки на экран поиска из nearest_driver. Без анимации движения.
- Забираем ETA с summary, обновляем из ответа ручки
- Анимация расходящихся кругов `p#9.1.1`.
- Backend присылает тексты для карточки поиска (title, subtitle)
- Title стартует анимацию shimmering-а.
- В сабтайтле "Рядом с вами Х машин":
    - пишем "более 5 машин", когда их 5 и более
    - пишем дефолтный текст без кол-ва машин, если машин < 3
    - после первого отказа перестаем писать про количество машин
- *102 Машины из nearest drivers не фильтруем по опциям в заказе – отложим в бэклог

    Например:

        - title: Рядом с вами 12 машин
        - subtitle: Начинаем поиск

        - title: Ищем водителя
        - subtitle: Рядом с вами 12 машин

---
    - *102 фильтр кандидатов nearest_drivers, которое мэчатся под критерии поиска


### 2. Кандидат найден:

![candidate found](screenshot/flow/default/candidate_found.jpg)

Из ручки, на клиент приходит информация отменил/принял ли водитель заказ.

- Backend присылает url с фото водителя.
- Из под кнопки отмены заказа анимированно выезжает иконка с текущим опрашиваемым кандидатом.
- При получении данных о водителе запускаем анимацию и начинаем грузить фото с дефолтным плейсхолдером.

    *201 Комонент кликабелен?
        - навигация на карточку водителя
        (*проработать кейс, когда штора открыта, а водитель сменяется*)

- Стартует анимация поллинга кандидата `#p9.2`
- Заказ отменен? goto `#p3.1` : goto `#p3.2`

---
    - *201 Кликабельность & навигация на карточку деталей о водителе  (скорее всего не будет поддержано)
    - *202 Запускать ли анимацию появления, если к моменту показа фото водителя не загрузилось, выпала ошибка?

### 3.1 Водитель отменил оффер

- "довести" анимацию из любого состояния в состояние, когда от пина до кандидата проложен маршрут (без баблов).
- анимация символизирующая отказ водителя от поездки `#9.1.3`
- Title & subtitle в карточке заказа с бэка
- goto `#p1`

### 3.2 Водитель принял оффер

- *320 здесь нам приходит driving и мы должны перейти на следующий экран, но мы специально задерживаем переход на экран driving-a в течении заранее заданного времени T (секунд/миллисекунд (приходит с бэка, или зашито на клиенте))
- довести анимацию поллинга из любого состояния в проложенный маршрут от пина до кандидата и остановить.
- haptic feedback (короткая вибрация, сообщающая пользователю, что водитель назначен)
- *321 анимация, показывающая, что водитель принял заказ.
- goto `#p4`

---
    - *320 какое время, как задаем  может ли бэк присылать информацию в ручке поллинга о том, что водитель принял заказ, а через некоторе время t в totw прислать driving?
    - *321 уточняется дизайном (зеленый blur, circle spinner or smth)


### 4. Driving

- плавный, анимированный переход без дерганий и резких изменений масштаба
- дальше экран без изменений

![driving](screenshot/state/driving.png)


### 7.0 Pitfals

- 7.1 Synchronization & data source truth.
    Самая большая проблема - сохранить синхронизацию между клиентом & backendом на критических участках(переходы между состояниями, важные изменения).
    Теоретически возможна ситуация, когда на клиенте накопиалсь очередь из анимаций, их все нужно проиграть(нельзя дропнуть) а рассинхрон растет неимоверными шагами.
    Что бы не загонять себя в угол и не принимать решение на клиенте - единственно верным решением кажется максимально дропать старые события и отдавать приоритет последним, даже в угоду ui/ux.
    Данная ситуация на текущий момент не кажется столь критичной, планируем вернуться к проработке и анализу после какой-то разработки(например 1 реализация mvp).

- 7.2 Reorder
[reorder](https://wiki.yandex-team.ru/users/vladazh/nagljadnye-reorder/swap-scenarii/)

В первой реализации дополнительно не заморачиваемся обработкой флоу реордера.
В большинстве случаев, смена произойдет адекватно, единственная сложность - поддержать плавные переходы между экранами.

---
    Не забыть:
    reorder (на ~ 1% заказов случается автореордер - когда водитель, выполняющий подачу “снимается” и ему ищется замена.)


### 8.0 Multiorder

- *800 В первой реализации решили не показывать какую-либо анимацию на экране мультизаказа.
При переходе в детали заказа с долгим поиском думаем не показывать анимацию тоже.

---
    - *800 Доля пользователей, которая проваливается в детали заказа при мультиордере ничтожна мала, что в теории дает нам шанс пренебречь реализацией(по крайней мере в первой итерации). Нужно исследовать


### 9. Компоненты:

- 9.0 Оверлей тени ака "паранжа"

- 9.1 Анимация расходящихся кругов

    - easing - чем дальше круг от центра, тем медленее анимация

- 9.1 Карточка деталей по заказу

    1. добавляется иконка водителя `#P9.2`
    2. при появлении анимация (*911 fade in) из-за кнопки отмены, выезжает от details/cancel button start в сторону card details start(противоположно кнопке details)
    3. при исчезании анимация (•911 fade out) перемещения за кнопку отмены(любую другую которая будет по центру, если кнопка отмены не там)


- 9.2 Иконка c информацией о водителе

    - рейтинг
    - фото профиля
    - имя


- 9.9 Анимация поллинга кандидата (ожидаем ответ от водителя)

    - *900 Animation steps. (время анимации взято из реализации долгого поиска в Uber Android)

        0. Кандидат въезжает в кадр с небольшим оффсетом и плавно fade in (1_000 ms.)
        1. Постепенно рисуем маршрут от точки А к кандидату (2_000 ms.)
        2. Когда маршрут доходит до машинки появляется анимация бабла с перебором троеточия (1_500 ms.).
        3. Постепенно стираем маршрут с карты в обратном порядке(от водителя к пину) (2_000 ms.)
        4. goto 1


    - Водитель отменил заказ:
        1. Прервать анимацию
        2. fade out машинки (600 ms.)

---
    - *900 время анимации в составных частях, хотим зашить или захардкодим?
    – *911 дизайн уточняет необходимость



### Changelog

- v0.1.3 Api model upd from 28.07.2022
- v0.1.2 Релили не склонять имена водитилей
- v0.1.1 Тело ответа totw. Передача текущего состояния с клиента на бэк. Мелкие доуточнения.
- v0.1.0 Определили место и алгоритм поллинга. Зафиналили модель ответа(с возможностью к изменениям в будущем), уточнили часть ответов из [delta](https://delta.yandex-team.ru/page/epad/page/48gnufxqer6tw5rc)
- v0.0.3 Уточнили место поллинга(totw) + префинализировали струкруту ответа
- v0.0.2 Решили, что не будем отказываться от "паранжи" - на клиенте синхронизируем нормальное появление без миганий.
- v0.0.1 snapshot after team meating

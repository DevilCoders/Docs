### Виджет для промо-блока Альтпина

Задача: показывать предложение по альтернативной точке посадки или высадки в промоплашке на экране обзора заказа.
Поддержать на бэке флоу, описанный здесь: https://www.figma.com/file/Q3E0wcxcsRV33UPvsntpJg/Альтпины

#### Основные изменения:

- Меняем текст сообщения о денежной выгоде альтпина на примерное значение, допускающее отклонения.
- Добавляем сборку новой промоплашки для promos_on_summary в inapp_communications: `altpin`
  и прокидываем её контекст из routestats в inapp_communications через PromoContext.
- Добавляем новый тип брендинга на экране summary: `altpin_price_soared`.
- Добавляем новый summary_context `"chosen_altpin"` в запрос в routestats.


#### Примерный сценарий при использовании альтпина:

1. Клиент переходит на summary screen и делает запрос в routestats
    с полем `"suggest_alternatives": true`
1. Routestats в backend-cpp при `"suggest_alternatives": true` отвечает с секцией alternatives,
    в которой выбрана предпочтительная альтернатива, а также определён список альтипнов,
    причём для каждого кроме прочего указаны:
    - локация альтпина
    - контекст для сборки промоплашки, содержащий мотивирующие и описательные сообщения
      (если это выгода в цене, то приблизительная) и контекст для перехода на экраны
      уточнения точки А и summary
    - сообщение бáбла для экрана уточнения
    - точная цена заказа из альтпина (пользователю не показывается,
      используется только для сравнения после пересчёта заказа)
1. Клиент делает запрос в inapp_communications,
    прокидывая в запросе контескт новой промоплашки.
1. Inapp_communications по эксперименту добавляет в ответ плашку, собранную
    из прокинутого из routestats контекста и конфига 3.0,
    с включающую контекст для экранов уточнения точки и summary.
    Плашка использует новый тип виджета для перехода на экран уточнения точек.
1. Клиент, отрисовывает промоплашку.
1. При нажатии на виджет промоплашки клиент запоминает все данные прошлого запроса в routestats,
    чтобы смочь его повторить, и показывает экран уточнения точки А,
    данные для которого берёт из контекста в плашке:
    - координаты
    - сообщение бáбла
    - оформление шторки
1. Пользователь (возможно) выбирает новую точку и нажимает кнопку подтверждения.
    Если был выбран альтпин, то запрос в routestats обогощается значением summary_context
    из контекста выбранного альтпина.
1. Routestats:
    - (uservices) при наличии контекста `"chosen_altpin"` подменяет нужную точку маршрута альтпином
      и устанавливает `"suggest_alternatives": false` и `"alternative_suggested": true`
    - (backend-cpp) при `"suggest_alternatives": false` отвечает без секции alternatives
    - (uservices) при наличии контекста `"chosen_altpin"` сравнивает цену нового актуального оффера с ценой,
      которую до этого увидел клиент для выбранной альтернативы.
      Если разница больше порога (достаётся из экспа),
      то в ответ с помощью brandings добавляется ремотивирующий баннер по banner_id (из того же экспа),
      который тянется клиентом из promotions (используется админка промок).
      Дальше флоу заказа как без альтпинов.


#### Изменения в routestats в backend-cpp

Обогощаем структуру `internal_data`:

```yaml
    InternalAlternative:
        description: альтернативные офферы
        type: object
        additionalProperties: false
        properties:
            offer_id:
                type: string
            type:
                type: string
            service_levels_data:
                type: array
                items:
                    $ref: "#/definitions/InternalServiceLevelData"
            plus_promo:
                $ref: "#/definitions/InternalAlternativePlusPromo"

            ### below comes new stuff ###
            point:
                additionalItems: false
                description: геокоординаты точки
                items:
                  - description: долгота
                    maximum: 180
                    minimum: -180
                    type: number
                  - description: широта
                    maximum: 90
                    minimum: -90
                    type: number
                minItems: 2
                type: array
            route_time_seconds:
                type: integer

        required:
          - offer_id
          - type
          - service_levels_data
          - point
```


#### Изменения в uservices routestats

Заводим новый плагин, который из коллекции альтернатив, полученных от backend-cpp,
генерирует контекст для inapp_communications, promos_on_summary.
Текстовые значения генерятся на основе эксперимента и могут содержать:
  - новую цену
  - разницу в цене из альтпина и из оригинальной точки
  - время пешком до альтпина
  - разницу во времени пешком до альтпина и до оригинальной точки
  - время в пути до конечной точки из альтпина
  - разницу во времени в пути до конечной точки из альтпина и из оригинальной точки
  - разные мотивирующие формулировки

Кроме этого, контекст содержит блок, на основе которого формируются действия клиента
при переходе к альтпину по промплашке:
  - тип точки альтпина
  - координаты альтпина
  - точная цена заказа

Также добавим ещё один плагин routestats для генерации ремотивирующего баннера.

Сейчас в ответе routestats секция alternatives проксируется через uservices из backend-cpp
без изменений.
Однако механизм с баннерами, который нам нужен в случае,
когда цена, предложенная в альтпине, вдруг поднялась после перехода на summary, находится uservices.
Поэтому целесообразно выполнить сравнение цен в uservices,
хотя остальная логика с альтпинами пока остаётся в backend-cpp.

Для отображения баннера при изменении цены мы воспользуемся структурой ServiceLevelBranding.
Мы добавим новый тип брендинга, `"altpin_price_soared"`, в который по эксперименту можем
подставлять разные баннеры из promotions по айдишнику.
Брендинг добавим в поле service_levels для того класса, для которого был создан оффер альтпина
(клиент передаёт его в `"selected_class"`).


#### Новый тип контекста promos_on_summary:

```yaml
   Amount:
       type: string
       maxLength: 20
       example: '12345.1434'
       description-ru: Сумма с фиксированной точностью
       description-en: Fixed-point sum

    AltpinPromoContext:
        description: данные для формирования промоплашки альтпина
        type: array
        items:
            description: данные об одном альтпине
            additionalProperties: false
            type: object
            properties:
                location:
                    $ref: definitions.yaml#/definitions/point
                point_type:
                    type: string
                price_new:
                    $ref Amount
                price_delta:
                    $ref Amount
                ride_time_minutes:
                    type: integer
                ride_time_delta_minutes:
                    type: integer
```


#### Расширение контекста summary_context

```yaml
    ChosenAltpinSummaryContext:
        description: данные о выбранном альтпине
        type: object
        additionalProperties: false
        required:
          - class
          - payload
        properties:
            class:
                type: string
                enum:
                  - chosen_altpin
            payload:
                type: object
                additionalProperties: false
                properties:
                    position:
                        $ref: "#/definitions/Point"
                    point_type:
                        type: string
                        description: a или b, откуда или куда
                    offer_price:
                        description: |
                            цена поездки из альтпина, предложенная пользователю ранее
                            для аналогичных параметров. берётся клиентом из поля `"new_price"`
                            контекста промоплашки выбранного альтпина.
                        type: string
                required:
                  - position
                  - point_type
                  - offer_price

    ClassSummaryContext:
        oneOf:
          - $ref: '#/definitions/DriveSummaryContext'
          - $ref: '#/definitions/ChosenAltpinSummaryContext'
        discriminator:
            propertyName: class
            mapping:
                drive: "#/definitions/DriveSummaryContext"
                chosen_altpin: "#/definitions/ChosenAltpinSummaryContext"
```


#### Изменения в inapp_communications:

Добавляем генерацию новой промоплашки при наличии контекста альтпина.

По эксперименту выбираем мотивирующие и уточняющие текстовые формулировки
в зависимости от степени выгоды по разным параметрам: цене, удалённости точки посадки
и общему времени в пути.

Примерная логика такая:

Сравниваем дельты с пороговыми значениями из эксперимента чтобы попасть
в одну из рубрик мотивирующих сообщений. Например, сильно сократилось время в пути.
Далее выбираем один из вариантов наполнения плашки в этой рубрике, например,
символ часов, большой текст "доберитесь на {ride_time_delta} быстрее" и мелкий текст
"а ещё и дешевле на {price_delta}".
Плейсхолдеры в сообщениях заменяются данными из контекста.
Для подписи пина на экране уточнения генерируем сообщение типа
"отсюда быстрее на {ride_time_delta}".

В сообщениях с ценами последние заменяются на приблизительные значения.


#### Новый тип виджета промоплашки:

```yaml
            widgets:
                type: object
                properties:
                    deeplink_arrow_button:
                        $ref: ...
                    attributed_text:
                        $ref: ...
                    drive_arrow_button:
                        $ref: ...
                    toggle:
                        $ref: ...
                    #### NEW ####
                    choose_altpin_button:
                        type: object
                        description: переход на экран уточнения точки с альтпином
                        properties:
                            altpin:
                                type: object
                                additionalProperties: false
                                description: описание альтпина на карте экрана уточнения
                                properties:
                                    position:
                                        $ref: "#/definitions/Point"
                                    point_type:
                                        type: string
                                        description: a или b, откуда или куда
                                    drawer_items:
                                        description: оформление шторки под картой
                                        $ref: '#/definitions/PromoblockContentArray'
                                    bubble_items:
                                        description: оформление бáбла альтпина на карте
                                        $ref: '#/definitions/PromoblockContentArray'
                                    routestats_summary_context:
                                        description: opaque context for routestats call on altpin confirmation
                                        $ref: '#/definitions/SummaryContext'
                                required:
                                  - position
                                  - point_type
                                  - drawer_items
                                  - bubble_items
                                  - routestats_summary_context
                            color:
                                type: string
                            items:
                                $ref: '#/definitions/PromoblockContentArray'
                        additionalProperties: false
                        required:
                          - altpin
                          - color
                          - items
```


#### Изменения на клиенте

Нужно сделать экран уточнения точек альтпинов.
Пока что поддерживается только точка А.
Добавить поддержку виджета choose_altpin_button.

После подтверждения уточнённой точки открывается summary.
Если на экране уточнения был выбран альтпин, нужно добавить в запрос routestats
блок summary_context из выбранного альтпина.


#### Заметки на будущее

Неплохо бы учитывать, что время прибытия складывается из времени до и после посадки.
Если пользователь потратит время, которое такси едет до места посадки, на перемещение
до более выгодной точки посадки, то время в пути пешком не увеличит суммарное время в пути,
потому как иначе пользователь потратил бы его на ожидание на своём месте или в пути к нему.

Отсюда ещё одно предложение развития: учитывать при построении рекомендаций альтпинов
не только выбранную пользователем точку А, но и его положение, если едет он сам.
Возможно, хорошее место посадки будет от пользователя в другом направлении,
чем где он планировал сесть.

Наверняка заинтересованность пользователей в разных характеристиках заказа можно оценить,
основываясь на реакции на плашки разного типа (время, цена, ...).
К примеру, кто-то не захочет идти лишние 2 минуты - для них стоит поднять порог по времени пешком.
Кто-то всегда торопится и хорошо мотивируется более ранним прибытием.
А кто-то перебежит автомагистраль чтобы сэкономить полтинник.
Этот профиль пользователя скорее всего будет более-менее постоянным.
Можно было бы сохранять статистику реакций на предложения с разной мотивацией и в inapp_communications
при сборке плашки их учитывать.

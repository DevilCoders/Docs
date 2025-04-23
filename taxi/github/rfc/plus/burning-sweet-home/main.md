# Сгорание баллов в домике
Если у пользователя скоро сгорят баллы, хотим ему об этом мягко намекнуть в домике.

Дезигн https://www.figma.com/file/zWSt3vNWyrVQPQYX7YI23B/Go-Плюс?node-id=45910%3A2828

![](./images/map_plaque.png) 
![](./images/summary_plaque.png)
![](./images/home_screen.png)
![](./images/native_screen.png)

## Что хотим
У пользователей в сентябре начнут сгорать баллы, с 1 августа планируется начать рассылать об этом коммуникации, призывающие купить подписку и, таким образом, отменить сгорание. Под сгорание попадают только пользователи, у которых нет и никогда не было подписки, а так же первые начисления датируются более чем за 6 месяцов до начала сгорания (Подробнее см. проработку Дани https://st.yandex-team.ru/TAXIBACKEND-35187)

### Краткая выдержка хотелок для этой проработки
* Уметь показывать иконку огонька в шильдике/бейджике в контексте сгорания баллов
* Уметь показать экран с информацией о сгорании баллов и кнопкой покупки подписки
* Точки входа на экран с информацией о сгорании:
  * Виджет в шильдике (с фоллбэком на открытие домика)
  * Шорткат (с фоллбэком на открытие домика)
  * Пуш (с фоллбэком на открытие домика)
  * Текст под балансом в домике (С фоллбэком на открытие домика??)
* Контроллировать периодичность показа шильдика (раз в несколько дней, несколько раз за сессиюю или на каком-то экране и тд.)
* Уметь перекрашивать шильдик/бейджик

## Как делæм
### Экран со сгоранием и покупкой

Так как контент динамический и присутствует очень симпатичная кнопка, а от вебвью решили отказаться, пришли к выводу делать нативный экран. Предлагаю следующие изменения:
В ответе ручки sdk-state положить поле typed_screens

```diff
responses:
    "200":
        description: ОК
        content:
            application/json:
                schema:
                    type: object
                    additionalProperties: false
                    properties:
                        state:
                            $ref: "#/components/schemas/UserState"
                        menu_type:
                            $ref: "#/components/schemas/MenuType"
                        menu:
                            $ref: "#/components/schemas/MenuV2"
                        menu_webview:
                            $ref: "#/components/schemas/MenuWebview"
                        plaque:
                            $ref: '../definitions/plaque.yaml#/components/schemas/PlaqueDefinitions'
                        typed_experiments:
                            $ref: '../definitions/experiments.yaml#/components/schemas/TypedExperiments'
+                       typed_screens:
+                           $ref: '../definitions/experiments.yaml#/components/schemas/TypedScreens'
+
+TypedScreens:
+   type: object
+   description: Клиентские экраны
+   additionalProperties: false
+   required:
+     - 'items'
+   properties:
+       'items':
+           type: array
+           items: $ref: '#/components/schemas/TypedScreen'
+TypedScreen:
+   type: object
+   additionalProperties: false
+   properties:
+      'type':
+         type: string
+         description: тип экрана
+         example: plus_burns
+       payload:
+           $ref: '#/components/schemas/ScreenPayload'
+   required:
+     - type
+     - payload
+
+ScreenPayload:
+   description: Наполнение нативного экрана
+   type: object
+   additionalProperties: false
+   properties:
+       title:
+           $ref: '#/components/schemas/AttributedText'
+       text:
+           $ref: '#/components/schemas/AttributedText'
+       background_image:
+           type: string
+           description: URL картинки на заднем фоне
+       image:
+           type: string
+           description: URL картинки под текстом
```
В payload положить всё необходимое для показа экрана. action_button работает как обычный, ходит в ручку покупки или апгрейда, в замисимости от экшена. Если прогрузить экран не получилось, фоллбэчимся на домик Плюса

### Иконка с огоньком и перекрашивание шильдика
Нужно в нескольких местах(на таблетке, в шильдике, в домике) рисовать иконку огня для сгорания. её можно:
1) Зашить на клиентах. Неудобно, потому что для изменения иконки нужно будет долго перевыкатывать клиенты
2) Присылать с бэка. Можно будет контроллировать какую иконку рисовать, но не без проблем:
  * В разных местах у иконки разные размеры. Можно:
    * Присылать с бэка картинки разных размеров, в зависимости от данных о разрешении экрана с клиентов. Усложняется апи, много логики на бэке по подбору нужной картинки.
    * Присылать одну картинку, но ресайзить её на клиентах. Артефакты при ресайзе растрового изображения могут простреллить колено, можно узнать, можем ли мы работать с вектором как на бэке так и на клиентах.
Так как правила отображения огня разные в разных местах (у таблетки на главной скрывается, если у пользовтаеля маленький баланс и он прочитал про сгорание), в шильдике только при сгорающем шильдике и т.д., то задавать этот огонь нужно отдельно для разных мест.

Есть три места, в которых нужно показать огонь и перекрасить цвета градиента:
1) Вместо нотификаций на главном экране иконка огня
2) В шильдике про сгорание баллов
3) В балансе в домике

Ввожу новую структуру, которая отвечает за стилизацию шильдика/таблетки/баланса, что бы это ни было 
```yaml
BadgeStyle:
    type: object
    description: Стиль отображения бейджика (цвет, вкус и тд)
    additionalProperties: false
    required: []
    properties:
        gradient_colors:
            type: object
            description: цвета градиента бейджика
            required:
              - bottom_left
              - top_right
            properties:
                bottom_left:
                    type: string
                    example: "#f19cbb"
                top_right:
                    type: string
                    example: "#cbbf19"
        icon:
            type: string
            description: >
                URL картинки в верхнем правом углу шильдика/бейджика.
                Например, иконка огня для сгорания
```
Если пришел badge_style, но в нем нет gradient_colors, то рисуется бейджик с "дефолтным" градиентом. Если пришло поле icon, то рисуется картинка (в нашем случае огонь)

### Вместо нотификаций на главном экране и в шильдике:
Нужно для пользователей с маленьким балансом показывать и скрывать при переходе в домик иконку огня, для пользователей с большим - держать перманентно. Граница с показом/непоказом должна контроллироваться с бэка, чтобы в том числе отключить этот огонь и не бесить пользователя. Продуктово нам ок, если огонь скроется только в следующей сессии. Из-за специфики отрисовки нотификаций на клиенте (они рисуются поверх бейджика на главной и шильдика) Предлагаю сделать примерно следующее:
Добавить в sdk-state.state поле badge_style
```diff
UserState:
    type: object
    description: Информация о состоянии пользователя.
    additionalProperties: false
    required:
      - wallets
      - subscription
      - settings
      - notifications
    properties:
        wallets:
            type: array
            items:
                $ref: '#/components/schemas/Wallet'
        subscription:
            $ref: '#/components/schemas/Subscription'
        settings:
            $ref: '../definitions.yaml#/components/schemas/VersionedSettings'
        notifications:
            $ref: '#/components/schemas/Notifications'
+       badge_style:
+           $ref: '#/components/schemas/BadgeStyle'
```
Если пришло поле badge_style, перерисовывать бадге и шильдик. Нам на бэке нужно определять факт того, что пользователь увидел "домик про сгорание", это очень похоже на typed_screen в виде домика, пришли к решению сделать следующее:
Добавить в ответе ручки sdk-state в поле menu поле home_type
```diff
MenuV2:
    type: object
    description: Описание UI-струкутуры меню.
    additionalProperties: false
    required:
      - balance_badge
      - sections
    properties:
        balance_badge:
            $ref: '#/components/schemas/BalanceBadge'
        action_button:
            $ref: '#/components/schemas/ActionButton'
        currency_rules:
            $ref: '#/components/schemas/CurrencyRules'
        sections:
            type: array
            items:
                $ref: '#/components/schemas/SectionV2'
+       home_type:
+           type: string
+           description: Тип домика, если пришел, считать домик за typed_screen
```
Его наличие будет означать, что сам домик является typed_screen, и его просмотр нужно будет сохранять и отправлять в запросе в sdk-state в поле existing_screens из пункта "Частотность показа шильдика". На бэке мы будем смотреть на последние даты просмотора экрана сграния и домика с информацией о сгорании под балансом, и принимать решение об отправлении огня на бейдж.

#### Огонь в домике на бейджике с балансом
Огонь на балансе в домике нужно будет рисоваь всегда, независимо от маленький/большой (только может быть при нулевом могут быть вопросы), поэтому он должен регулироваться отдельно, для этого стиль хочу положить в sdk-state.menu.balance_badge.style
```diff
BalanceBadge:
    type: object
    description: Беджик баланса одного кошелька.
    additionalProperties: false
    required:
      - show_glyph
    properties:
        subtitle:
            type: string
            description: Подпись под беджиком.
            example: "ваши баллы на Плюсе"
        placeholder:
            type: string
            description: |
                Замещающий текст, который будет показан вместо баланса в зависимости
                от разных условий, например: нулевой баланс, отсутствие информации
                о балансе, etc.
            example: "плюс"
        show_glyph:
            type: boolean
            description: Показывать ли глиф (изображение плюса) на беджике.
+       style:
+            $ref: '#/components/schemas/BadgeStyle'
```

### Шильдик про сгорание
Так как огонь рисуется везде, в шильдике, в домике, на микро_бадге на главном экране, то наличие огня лучше не привязывать к шильдику, тогда в виджете останется только тапабельный текст. Чтобы сделать тапабельный текст, предлагаю добавить новый тип виджета TEXT, а рядом положить action с диплинком
```diff
Widget:
    type: object
    description: Описание виджета - составной части шильдика.
    additionalProperties: false
    required:
      - widget_id
      - type
    properties:
        widget_id:
            $ref: '#/components/schemas/WidgetId'
        type:
            type: string
            description: |
                Тип виджета - определяет его внешний вид.
                Описание конкертного типа располагается в поле,
                соответствующем названию типа (например, `button` для
                типа `BUTTON`).
            enum:
              - BUTTON
              - SWITCH
              - BALANCE_CHANGE
              - BALANCE
+             - TEXT
        button:
            $ref: '#/components/schemas/ButtonWidget'
        switch:
            $ref: '#/components/schemas/SwitchWidget'
        balance_change:
            $ref: '#/components/schemas/BalanceChangeWidget'
        balance:
            $ref: '#/components/schemas/BalanceWidget'
+       text:
+           $ref: '#/components/schemas/TextWidget'
        # Тот самый action с диплинком. Если не придет, то виджет - обычный текст
        action:
            $ref: 'actions.yaml#/components/schemas/Action'

+TextWidget:
+   type: object
+   description: Виджет - текст.
+   additionalProperties: false
+   required:
+     - text
+   properties:
+       text:
+           type: string
+           description: Отображаемый текст.
+           example: "Баллы сгорят через 7 дней"
```
При нажатии на такой текст будет открываться экран про сгорание (предлагаю диплинком, рад услышать альтернативные предложения) 

### Кликабельный текст под балансом в домике
Так как меняется цвет текста, можно делать двумя вариантами
1) На клиентах под таблеткой в домике держать хтмльку вместо обычного текста (без изменений в апи, доработки на клиентах, немного на бэке)
2) Вместо обычного текста можно заиспользовать attributed text. Для этого понадобятся примерно такие изменения в апи:
```diff
BalanceBadge:
    type: object
    description: Беджик баланса одного кошелька.
    additionalProperties: false
    required:
      - show_glyph
    properties:
        subtitle:
            type: string
            description: Подпись под беджиком.
            example: "ваши баллы на Плюсе"
+       attributed_subtitle:
+           $ref: '#/components/schemas/AttributedText'
+       subtitle_action:
+           $ref: '../definitions/actions.yaml#/components/schemas/Action'
        placeholder:
            type: string
            description: |
                Замещающий текст, который будет показан вместо баланса в зависимости
                от разных условий, например: нулевой баланс, отсутствие информации
                о балансе, etc.
            example: "плюс"
        show_glyph:
            type: boolean
            description: Показывать ли глиф (изображение плюса) на беджике.
```
Если придут и subtitle и attributed_text - отдавать приоритет attributed_text. Если придет subtite_action - при нажатии на текст (неважно, attributed или обычный) выполнять необходимое действие

## Частотность показа шильдика
Не хотим, чтобы шильдик показывался слишком часто, поэтому разберу по пунктиках, что мы можем с этим сделать:

Шильдик распепячивается только для пользователей с >X баллов. Сейчас в эксперименты проползает баланс пользователя, можно использовать его для ограничения отображения шильдика, таким образом разработка не понадобится

Виджет показывается на ограниченное время (3 сек). Уже реализовано (по крайней мере, на бэке).

Есть временнные промежутки показа шильдика
* 30-15 дней до сгорания
* 15-3 дня до сгорания
* 3-0 дня до сгорания

В каждый из этих промежутков нужно минимум один раз распепячить шильдик.
Самый простой вариант добиться такого эффекта - использовать 3 разных plaque_id для этих временных промежутков. Возможно, прорастить время сгорания в эксперименты, чтобы добиться растроения шильдика.

Шильдик во временном промежутке не показывается, когда мы видели нативный экран про сгорание. В связи с чем хочу добавить в запросе в sdk-state новое поле existing_screens, в котором отправлять с клиентов информацию о последнем показе typed экранов. На бэке мы будем смотреть в это поле, если пользователю можно будет ещё раз показать этот экран, будем отдавать шильдик и typed_screen

```diff
SdkStateRequest:
    type: object
    additionalProperties: false
    properties:
        include:
            #...
        size_hint:
            #...
        supported_features:
            #...
        geo_state:
            #...
        existing_plaques:
            #...
+       existing_screens:
+           type: array
+           description: Информация об экранах, присутствующих на клиенте
+           items:
+               $ref: '#/components/schemas/ExistingScreen'

+ExistingScreen:
+   type: object
+   description: Информация об экране, сохраненном на клиенте
+   required:
+     - 'type'
+   additionalProperties: false
+   properties:
+       'type':
+           type: string
+           description: Тип нативного экрана
+       last_shown_at:
+           type: string
+           description: |
+               Время последнего показа typed экрана.
+               Если экран ни разу не был показан,
+               то это поле должно отсутствовать.
+           format: 'date-time'
+           example:
+             - '2021-02-27T08:00:00+03:00'
+             - '2021-02-27T08:00:00Z'
```

### Не показывать шильдик сразу после взаимодействия со сгоранием
Если во время сессии пользователь увидел домик про сгорание или экран сгорания, то шильдик про сгорание распепячиваться не должен. Есть несколько вариантов, как это можно сделать:
1) При взаимодействии со сгоранием перезапрашивать sdk-state, на бэке мы уже можем не присылать шильдик. Плюсы - больше ничего делать не нужно, минусы - сильно вырастет нагрузка на бэк
2) В условия показа шильдика положить поле unseen_typed_screens, куда положить списочек typed_screens. Если хотя бы один из них просмторен, шильдик НЕ показывать. Нужно будет уметь с бэка сбрасывать факт показа экрана, для этого рядом с typed_screens.items в ответе sdk-state положить items_to_delete.

Условия показа шильдика
```diff
SimpleCondition:
    type: object
    #...
    properties:
        screens:
            #...
        order_states:
            #...
        tariffs:
            #...
+       unseen_typed_screens:
+           type: array
+           description: Список type необходимых нативных экранов. 
+           items:
+               type: string
```

Список экранов, для которых нужно будет удалить факт показа
```diff
TypedScreens:
    type: object
    description: Клиентские экраны
    additionalProperties: false
    required:
      - 'items'
    properties:
        'items':
            type: array
            items: $ref: '#/components/schemas/TypedScreen'
+       items_to_delete:
+           type: array
+           items: string
+           description: Список типов typed_screens, для которых нужно удалить информацию о показе (last_shown_at)
```

3) Отдавать в ответе для шильдика unseen_typed_screen, куда положить время, через которое можно ещё раз показывать шильдик. Т.е. на клиенте лежит последнее время показа, в ответе придет дифф, показать еще раз можно будет через последнее время + дифф

```yaml
unseen_typed_screens:
    type: array
    description: Список id необходимых нативных экранов. 
    items:
        type: object
        additionalProperties: false
        properties: 
            'type': 
                type: string
                description: тип typed_screen
            last_shown_duration:
                type: string
                description: > 
                    Время, которое должно пройти с момента last_shown_at для typed_screen, чтобы можно было показать шильдик ещё раз

```
Если хотя хотя бы один typed_screen из списка unseen_typed_screens нельзя показывать из-за того что now < last_shown_at + last_shown_duration, шильдик не показывать. Так же возможно понадобится в ответе sdk-state отдавать время сервера

Мне больше нравится вариант под номером 2, так как на клиентах получается меньше логики

### Ограничение показа за сессию (Нужно ли?)
Хочется ограничить количество показов в принципе. Предлагаю для этого добавить новое поле sdk-state.plaque.plaques[].periodicity

```diff
Plaque:
    type: object
    description: Конечный шильдик.
    additionalProperties: false
    required:
      - plaque_id
      - layout
      - widgets
      - condition
      - priority
    properties:
        plaque_id:
            # ...
        layout:
            # ...
        widgets:
            # ...
        condition:
            # ...
        priority:
            # ...
        params:
            # ...
+       periodicity:
+           $ref: '#/components/schemas/PlaqueShowPeriodicity'
+
+PlaqueShowPeriodicity:
+   type: object
+   description: Параметры периодичности показа шильдика
+   additionalProperties: false
+   properties:
+       global:
+           $ref: '#/comonents/schemas/Periodicity'
+       session:
+           $ref: '#/comonents/schemas/Periodicity'
+
+Periodicity:
+   type: object
+   description: Периодичность показа
+   additionalProperties: false
+   properties:
+       max_show_count:
+           type: integer
+           description: Максимальное количество показов
+           minimum: 0
```
Для показа шильдика должны выполняться глобальные И сессионные условия периодичности. Если пришло только одно из них, то только одно. Если нет ни того, ни другого, условия периодичности считаются выполненными

## Скоуп на бэк:
* В домике получать информацию о сгорании(1d)
* typed_screens (3d)
* Виджет с текстом в шильдике (2d)
* BadgeStyle в трех местах (4d) 
* attributed_text в balance_badge и subtitle_action (2d)
* частотность показа шильдика(3d)

## Скоуп на клиенты(по мнению бэкендера):
* Поддержать новый виджет в шильдике
* Нативный экран с кнопкой
* Диплинк на этот экран
* Изменение типа шильдика по badge_style
* Научиться рисовать attributed subtitle под балансом с действием по нажатию
* Периодичность в шильдике

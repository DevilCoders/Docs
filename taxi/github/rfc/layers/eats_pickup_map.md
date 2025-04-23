# Карта ресторанов самовывоза в Yandex GO

## Задачи
1. Добавить на карту в приложении Яндекс GO новые объекты -- рестораны, предоставляющие услугу самовывоза.
2. Пользователи должны видеть рестораны в двух сценариях:
    * После перехода в режим Город
    * По тапу на баннер из webview Еды
3. Сделать отображение пинов и информации о ресторанах в Яндекс GO максимально консистентным с тем, как это выглядит в Яндекс Еде.

## Основные элементы карты -- как это реализовано В Яндекс Еде
Пины на карте отображаются в одном из четырех режимов --  hidden, small, medium и large.
Визуализация зависит от размера:
* Small -- только иконка. Изображение используется либо дефолтное (вилка и нож), либо в соответствии с главной категорией ресторана (Суши, Бургеры и т.д.).
* Medium -- иконка и наименование заведения справа от неё.
* Large -- иконка, справа от неё -- текст в две строки (название заведения и информация о рейтинге).

Рестораны начинают появляться на карте при достижении минимального валидного уровня зума (примерно 12 -- такого, чтобы на экране помещалась примерно вся Москва). При увеличении зума объекты на карте постепенно увеличивают свой размер, осуществляя переходы hidden -> small -> medium -> large.
Пороговые значения уровней зума, при достижении которых осуществляется переход, различны для всех ресторанов и зависят только от информации о заведении и пользователе.

Также на карте присутствуют кластеры, которые выглядят как пин размера Small без "ножки" со счётчиком в правом верхнем углу. Кластеры вычисляются динамически на каждый запрос. НЕ гарантируется, что при разных уровнях зума в кластер попадут одни и те же заведения а также, что центорид кластера не изменит свои координаты.

Кроме того, на пинах всех размеров (за исключением кластеров) может отображаться произвольная иконка в правом верхнем углу. Сечас это используется, чтобы пометить "избранные" заведения.


## Интеграция с Яндекс GO

### Новый режим приложения
Добавляется новый mode для состояния приложения -- restaurants.
```yaml
Mode:
    description: режим приложения
    type: string
    enum:
      - normal
      ...
      - city
      - restaurants
```

### Визуализация пинов на карте
#### Единичные заведения
Предлагается для отображения пинов на карте использовать объект `Bubble`. При отсутствии `style` и `simplified_style` баббл должен располагаться "ножкой" в точке объекта, при наличии -- над иконкой объекта.

Чтобы поддержать разные состояния пина в зависимости от зума, необходимо добавить массив `bubbles_list` в объект `PointProperties`. Диапазон зумов, в пределах которого виден баббл, задается полем `zooms`. Отрезки зумов в объектах массива `bubbles_list` следуют один за другим, так что конец одного отрезка совпадает с началом следующего. Объединение всех отрезков совпадает с полем `zooms`, заданным в `DisplaySettings`.
Поле `bubble` останется для обратной совместимости со старыми версиями клиентов. Бэкенд гарантирует, что в ответе будет присутствовать либо `bubble`,  либо `bubbles_list`, но не одновременно.

```yaml
PointProperties:
    type: object
    additionalProperties: false
    properties:
        ...
        bubbles_list:
            description: |
                Баблы объекта. Всплывают над объектом в зависимости от уровня зума.
            type: array
            items:
                $ref: "#/definitions/Bubble"
        ...
```

Сделать `Bubble` гибко настраиваемым под каждый вариант визуализации можно путем добавления новых `BubbleComponent`.
Все компоненты будут передаваться в массиве `components` и должны быть отображены на баббле один за другим, слева направо в порядке их следования в массиве. Размер баббла должен быть таким, чтобы обтекать все компоненты без зазоров по краям.

```yaml
Bubble:
    type: object
    description: Бабл для показа пользователю
    additionalProperties: false
    properties:
        ...
        components:
            type: array
            items:
                $ref: "#/definitions/BubbleComponent"
        selected_components:
            type: array
            items:
                $ref: "#/definitions/BubbleComponent"
        ...

BubbleComponent:
    oneOf:
        - $ref: "#/definitions/BubbleComponentText"
        - $ref: "#/definitions/BubbleComponentImage"
        - $ref: "#/definitions/BubbleComponentATText"
        - $ref: "#/definitions/BubbleComponentComposite"
```

Предлагаются следующие типы компонент:
1. Компонента с текстом: текст отбражается на одинаковом расстоянии от верхнего и нижнего краев баббла.
```yaml
BubbleComponentText:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - text
        value:
            type: string
            description: текст 
        font_style:
            type: string
            enum:
              - bold
              - italic
    required:
      - type
      - value
```
2. Компонента с изображением: картинка отображается на одинаковом расстоянии от верхнего и нижнего краев баббла.
```yaml
BubbleComponentImage:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - image
        value:
          oneOf:
            - $ref: "#/definitions/ATImageProperties"
            - $ref: "#/definitions/ATImageUrlProperties"
    required:
      - type
      - value
```
3. Компонента с AttributedText
```yaml
BubbleComponentATText:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
                - attributed_text
        value:
            $ref: "#/definitions/AttributedText"
    required:
        - type
        - value
```
4. Составная компонента: title отображается сверху, subtitle - под ним
```yaml
BubbleComponentComposite:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
              - composite
        title:
            $ref: "#/definitions/AttributedText"
        subtitle:
            $ref: "#/definitions/AttributedText"
    required:
      - type
      - title
      - subtitle
```

Также необходимо добавить опциональное поле `overlay` - бейджик в правом верхнем углу баббла, в котором может быть как изображение, так и текст.
```yaml
Bubble:
    type: object
    description: Бабл для показа пользователю
    additionalProperties: false
    properties:
        ...
        overlay:
            description: Бейдж в правом верхнем углу
            $ref: "#/definitions/BubbleOverlay"
        ...

BubbleOverlay:
    type: object
    additionalProperties: false
    properties:
        shape:
            type: string
            enum:
                - rounded_rectangle
        zooms:
            description: |
                диапазон зумов, в котором отображается оверлэй.
                Если объект находится в выбранном состоянии, то поле
                zooms игнорируется
            $ref: "#/definitions/Zooms"
        attributed_text:
            $ref: "#/definitions/AttributedText"
        show_states:
            type: array
            items:
                type: string
                enum:
                    - unselected
                    - selected
        background:
            type: object
            additionalProperties: false
            properties:
                color:
                    type: string
                meta_color:
                    $ref: '#/definitions/MetaColor'
                image_tag:
                    type: string
    required:
        - shape
        - zooms
        - attributed_text
        - show_states
```

#### Кластеры 
Пин кластера не меняет своего размера при увеличении зума и не "расхлопывается" на отдельные точки. Для кластера в объекте `style` будет дефолтная иконка (вилка и нож).  
Счетчик будет задан одним элементом в массиве `overlays` объекта `PointProperties`.

#### Attributed Text
Текущая спецификация `AttributedText` поддерживает только `image_tag`, поэтому предлагается расширить `properties`, добавив возможность задавать произвольную ссылку на картинку c помощью типа `ATImageUrlProperties`.
```yaml
AttributedText:
    additionalProperties: false
    properties:
        items:
            type: array
            items:
                oneOf:
                    - $ref: "#/definitions/ATTextProperties"
                    - $ref: "#/definitions/ATImageProperties"
                    - $ref: "#/definitions/ATImageUrlProperties"
    required:
        - items
    type: object

ATImageUrlProperties:
    type: object
    additionalProperties: false
    properties:
        type:
            type: string
            enum:
                - image_url
        image_url:
            type: string
        vertical_alignment:
            type: string
            enum:
                - baseline
                - center
        color:
            type: string
            pattern: "^#?[0-9A-Z]{6}"
        meta_color:
            $ref: '#/definitions/MetaColor'
    required:
        - type
        - image_url
``` 


### Обработка нажатия на пин

Предлагается передавать информацию о заведениях в ответе `/v2/objects`, чтобы убрать у клиентов необходимость производить дозапрос по нажатию на пин.
Для пина, соответствующего единичному ресторану, будет передаваться информация только о нем, для кластера -- о всех заведениях, которые в него входят.

Для единооборазия обработки нажатия на пин предлагаю добавить новый тип action'а `ShowShortcutsScreenAction` и расширить определение `Option`.

```yaml
Option:
    type: object
    additionalProperties: false
    properties:
        'on':
            $ref: "#/definitions/OptionTypeOn"
        keep_pin:
            type: boolean
        actions:
            description: Описание действия
            type: array
            items:
                oneOf:
                    ...
                    - $ref: "#/definitions/ShowShortcutsScreenAction"
    required:
        - 'on'
        - actions

ShowShortcutsScreenAction:
    type: object
    additionalProperties: false
    properties:
        type:
            description: Тип действия
            type: string
            enum:
                - show_shortcuts
        payload:
            description: Информация о шорткатах, которые нужно показать
            $ref: "#/definitions/ShortcutsActionPayload"
    required:
        - type
        - payload
```

Далее, в `PointFeature.options` передавать один элемент `Option` с полями `Option.on = tap`, `Option.keep_pin = true`, в массиве `Option.actions` -- один объект `ShowShortcutsScreenAction`. 

`ShortcutsActionPayload` должен по формату совпадать с единым форматом шорткатов, который возвращает сервис shortucts и ручка `/products/screen`.

## Архитектура

В сервис layers добавляется еще один провайдер restaurants. Запрос к нему осуществляется в состоянии приложения `mode = restaurants`, `screen = discovery`. 

Провайдер restaurants самостоятельно расширяет bounding box, пришедший в запросе, фильтрует найденные объекты и вычисляет zoom range. Следовательно, `FilteringManager` не должен добавлять никакой логики, а только ограничиваться походом в restaurants.

Провайдер будет получать объекты на карте и информацию о заведениях из ручки Еды. Предлагаю добавить новую ручку `/internal/v1/catalog-for-superapp-map` в сервис eats-catalog, которая повторяет логику поиска и обработки точек на карте за существующей ручкой `catalog-for-map`, но оличается от нее форматом ответа (отдает информацию о заведениях в виде шорткатов).

### Тайминги ответов
В настоящий момент 98-процентиль времени ответа `/internal/v1/catalog-for-map` составляет примерно 290-300 мс. 
В обработчкие `/v2/objects` будет производиться только запрос к апстриму и парсинг ответа. На издержки похода по сети будет потрачено не более 30 мс, на парсинг ответа -- не более 10 мс (по аналогии с eats-layout-constructor, который сечас обрабатывает ответ catalog-for-map).
В итоге, ожидаемое время ответа `/v2/objects` в режиме `restaurants` -- примерно 350 мс.

### RPS
Сейчас карта самовывоза работает на 100% пользователей Android в нативном приложении Еды. Текущий максимальный RPS -- не более 0.5 .
Учитывая, что процент DAU, который приходится на iOS и Andorid, составляет 47% и 22% соответственно, и конверсия на обеих платформах примерно одинакова, можно ожидать что после релиза на iOS общее количество запросов и объем трафика также увеличится примерно в 3 раза, итого 1.5 RPS.
DAU супераппа составляет около 17%, поэтому после включения карты в Яндекс GO RPS увеличится максимум до 2.

В скором времени планируется по нажатию на фильтр сразу переводить пользователя на карту. Сейчас количество сессий, начавшихся с нажатия на фильтр "С собой", составляет примерно 1,500 в пиковые часы, количество сессий, в которых присутствует нажатие на баннер -- примерно 165. Можно ожидать, что после включения сценария перехода с фильтра на карту RPS возрастет пропорционально количеству сессий, то есть в 1,500/165 = 9 раз.
Итоговый RPS на апстрим eats-catalog составит около 18, на сервис layers -- не больше 5.

На данный момент количество заказов самовывоза в день составяет примерно 1,500, продуктовые ожидания - достичь 5,000 заказов в день. Предполагая, что конверсия останется прежней, потенциально RPS может возрости еще в 50/15 раз. Следовательно, необходимо заложить ресурсов, чтобы потенциально выдержать 60 RPS.

### Ресурсы апстрима eats-catalog
Логика ручки `/catalog-for-map` по нагрузке на CPU пркатически аналогична `/catalog-for-layout`. RPS на `/catalog-for-layout` равняется примерно 60, на весь сервис eats-catalog -- 500. 
В пиковые часы каждый из 6 инстансов каталога потребляет 2 ядра. Можно примерно положить, что отдельно ручка `/catalog-for-layout` потребляет 60/500 * 2 * 6 = 1.5 ядра. 
Оцененное выше количество запросов к карте самовывоза равно 18, следовательно `/catalog-for-map` добавит примерно 18/60 * 1.5 ~ 0.5 ядра.

### Ресурсы layers
Учитывая, что сейчас сервис layers выдерживает больше 5,000 запросов в секунду, добавляемая нагрузка для него будет незаметной.

### Fallback'и

Предлагается сделать следующий фоллбек -- при недоступности сервиса eats-catalog либо увеличении таймингов или ошибочных ответов нового провайдера `/internal/v1/catalog-for-superapp-map` отключать кнопку "С собой" в режиме города.
Эта логика будет вынесена в ручку `/4.0/mlutp/v1/products/screen/city-mode`, которая будет использовать толстого клиента к сервису statistics для получения информации о метриках eats-catalog. 
Ручка `/v2/objects` сервиса layers будет отправлять статистику времен и кодов ответа апстрима `/internal/v1/catalog-for-superapp-map` в сервис statistics, где метрики аггрегируются и синхронизируются между разными инстансами. Ручка `/products/screen/city-mode` запрашивает эти метрики у сервиса статистик и, если 95-процентиль таймингов или доля ошибочных ответов превысили пороговые значения, перестает отдавать кнопку "С собой" клиентам.

Сервис layers проксирует ошибки провайдера `/internal/v1/catalog-for-superapp-map` клиентам. В случае, если `/v2/objects` ответила НЕ 200, клиент должен показывать пустую карту и не выполнять ретраев до следующего взаимодействия пользователя с картой.

Таким образом, если новый провайдер начнет деградировать, то нагрузка на него и Яндекс GO будет уменьшаться благодаря отключению кнопки, а пользователи, которые уже на карте либо дождутся восстановления функциональности, либо уйдут.

Следующим этапом разработки можно сделать фоллбек на тыкву -- статичный набор ресторанов, которые всегда активны и предоставляют услугу самовывоза. В случае ошибочного ответа провайдера сервис layers будет отдавать рестораны из статичного файла и `optimal_bbox`, достаточный, чтобы при отзуме на этот прямоугольник у пользователя появились несколько ресторанов на экране. Это предложение нуждается в предварительной продуктовой проработке.


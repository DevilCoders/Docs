
## Что хочется сделать:
[PRD](https://wiki.yandex-team.ru/users/tsolokhina/informer-v-ritejjle/)

Хочется уметь показывать информеры (текст с картинкой или просто картинка) на разных экранах Еды:
- главная поиска по магазинам 
- поиск внутри магазина 
- главная магазина
- категория магазина
- карточка товара

Можно увидеть, как это будет выглядеть тут:
[Ссылка на фигму](https://www.figma.com/file/Gt02EytPqiUN94dq84s4eT/Гарантия-качества-сборки?node-id=0%3A1)

Так же хотелось бы иметь централизованное место, где будут задаваться данные по информеру (картинки, надпись и тд), 
регулируются условия для показа и возможность управлять стратегиями показа(скрывать после 1-ого показа)

Уже есть похожее решение для баннеров, сторис с отдельной для этого [админкой](https://tariff-editor.taxi.tst.yandex-team.ru/eats-communications/inapp?type=eats-promotions-banner&status=all), 
в которой задаются данные баннеров, условия показов регулируются через привязанные к баннерам эксперименты.

Общая схема взаимодействия:
Админка коммуникаций <--> ```feeds-admin``` -(сохранение в БД в виде json)-> ```feeds``` <-получение фидов(баннеры, сторизы и тд)- ```eats-communications```
eats-communications ходить в feeds и получает фиды по 
Фид - json объект, который может быть баннеров, сториз, информеров и тд.
Фид получается по соответствующему ему каналу. Одному каналу может соответствовать несколько фидов. 
В случае баннеров каналом является название привязанному к этому баннеру эксперименту. 
Для баннеров в этом случае получаются все сматчившиеся эксперименты, у которых ```consumer```: ```eats-communications/eats-promotions-banner```, 
они и являются каналами для получения баннеров. В этих экспериментах прописываются условия для отображения баннеров по полученным кваргам

Предлагается сделать аналогичное решение для информеров, в котором eats-communications будет выступать источником баннеров для сервисов:
- eats-products (меню магазинов)
- eats-full-text-search (поиск)

[Диаграмма последовательностей: ./sequence_diagram.png](./sequence_diagram.png)

## Как хотим сделать

Предлагается использовать текущее решение для внедрения информеров с небольшими доработками

Дополнения к схеме взаимодействия:
```eats-communications``` <-(получение информеров)- ```eats-products```, ```eats-full-text-search```

По текущим требованиям в одном месте может быть отображен только 1 информер, 
потому eats-communications в случае нескольких информеров будет выбирать наиболее приоритетный

В сервисе eats-communication будут добавлены ручки, в которые будут ходить сервисы для получения коммуникаций.
Ручки будут универсальными, чтобы в них же была возможность получать коммуникации других типов, кроме информеров
Потребуется сделать ручки:

# eats-communications

### Ручка получения информеров для категорий меню ```/eats-communications/v1/categories/communications```
Так как в меню (```eats-products /api/v2/menu/goods/```) за раз отдается несколько категорий разных уровней, 
то необходимо сделать отдельную ручку, иначе придется делать запрос по каждой из категорий, а их может быть 10 штук за раз -> примерно 400 рпс из меню
Поэтому ручка будет принимать список категорией, а в ответе каждой категории при наличии будет соответствовать массив информеров.

#### Алгоритм работы ручки:
1. Сходить в eats-orders-stats, чтобы получить количестов заказов пользователя в ритейле
2. Проходим в цикле по всем категориям
   2.1. Составляем кварги с учетом текущей категории
   2.2. Получаем список экспериментов, которые сматчились с этими кваргами
   2.3. Добавляем в мапу, где ключ category_id, а значение массив экспериментов полученные значения
3. Из полученной мапы составляем сет всех сматчившихся экспериментов по всем категориям. Он же список каналов
4. По полученным каналам запрашиваем фиды
5. Проходим по всем фидам
   5.1. Проходим по мапе категория -> эксперименты
   5.1.1. Если в списке есть эксперимент, соответствующий полю experiment в фиде,
   5.1.2. То добавить в мапу, где ключ category_id, а значение список информеров в этой категории
6. В каждой категории отсортировать информеры по приоритету
7. Вернуть в ответе 1 информер по каждой категории, у которой он есть

Если один и тот же информер подходит разным категориям, то он будет возвращен во всех таких категориях, 
так как в данный момент требований по ограничению информеров на одну категорию нет.

### Ручка получения информеров для остальных экранов ```/eats-communications/v1/screen/communications```

#### Алгоритм работы ручки:
1. Сходить в eats-orders-stats, чтобы получить количестов заказов пользователя в ритейле
2. Составить кварги на основе данных ручки и результата 1 пункта
3. Получить по ним соответствующие каналы
4. Получить по всем каналам фиды
5. Преобразовать к ответу на фронт. При преобразовании будут учитывать картинки только нужной платформы(десктоп веб или мобилки)

Примерные спеки ручек описаны в файле [handlers.yaml](./handlers.yaml)
Кварги для информеров описаны в файле [informers_kwargs.yaml](./informers_kwargs.yaml)
Пояснения по кваргам:
- screen - экран, с которого пришел запрос (source в запросе)
- user_orders_retail_count - количество заказов пользователя в ритейле(получается из eats-orders-stats)

## Будущие доработки
При необходимости обе текущие ручки будут дорабатываться, чтобы принимать больше параметров, от которых зависит факт отображения информеров. 
В этих случаях в схемы ручек будут добавлены новые поля и они будут прокидываться в кварги получения экспериментов для информеров.
Например, количество товаров с признаком is_fresh


# feeds-admin
Для того, чтобы админка коммуникаций могла добавлять/изменять/удалять информеры необходимо внести изменения в сервис feeds-admin, 
который отвечает за взаимодействие с админкой и сохранением фидов в сервис feeds

## Изменения в спеке
Добавляется новый тип [InformerPayload](./feeds_spec.yaml)

Он добавляется к ```oneOf``` в поле ```payload``` (рядом с ```BannerPayload```) в ручках:
- ```/v1/eats-promotions/create```
- ```/v1/eats-promotions/update```
- ```/v1/eats-promotions/get```


## Изменения в коде
- Добавить в enum поля service значение eats-promotions-informer в /docs/yaml/api/v1_eats_promotions.yaml
- Дописать код, который позволит сохранять и получать данные информера. С виду кажется, что изменения будут в файлах: feeds_admin/api/get_eats_promotions_get.py, feeds_admin/services/eats_promotions.py
- Написать тесты в test_feeds_admin/web/services/test_eats_promotions.py


# Админка (фронт)
Для того, чтобы можно было редактировать информеры необходимо внести изменения в [админке](https://tariff-editor.taxi.tst.yandex-team.ru/eats-communications/inapp?type=eats-promotions-banner&status=all)

Добавить в админке Еда.Клиенты коммуникации новый тип "Информеры"
В ней будут поля, аналогичные вкладки Баннеры:

Основная информация:
- Название
- Приоритет
- Описание информера
- Стратегия показа

Публикация:
- Название эксперимента
- Расписание показа

Настройка показа:
- URL
- Диплинк

Настройка рекламы:
- Рекламный

Картинки:
- Тип информера: "Текстовый с картинкой", "Фоновый"
- Крестик закрытия информера (true/false)
  Для "Текстовый с картинкой" (объект TextWithImageInformerPayload в payload):
  - Текст: поле для ввода текста, галочка "Использовать ключ из танкера", цвет light и dark. (похоже на то как в сториз)
  - Картинка: кнопки "Выберите файл" для light и dark тем (Аналогично баннерам)
  - Фон: либо Цвет, либо изображение для light и dark тем (аналогично сториз)
  Для "Фоновый" (объект BackgroundInformerPayload в payload):
  - Фон: либо Цвет, либо изображение для light и dark тем (аналогично сториз)
  - Текст: (опциональный) поле для ввода текста, галочка "Использовать ключ из танкера", цвет light и dark. (похоже на то как в сториз)


# Клиенты новых ручек

## eats-products

Сервис будет отвечать за отображение информеров:
- на главной магазина
- в категориях меню магазина
- в карточке товара

Формат информера в eats-products
```
components:
    schemas:
        Informers:
            description: Список информеров для отображения. Если пустое, то ображать информеры не нужно
            type: array
            items:
                $ref: '#/components/schemas/InformerPayload'
```
### Информеры на главной магазина

При получении от фронта запроса ```/api/v2/menu/goods``` без указания категории, нужно сходить в ручку ```eats-communications``` ```/eats-communications/v1/screen/communications```
c ```screen``` = ```shop_main_page```, ```type``` = ```informers```, ```brand_id```, ```place_id```

В ответе ручки ```/api/v2/menu/goods``` в поле ```payload.communications.informers``` перемапить полученные информеры из eats-communications
```
payload:
    type: object
    additionalProperties: false
    required:
      - categories
      - communications
    properties:
        ...
        communications:
            type: object
            additionalProperties: false
            required:
              - informers
            properties:
                informers:
                    $ref: '#/components/schemas/Informers'
```
### Информеры в категориях

При получении от фронта запроса ```/api/v2/menu/goods``` с указанием категории, нужно после получения всех данных о товарах и категориях из номенклатуры сходить в
ручку ```eats-communications``` ```/eats-communications/v1/categories/communications```
с ```screen``` = ```shop_category```, ```type``` = ```informers```, ```brand_id```, ```place_id```. А в поле ```categories``` вписать нужные данные по всем категориям.

В ответе ручки ```/api/v2/menu/goods``` в поле ```payload.categories.communications.informers``` по каждой категории из ответа eats-communications перемапить полученные информеры
```
Category:
    type: object
    additionalProperties: false
    required:
        ...
      - communications
    properties:
        ...
        communications:
            type: object
            additionalProperties: false
            required:
              - informers
            properties:
                informers:
                    $ref: '#/components/schemas/Informers'
```

### Информеры в карточке товара

В ручке ```/api/v2/menu/product``` после получении информации о товаре, сходить в ручку ```eats-communications```
```/eats-communications/v1/screen/communications``` c ```screen``` = ```product_card```, ```type``` = ```informers```, ```brand_id```, ```place_id``` ,
чтобы получить информеры, которые будут отображены в карточке товара.
Для этого поле ```detailed_data``` будет расширено новым типом.
Новый блок при наличии информеров будет добавляться до блока Header
```
detailed_data:
    description: >
        Данные для отображения в карточке. На фронте
        отображаются в отданном порядке.
    type: array
    items:
        oneOf:
          - $ref: '#/components/schemas/Gallery'
          - $ref: '#/components/schemas/Header'
          - $ref: '#/components/schemas/ProductDescriptions'
          - $ref: '#/components/schemas/Separator'
          - $ref: '#/components/schemas/EnergyValues'
          - $ref: '#/components/schemas/UpsellRecommendations'
          - $ref: '#/components/schemas/DetailedDataInformers'
        discriminator:
            propertyName: type
            mapping:
                gallery: '#/components/schemas/Gallery'
                header: '#/components/schemas/Header'
                description: '#/components/schemas/ProductDescriptions'
                separator: '#/components/schemas/Separator'
                energy_values: '#/components/schemas/EnergyValues'
                upsell_recommendations: '#/components/schemas/UpsellRecommendations'
                informers: '#/components/schemas/DetailedDataInformers'

DetailedDataInformers:
    type: object
    additionalProperties: false
    required:
      - type
      - payload
    properties:
        type:
            type: string
            enum: [informers]
        payload:
            type: object
            additionalProperties: false
            required:
              - informers
            properties:
                informers:
                    $ref: '#/components/schemas/Informers'
```


## eats-full-text-search

Сервис будет отвечать за отображение информеров:
- при поиске на главной во вкладке "Магазины"
- при поиске внутри магазина

### Изменения спеки
В ручке ```/eats/v1/full-text-search/v1/search``` в поле ```blocks``` поле ```type``` расширяется новым типом ```informers```
```
SearchResponseBlock:
    type: object
    additionalProperties: false
    required:
      - title
      - type
      - payload
    properties:
        title:
            type: string
            description: Назвение блока поисковой выдачи
            example: Совпадения в других категориях
        type:
            type: string
            enum:
              - selector
              - places
              - items
              - categories
              - banners
              - separator
              - informers
            description: Тип блока поисковой выдачи - блок с ресторанами,
                с категориями, элементами меню
        payload:
            oneOf:
              - $ref: "#/components/schemas/SelectorBlock"
              - $ref: "#/components/schemas/PlacesBlock"
              - $ref: "#/components/schemas/ItemsBlock"
              - $ref: "#/components/schemas/CategoriesBlock"
              - $ref: "#/components/schemas/BannersBlock"
              - $ref: "#/components/schemas/SeparatorBlock"
              - $ref: "#/components/schemas/InformersBlock"

InformersBlock:
    description: Список информеров для отображения
    type: array
    items:
        $ref: '#/components/schemas/InformerPayload'
```

### Информеры при поиске товаров на главной странице Еды
Необходимо при поиске товаров внутри магазина получать информеры

Для этого нужно:
1. Расширить ```models::SearchResponse``` полем ```std::vector<clients::eats_communications::InformerPayload> informers```
2. В ```GetCatalogSearchResponseLayout``` ходить в ручку ```eats-communications``` ```/eats-communications/v1/screen/communications``` 
   с ```source``` = ```search_main_shops```, ```type``` = ```informers``` (по флагу ```request_params.selector_storage.IsShopSelectorSelected()```)
3. В ```CatalogSearchLayoutBuilder``` прокидывать полученные информеры и в ```Build``` добавлять в ```blocks_layout``` новый ```InformersBlockLayout```

### Информеры при поиске товаров внутри магазина
Необходимо при поиске товаров внутри магазина получать информеры

Для этого нужно:
1. Расширить ```models::SearchResponse``` полем ```std::vector<clients::eats_communications::InformerPayload> informers```
2. В ```GetMenuSearchResponseLayout``` ходить в ручку ```eats-communications``` ```/eats-communications/v1/screen/communications``` 
   с ```source``` = ```search_inside_shop```, ```type``` = ```informers``` (только для ```PlaceBusiness::kShop```)
3. В ```MenuSearchLayoutBuilder``` прокидывать полученные информеры и в ```BuildShopMenuSearchLayout``` и ```BuildShopCategorySearchLayout``` добавлять в ```blocks_layout``` новый ```InformersBlockLayout```


# Фронт:
Схема самих информеров описана в [informers_spec.yaml](./informers_spec.yaml)
1. При заходе в магазине, если в запросе ```/api/v2/menu/goods``` (без указания категории) в ответе в ```payload.communications.informers```
   пришли информеры, отобразить их на главной магазина.
2. При запросе категорий ```/api/v2/menu/goods``` с указанием категории, если в ответе по категориям в полях ```payload.categories.communications.informers```
   пришли информеры, то отобразить их в соответствующих категориях
3. При запросе ручки детальной информации о товаре ```/api/v2/menu/product```, если в поле ```detailed_data``` пришел тип ```informers```,
   то отобразить эти информеры
4. При запросе ручки поиска ```/eats/v1/full-text-search/v1/search``` в случае получения в ```blocks``` значения ```type``` == ```informers```, 
   отображать информеры в соответствуещем месте ( поиск на главной Еды, или поиск по магазину)
5. Если у информера есть ссылка (deeplink или url в зависимости от платформы), на нем нужно отобразить кнопочку перехода (в фигму будет добавлено попозже)
6. Если у информера `has_close_button` == true, то у пользователя должна быть возможность закрыть этот информер.
   Если пользователь нажал на кнопку закрытия информера, то необходимо вызывать ручку `/eats/v1/eats-communications/v1/viewed` c id информера, `type` = `informer`, чтобы отметить информер просмотренным
   [Ссылка на спеку ручки](https://a.yandex-team.ru/arc_vcs/taxi/uservices/services/eats-communications/docs/yaml/api/viewed.yaml)
7. При получении информера неизвестного типа в payload.type, такой информер отображать не нужно

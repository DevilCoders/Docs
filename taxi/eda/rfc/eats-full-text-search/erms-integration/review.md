# Интеграция с сервисом eats-rest-menu-storage

В рамках данного проекта хотим отказаться от
использование ElasticSearch в поиске и заменить его
связкой eats-rest-menu-storage и saas.

## Индексация

В части индексации предлагается переиспользовать схему ретейла с stq и вызовом
http ручки сервиса меню внутри таски, но с тем изменением, что в stq будут идентификаторы
изменившихся айтемов. И запрос в erms будет происходить только по изменившимся айтемам.

Так при изменении меню erms будет генерировать stq задачу на fts-indexer, тот в
параметраз задачи получает идентификаторы изменившихся айтемов, запрашивает их
из erms и отправляет изменения в saas.

Аргументы stq задачи

```yaml
UpdateRestPlaceParams:
  type: object
  required:
    - place_id
    - updated
    - deleted
  properties:
    place_id:
      type: string
      description: Идентификатор заведения, в котором обновились айтемы
    updated:
      type: array
      items:
        type: string
        description: Идентификаторы обновленных(добавленных или измененных) айтемов
    deleted:
      type: array
      items:
        type: string
        description: Идентификаторы удаленных навсегда айтемов
```

При этом в eats-rest-menu-storage нужно
завести отдельную ручку с минимальной информацией о товарах.
Текущая ручка get-items (аналог get-items в коре и eats-products),
не подходит так как содержит полные карточки товаров c опциями, что
требует дополнительных запросов в базу, раздувает ответ, но эти данные
для индексации не нужны.
При этом эту же ручку можно переиспользовать для вывода товаров в поисковой выдаче
при поиске на главной.
Предлагаемая [спека](./api/item_preview.yaml)

Схема взаимодействия при индексации:

![indexing](./img/indexing.svg)

<!--
@startuml img/indexing.svg

"eats-rest-menu-storage" -> "eats-full-text-search-indexer": stq place_id, updated_ids, deleted_ids
"eats-full-text-search-indexer" -> "eats-rest-menu-storage": item_preview place_id, updated_ids
"eats-full-text-search-indexer" -> "saas_push": Параллельно удаляем deleted_ids айтемы
"eats-full-text-search-indexer" <- "eats-rest-menu-storage": карточки айтемов
"eats-full-text-search-indexer" -> "saas_push": Идентификаторы и название обновленных айтемов
@enduml
-->

Для более безопасного переключения, новые данные
будут заливаться в отдельный kps в saas.
Для ретейла мы в saas сейчас отгружает не только название по которому
идет поиск, но и всякие полузные данные: описание, картинка, вес, цена...
Но как показывает опыт переезда на мастер меню и маркетный поиск, лучше
эти данные получать в рантайме поиска, а не хранить в поисковом индексе.

## Поиск по меню

При поиске по меню предлагается аналогичная схема как в ретейле.
Матчим айтемы из saas, затем идем в ручку get-items и получаем полную карточку товара
с опциями, преобразовываем в формат клиента и отдаем.

![menu_search](./img/menu_search.svg)

<!--
@startuml img/menu_search.svg

"client" -> "eats-full-text-search": Поисковый запрос
"eats-full-text-search" -> "saas": Идентификатор заведения и поисковая фраза
"eats-full-text-search" <- "saas": Идентификаторы сматченных товаров
"eats-full-text-search" -> "eats-rest-menu-storage": Запрос полной карточки товаров get-items
"eats-full-text-search" <- "eats-rest-menu-storage": Полная информация о каточки товара
"client" <- "eats-full-text-search": Поисковая выдача в формате клиента
@enduml
-->

## Поиск с главной

Про поиске с главной в случае ретейла мы сейчас все равно запрашиваем
все данные из eats-nomenclature, хотя не все нудны для ответа клиентам.
Поэтому тут схема аналогичная поиску по меню за исключением
того что запрашиваем не get-items, а items-previw

![catalog_search](./img/catalog_search.svg)

<!--
@startuml img/catalog_search.svg

"client" -> "eats-full-text-search": Поисковый запрос
"eats-full-text-search" -> "saas": Идентификаторы заведений по точке и поисковая фраза
"eats-full-text-search" <- "saas": Идентификаторы сматченных товаров
"eats-full-text-search" -> "eats-rest-menu-storage": Запрос минимальной карточки товара items-preview
"eats-full-text-search" <- "eats-rest-menu-storage": Минимальная информация о товарах
"client" <- "eats-full-text-search": Поисковая выдача в формате клиента
@enduml
-->

# Ресурс /vendors/[vendorID]/recommended/blacklist

## GET /vendors/[vendorID]/recommended/blacklist

Получение магазинов из "чёрного списка" услуги "Рекомендованные магазины"

### Примечание
  - В чёрный список магазины добавляет менеджер, по запросу от этих магазинов
  - Сам вендор напрямую этого списка не видит
    - Но видит эти магазины в своём списке помеченными как отказавшиеся (status=`REFUSED`)

### Параметры
  - **uid** `<UID>` - ID пользователя для аутентификации
  - [Параметры пагинации](/_entities/Pager.md#Параметры)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array>`
          - **id** `<Integer>` - shopId магазина
          - **name** `<String>` - название магазина
          - **domain** `<String>` - домен магазина
          - rating `<Integer>` - рейтинг магазина
          - clones `<Array [Object]>`
            - **id** `<Integer>` - shopId клона
            - **name** `<String>` - название клона
            - **domain** `<String>` - домен клона
            - **status** `<VendorShopStatus>` - перечислимый тип для статуса рекомендованного магазина, описанный [тут](/_entities/VendorShopStatus.md)            
          - **bid** `<Integer>` - ставка в центах
        - **status** `REFUSED` - здесь везде будет `REFUSED`, так как эти магазины отказались от участия в программе
    - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

### Вопросы
  - Нужно ли делать здесь поиск по магазину?
  - Сейчас выдача идентична выдаче ручки /shops. Нельзя ли выкинуть какие-то поля?

## POST /vendors/[vendorID]/recommended/blacklist

Добавление магазинов в чёрный список услуги "Рекомендованные магазины"

### Параметры
  - **uid** `<UID>` - ID пользователя для аутентификации

### Данные
  - **identifiers** `<Array[Integer]>` - идентификаторы магазинов, которые нужно добавить
    - *Здесь мы ожидаем только* ***shopId***

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Array[Object]>`- результаты добавления магазина в чёрный список
      - **identifier** `<String>` - идентификатор магазина
      - **status** `<Boolean>` - статус добавления
      - reason `<Error>` - в случае неуспешного добавления, причина, иначе отсутствует
        - *некоторые возможные причины –  "Магазин не найден", "Уже добавлен", etc.*
      - shop `<Object>` - в случае успешного добавления, данные магазина, иначе отсутствует
         - **id** `<Integer>` - shopId магазина
         - **name** `<String>` - название магазина
         - **domain** `<String>` - домен магазина
         - **status** `<VendorShopStatus>` - перечислимый тип для статуса рекомендованного магазина, описанный [тут](/_entities/VendorShopStatus.md)     
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Не передан параметр identifiers](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

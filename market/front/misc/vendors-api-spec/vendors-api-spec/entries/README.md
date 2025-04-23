# Ресурс /entries

## POST /entries

Подача заявки и принятие оферты

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - **company** `<String>` - юр лицо, подающее заявку
  - **name** `<String>` - контактное лицо
  - **phone** `<Phone>` - телефон
  - **email** `<Еmail>` - e-mail
  - **address** `<String>` - адрес текстом
  - **brands** `<String|String[]>` - имена брендов для заявки
    - *передаются в виде списка либо строкой с разделителями, пока не решили*
  - **documents** [`<Array[Document]>`](/_entities/documents/Document.md) - список документов,
    подтверждающих право принятия оферты (пока опционально)
  - sites `<Array[String]>` - список ссылок на официальные сайты перечисленных брендов

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **status** `NEW`
      - **company** `<String>` - возвращено переданное юр лицо, подающее заявку
      - **name** `<String>` - возвращено переданное контактное лицо
      - **phone** `<Phone>` - возвращен переданный телефон
      - **email** `<Еmail>` - возвращен переданный e-mail
      - **address** `<String>` - возвращен переданный адрес текстом
      - **brands** `<String|String[]>` - возвращены переданные имена брендов для заявки
      - **offer** `<Boolean>` - маркер принятия заявителем оферты, для новых заявок всегда должен быть true
      - **offerAcceptedUid** `<Long>` - UID пользователя, принявшего оферту
      - **offerAcceptedTime** `<Date>` - время принятия оферты
      - **documents** [`<Array[Document]>`](/_entities/documents/Document.md) - список документов,
        присланных в заявке.
      - sites `<Array[String]>` - список ссылок на официальные сайты перечисленных брендов
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/brands-api-spec#Стандартные-ошибки)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### У этого пользователя уже есть заявка в статусе NEW или ACCEPTED
#### [Ошибки работы с документами](/_rules/documents/DocumentErrors.md)

##### Примечания
  - Если заявка пользователя отменена, кажется, что можно позволить ему отправить повторную заявку
  - [Правила работы с документами](/_rules/documents/DocumentRules.md#postинг)
  - [Правила работы с документами в "оферте"](/_rules/documents/OfferDocumentRules.md)

##### Структура
  - statusCode: `409 CONFLICT`
  - code: `ALREADY_EXISTS`
  - message: `Current user has already submitted an entry`

## GET /entries

Поиск заявок по параметрам

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации
  - status `Array(NEW|IN_WORK|ACCEPTED|CANCELLED)` - статус заявки
  - text `<String>` - поиск по всем текстовым полям
  - managerLogin `<String>` - фильтрация по логину менеджера, взявшего заявку в работу
  - [Параметры пагинации](/_entities/Pager.md#Параметры)

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **pager** [`<Pager>`](/_entities/Pager.md)
      - **items** `<Array>`
        - **id** `<Integer>` - идентификатор заявки
        - **company** `<String>` - юрлицо, отправившее заявку
        - **status** `NEW|IN_WORK|ACCEPTED|CANCELLED` - текущий статус заявки
        - **creationDate** `<DateTime>` - время создания заявки
        - **lastModifiedDate** `<DateTime>` - время последней модификации заявки
        - **uid** `<UID>` - идентфикатор пользователя, создавшего заявку
        - **login** `<String>` - логин пользователя, создавшего заявку
        - **unknownBrands** `<String[]>` - имена нераспознанных при создании заявки брендов
        - **brands** [`<Array[Brand]>`](/_entities/Brand.md) - распознанные при создании заявки бренды
        - manager [`<User>`](/_entities/User.md) - менеджер, взявший заявку в обработку
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)

##### Примечания
Обработанные и отклонённые заявки отдаются вендору только в течение 2-х недель после смены статуса заявки.

## Доработки

 - Нужно добавить метод добавления/удаления бренда в заявку
 - Нужно добавить метод редактирования списка не определенных автоматически брендов в заявке
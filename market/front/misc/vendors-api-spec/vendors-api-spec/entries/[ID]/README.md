# Ресурс /entries/[ID]

## GET /entries/[ID]

Получение информации о заявке

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - meta `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **id** `<Integer>` - идентификатор заявки
      - **uid** `<UID>` - идентфикатор пользователя, создавшего заявку
      - **login** `<String>` - логин пользователя, создавшего заявку
      - **status** `NEW|IN_WORK|ACCEPTED|CANCELLED` - текущий статус заявки
      - **company** `<String>` - юрлицо, отправившее заявку
      - **name** `<String>` - контактное лицо
      - **phone** `<Phone>` - контактный телефон
      - **email** `<Еmail>` - контактный e-mail
      - **address** `<String>` - адрес
      - **creationDate** `<DateTime>` - время создания заявки
      - **lastModifiedDate** `<DateTime>` - время последней модификации заявки
      - **offer** `<Boolean>` - маркер принятия заявителем оферты, для новых заявок всегда должен быть true
      - **offerAcceptedUid** `<Long>` - UID пользователя, принявшего оферту
      - **offerAcceptedTime** `<Date>` - время принятия оферты
      - **documents** [`<Array[Document]>`](/_entities/documents/Document.md) - список документов оферты
      - brands `<Array[Object]>` - cписок брендов в заявке
        - **id** `<Integer>` - id бренда
        - **name** `<String>` - имя бренда
      - unknownBrands `<Array[String]>` - неизвестные бренды, которых не получилось распарсить (массив названий)
      - sites `<Array[String]>` - список ссылок на официальные сайты перечисленных брендов
      - manager [`<User>`](/_entities/User.md) - менеджер, взявший заявку в обработку
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такой заявки](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

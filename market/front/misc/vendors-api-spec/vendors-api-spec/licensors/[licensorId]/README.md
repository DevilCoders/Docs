# Ресурс /licensors/[licensorId]

## GET /licensors/[licensorId]

Получение полной информации о лицензиаре по его licensorId

### Примечания
  - Получение карточки доступно для менеджера, "читающего" менеджера, суппорта и всех ролей лицензиара (на текущий момент админ и управленец контентом)

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **licensorId** `<Integer>` - идентификатор карточки лицензиара
      - marketId `<Integer>` - маркетный идентификатор лицензиара, присутствует если лицензиар распознан
      - **title** `<String>` - отображаемое имя карточки
        - *выводится в верхней шапке в выпадающем списке*
        - *является уникальным как среди вендоров, так и лицензиаров и может служить для идентификации и поиска карточки*
      - **company** `<String>` - имя компании лицензиара
      - **address** `<String>` - юридический адрес компании лицензиара
      - **name** `<String>` - контактное лицо
      - **phone** `<Phone>` - контактный телефон
      - **email** `<Email>` - контактный e-mail
      - **offer** `<Boolean>` - маркер того принял ли лицензиар оферту или нет
      - offerAcceptedUid `<Long>` - UID пользователя, принявшего оферту, если есть
      - offerAcceptedTime `<Date>` - время принятия оферты, если есть
      - documents [`<Array[Document]>`](/_entities/documents/Document.md) - список документов оферты, обязателен для лицензиара, принявшего оферту
      - сontract `<String>` - идентификатор контракта лицензиара
      - site `<String>` - ссылка на официальный сайт лицензиара 
      - franchisings [`<Array[Franchising]>`](/_entities/Franchising.md) - франшизы лицензиара, переданные списком
      - сomment `<String>` - комментарий
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## PUT /licensors/[vendorId]

Редактирование информации о лицензиаре

### Примечания
  - Редактирование карточки доступно менеджеру, суппорту и админу лицензиара
  - Ручка доступна суппорту только если у карточки лицензиара не назначен менеджер

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
 - [см POST /licensors](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors#Данные)

### Ответ
 - [см GET /licensors/[licensorId]](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/licensors/%5BlicensorId%5D#Ответ)

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого лицензиара](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
 - Ошибка с нарушением уникальности тайтла будет обработана здесь с кодом `ALREADY_EXISTS`
 - Сочетание имени компании лицензиара и имени франшизы уже существует
 - Оферта не принята, вызов лицензиаром запрещен
#### [Ошибки работы с документами](/_rules/documents/DocumentErrors.md)
#### Попытка суппортом редактирования карточки с назначенным менеджером
  - statusCode: `403`
  - code: `UNAUTHORIZED`
  - message: Support is not allowed to modify licensor with linked manager 
 
##### Примечания
  - [Правила работы с документами](/_rules/documents/DocumentRules.md#postинг)
  - [Правила работы с документами в "оферте"](/_rules/documents/OfferDocumentRules.md)


# Ресурс /vendors/[vendorId]/modelbids

## POST /vendors/[vendorId]/modelbids

Добавление услуги "Управление ставками на модели" вендору по его vendorId 

### Примечание
  - Для вендора, принявшего оферту, автоматически подбирается или создается клиент в балансе, а пользователь, принявший оферту, автоматически к нему привязывается. 
  - Для вендора, не принявшего оферту, возможен только контрактный (неофертный) тип услуги с заранее существующим клиентом в балансе, контракт обязателен.
  - Ответ соответствует ответу ручки [GET /vendors/[vendorId]/modelbids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/recommended#get-vendorsvendoridmodelbids#Ответ)

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Данные
  - clientId `<Integer>` - клиентский id (для баланса), обязателен для контрактной услуги
  - contractId `<Integer>` - идентификатор контракта в балансе (для списания кредитных средств), обязателен для контрактной услуги
  - contractType [`<ContractType>`](/_entities/ContractType.md) - тип контракта, при предоплатном типе становится доступен перевод средств между услугами
  - offer `<Boolean>` - маркер того является ли продукт офертным, для офертного вендора может быть любым, для неофертного вендора - только false
    
### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **vendorId** `<Integer>` - идентификатор карточки вендора
      - contractId `<Integer>` - идентификатор контракта в балансе (для списания кредитных средств), отсутствует или 0 для предоплаты/оферты
      - **contractType** [`<ContractType>`](/_entities/ContractType.md) - тип контракта
      - **offer** `<Boolean>` - маркер того является ли продукт офертным
      - **orderId** `<Integer>` - идентификатор заказа в балансе
      - **clientId** `<Integer>` - клиентский id (для баланса)
      - **clientName** `<String>` - имя клиента в балансе
      - **logins** `<Array[Object]>`  - получаются автоматически из баланса по `clientId`
        - **login** `<String>`
      - **balance** `<Integer>` - баланс в центах
      - **expenses** `<Integer>` - расходы в центах
      - **placement** `ACTIVE|SUSPENDED` - текущее состояние размещения кампании
      - activeCutoffTypes [`Array[String]`](/_entities/CutoffType.md) - типы открытых на данный момент катоффов
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Офертная услуга невозможна для неофертного вендора](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Отсутствует clientId для контрактной услуги](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Отсутствует contractId для контрактной услуги](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


## GET /vendors/[vendorId]/modelbids

Получение информации об услуге "Управление ставками на модели" вендора по его vendorId

### Параметры
  - **uid** `<UID>` - обязательный параметр для аутентификации

### Ответ
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **vendorId** `<Integer>` - идентификатор вендора
      - contractId `<Integer>` - идентификатор контракта в балансе (для списания кредитных средств), отсутствует или 0 для предоплаты/оферты
      - **contractType** [`<ContractType>`](/_entities/ContractType.md) - тип контракта
      - **offer** `<Boolean>` - маркер того является ли продукт офертным
      - **orderId** `<Integer>` - идентификатор заказа в балансе
      - **clientId** `<Integer>` - клиентский id (для баланса)
      - **clientName** `<String>` - имя клиента в балансе
      - **logins** `<Array[Object]>` - получаются автоматически из баланса по `clientId`
        - **login** `<String>`
      - **balance** `<Integer>` - баланс в центах
      - **expenses** `<Integer>` - расходы в центах
      - **placement** `ACTIVE|SUSPENDED` - текущее состояние размещения кампании
      - activeCutoffTypes [`Array[String]`](/_entities/CutoffType.md) - типы открытых на данный момент катоффов.
  - errors `<Error[]>`

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)

## PUT /vendors/[vendorId]/modelbids

Редактирование "Управление ставками на модели" вендора по его vendorId

### Примечание
  - Для вендора, принявшего оферту, при пустом (нулевом) клиенте автоматически подбирается или создается новый клиент в балансе, а пользователь, принявший оферту, автоматически к нему привязывается.
  - Для вендора, принявшего оферту, возможен переход услуги на контракт через явную передачу флага offer=false, также для этого заполняется контракт и если надо клиент (или меняются, если уже заполнены). Для возвращения на оферту передается offer=true, контракт и клиент если надо тоже зачищаются.
  - Для вендора, не принявшего оферту, возможен только контракный вид услуги с заранее существующим клиентом в балансе, поэтому контракт и клиент обязательны. Для него можно запросить переход на предоплату через явное выставление предоплатного типа контракта и обратно, для открытия перевода средств.
  - Для вендоров возможна смена владельца (клиента) и контракта.

### Параметры
  - **uid** `<UID>`

### Данные
  - clientId `<Integer>` - клиентский id (для баланса), обязателен для контрактной услуги
  - contractId `<Integer>` - идентификатор контракта в балансе (для списания кредитных средств), обязателен для контрактной услуги
  - contractType [`<ContractType>`](/_entities/ContractType.md) - тип контракта, при предоплатном типе становится доступен перевод средств между услугами
  - offer `<Boolean>` - маркер того является ли продукт офертным, для офертного вендора может быть любым, для неофертного вендора - только false

### Ответ
  - [см GET /vendors/[vendorId]/modelbids](https://github.yandex-team.ru/market/vendors-api-spec/tree/master/vendors/%5BvendorId%5D/modelbids#get-vendorsvendoridmodelbids#Ответ)

### Ошибки
#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Неверные параметры вызова](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Офертная услуга невозможна для неофертного вендора](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Отсутствует clientId для контрактной услуги](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)
#### [Отсутствует contractId для контрактной услуги](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)


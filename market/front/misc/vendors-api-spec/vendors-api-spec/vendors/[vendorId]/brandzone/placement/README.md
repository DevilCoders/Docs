## PUT /vendors/[vendorId]/brandzone/placement

Изменение размещения (включение/выключение) услуги "Бренд-зона на Сервисе Яндекс.Маркет" для указанного вендора

Логика будет возвращена в https://st.yandex-team.ru/VNDMARKET-2103
Временно работает так: 
  - если передан placement=ACTIVE, снимается один из катоффов услуги. Если вызывает менеджер, то сначала снимается админский катофф (при наличии), а в следующий вызов - клиентский.
  - если передан placement=SUSPENDED, устанавливается катофф в соответствии с ролью.

### Параметры
  - **uid** `<UID>`

### Данные
  - **placement**: `ACTIVE|SUSPENDED`

### Ответ:
  - **meta** `<Object>`
  - result `<Object>`
    - **item** `<Object>`
      - **placement** `ACTIVE|SUSPENDED|REJECTED` - текущий статус публикации бренд-зоны (ACTIVE - опубликована, SUSPENDED - распубликована, REJECTED - публикация приостановлена по другим причинам)
      - **activeCutoffTypes** [`<Array[CutoffType]>`](/_entities/CutoffType.md) - список активных типов отключений, висящих на кампании **после** попытки смены статуса публикации.
  - errors `<Error[]>`

### Примечания
  - Если был послан запрос на распубликование (`SUSPENDED`), то ответ будет 
  содержать в поле `activeCutoffTypes` (среди прочего!) ново-созданное отключение.

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение status](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

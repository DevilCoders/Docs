## PUT /vendors/[vendorID]/modelbids/placement

~~Изменение размещения (включение/выключение) услуги "Управление ставками на модели" для указанного вендора~~

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
      - **placement** `ACTIVE|SUSPENDED|REVOKE|REJECTED` - текущий статус размещения (ACTIVE - размещается, SUSPENDED - не размещается, REVOKE - не достаточно средств для размещения, REJECTED - размещение приостановлено менеджером)
  - errors `<Error[]>`

### Ошибки

#### [Стандартные](https://github.yandex-team.ru/market/vendors-api-spec#Стандартные-ошибки)
#### [Нет такого вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Нет такой услуги у вендора](https://github.yandex-team.ru/market/vendors-api-spec#Несуществующий-объект-данных)
#### [Некорректное значение status](https://github.yandex-team.ru/market/vendors-api-spec#Неверные-параметры-вызова)

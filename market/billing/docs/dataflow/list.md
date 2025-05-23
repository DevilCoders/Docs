# Потоки данных в окрестности Биллинга Маркета

## Обмены данными

### Чекаутер -- Биллинг, LB

- **Источник:** Чекаутер
- **Приемник:** Биллинг Маркета
- **Протокол:** Logbroker
- **Данные:** События по заказам
- **Подробности**
  - lbkx/market-checkout/production/checkouter-order-event-log

### Чекаутер -- Биллинг, http

- **Источник:** Чекаутер
- **Приемник:** Биллинг Маркета
- **Протокол:** http / pull
- **Данные:** Дополнительные свойства событий (?)
- **Подробности**


### Биллинг Маркета -- Баланс, YT

- **Источник:** Биллинг Маркета
- **Приемник:** Баланс
- **Протокол:** YT
- **Данные:** tlog
- **Подробности**
  - <https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mbi/billing/tlog>
  - [{#T}](../reference/tlog.md)



### Marketstat -- Биллинг, LB

- **Источник:** Marketstat
- **Приемник:** Биллинг Маркета
- **Протокол:** Logbroker
- **Данные:** Клики (очищенные онлайн-антифродом)
- **Подробности**
  - <https://lb.yandex-team.ru/lbkx/accounts/marketstat/prod/market-clicks-log>


### Антифрод Маркета -- Биллинг, LB

- **Источник:** Антифрод
- **Приемник:** Биллинг Маркета
- **Протокол:** Logbroker
- **Данные:** оффлайн-антифрод (откаты кликов)
- **Подробности**
  - <https://lb.yandex-team.ru/lbkx/accounts/marketstat/prod/market-clicks-rollbacks-log>


### Антифрод Маркета -- Биллинг, YT

- **Источник:** Антифрод
- **Приемник:** Биллинг Маркета
- **Протокол:** Logbroker
- **Данные:** оффлайн-антифрод (откаты кликов)
- **Подробности**
  - <https://lb.yandex-team.ru/lbkx/accounts/marketstat/prod/market-clicks-rollbacks-log>


### LOM -- Биллинг, YT

- **Источник:** LOM
- **Приемник:** Биллинг
- **Протокол:** YT
- **Данные:** ???
- **Подробности** ???


### LOM -- Биллинг, LB

- **Источник:** LOM
- **Приемник:** Биллинг
- **Протокол:** Logbroker
- **Данные:** ???
- **Подробности** ???


### Биллинг Маркета -- Баланс, http push

- **Источник:**
- **Приемник:**
- **Протокол:**
- **Данные:**
  - результаты Белого биллинга
- **Подробности** xmlrpc



### ПИ -- Биллинг Маркета, общая БД

- **Источник:** ПИ
- **Приемник:** Биллинг Маркета
- **Протокол:** общая таблица в Oracle
- **Данные:** заявки на асинхронные отчеты
- **Подробности**
  - у отчетов в целом немного туманная принадлежность


### ПИ -- Биллинг Маркета, http-push

- **Источник:** ПИ
- **Приемник:** Биллинг Маркета
- **Протокол:** http-push
- **Данные:** расписание выплат (мерч устанавливает в ЛК)
- **Подробности**
  - TODO ссылка на ручку API


### Биллинг Маркета -- Баланс, YQL в Бункере

- **Источник:** Биллинг Маркета
- **Приемник:** Баланс
- **Протокол:** YQL в Бункере
- **Данные:** премии агенствам???
- **Подробности**


### Биллинг Маркета -- OEBS, http

- **Источник:** Биллинг Маркета
- **Приемник:** OEBS
- **Протокол:** http / push
- **Данные:** отчет по реалазации товара для комплекта закрывающих документов
- **Подробности**


### Биллинг Маркета -- OEBS, YT

- **Источник:** Биллинг Маркета
- **Приемник:** OEBS
- **Протокол:** YT
- **Данные:** признак "такой-то мерч работает по факторингу на такую-то дату"
- **Подробности**
  - TODO: путь к таблице


### OEBS -- Биллинг Маркета, LB

- **Источник:** Биллинг Маркета
- **Приемник:** OEBS
- **Протокол:** LB
- **Данные:**
  - платежные поручения TODO уточнить у Андрея Колчанова, что ПП через LB
  - инфа о Мерчах TODO подробности, что за инфа
- **Подробности**
  - TODO: путь к топикам


### Биллинг Маркета -- ПИ, MDS (отчет о движении товаров)

- **Источник:** Биллинг Маркета
- **Приемник:** ПИ
- **Протокол:** MDS
- **Данные:** отчет о реализации товаров
- **Подробности** TODO путь в MDS


### Биллинг Маркета -- Балалайка (банки), http-push

- **Источник:** Биллинг Маркета
- **Приемник:** Балалайка (прокси к банкам)
- **Протокол:** http-push
- **Данные:** список мерчей (на проверку)
- **Подробности**
  - `[{#T}](../reference/jobs/list/sendClientsToFactoringBankExecutor.md)` (TODO разобраться, почему не резолвится ссылка)
  - [{#T}](../reference/architecture/payment-control/payment-control-ext.md)


### Балалайка (банки) -- Биллинг Маркета, http-pull

- **Источник:** Балалайка (прокси к банкам)
- **Приемник:** Биллинг Маркета
- **Протокол:** http-pull
- **Данные:** черный список мерчей
- **Подробности**
  - TODO уточнить, что это правда http-pull; ссылка на джобы
  - [{#T}](../reference/architecture/payment-control/payment-control-ext.md)



## Непонятности

- Тарифница: ???
- Биллинг логистики: ???
- Группа по работе с агентствами -- Биллинг, админка???
- Биллинг -- ПИ, ClH ???

Контракты данных
<https://wiki.yandex-team.ru/market/strategy-and-finance/businessintelligence/staraja-struktura/1.-istochniki-dannyx/kontrakty-s-istochnikami-dannyx/>


## Служебное

### Шаблон описания { #template }

- **Источник:**
- **Приемник:**
- **Протокол:**
- **Данные:**
- **Подробности** (пути к таблицам, топики LB, тикеты, описания http-ручек и т.д.)


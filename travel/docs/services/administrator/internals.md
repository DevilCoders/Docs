---
title: Внутреннее устройство
rank: 20
---

### Флоу основных сущностей

Центральной сущностью является `HotelConnection` со следующим флоу при подключении:

```
New -----> Publishing ---------> Published
 |             ^                   |
 |             |                   V
 ---> Manual_Verification ----> Unpublished
```  
  
У сущности `LegalDetails` флоу следующий:
```
New -----> Registering -------> Registered
               |                     |
               |                     V
               |--------------> Deactivated
```

Флоу `HotelConnectionUpdate`:
```
New -----> Processing -------> Applied
|                     
|                     
|--------------> Rejected
```

### Основные шаги при подключении Отеля
1. Вызвать ГеоПоиск для получения пермалинка и названия отеля
2. Проверить, что отель находится в таблице `Matched`, которая поставляется Контент Платформой
3. Зарегистрировать юр. данные (отдельный флоу `LegalDetails`)

Шаги 2 и 3 выполняются параллельно.  

Шаги при регистрации юр. данных:
1. Создать клиента в Балансе (`client`)
2. Создать плательщика в Балансе (`person`)
3. Создать договор в Балансе (`contract`)

### Интеграция с другими сервисами

1. XML-RPC Баланса — необходимо для регистрации юр. лица, создания контракта и проверки активности контракта
2. Партнеры
    1. Travelline
    2. Bnovo
3. YT таблица для создания реквестов на проверку кластеризации [//home/travel/prod_inbox/content_manager/cl_new_permalinks](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod_inbox/content_manager/cl_new_permalinks)
4. ГеоПоиск — необходим для первоначального получения имени отеля и его пермалинка
5. Стартрек — Администратор тесно завязан на тикеты в Стартреке - создает их, отслеживает их статус, меняет его, линкует тикеты и оставляет комментарии
6. YT таблица уже кластеризованных отелей [//home/travel/prod/content_manager/export/matched_hotels](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/content_manager/export/matched_hotels)
7. Унификатор адресов — используется при получении адресов от партнеров для унификации (унифицируем только если унификатор смог это сделать)
8. АПИ Спарка — используется для получения ОГРН организации

### GRPC API

Администратор имеет 2 основных GRPC-интерфейса:
* [AdministratorService](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/hotels_administrator/src/main/java/ru/yandex/travel/hotels/administrator/AdministratorService.java) - используется преимущественно External API, которое в свою очередь доступно партнерам
* [AdministratorAdminService](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/hotels_administrator/src/main/java/ru/yandex/travel/hotels/administrator/AdministratorAdminService.java) - содержит эндпоинты для ручных действий, которые вызываются дежурными из Administrator CLI

### Используемые таск процессоры

1. **TicketAwaitingResolution**  
   Проверяет, не закрыт ли тикет, принадлежащий `ConnectionStep`, находящийся в статусе `CSS_WAIT_FOR_TICKET_RESOLUTION`. 
   В этом случае отправляется событие `TTicketClosed`. 
   Типичный пример: шаг CallGeoSearchStep
   Отель не найден в ГП, дежурный закрывает тикет, посылается `TTicketClosed`, если отель найден в ГП, то шаг считается выполненным, если нет - тикет переоткрывается.  
   

2. **Clusterization**  
   Если в момент подключения кластеризация отеля не была проверена, то отель "подвисает" на стадии проверки кластеризации и таск процессор периодически проверяет, не появился ли отель в списках проверенных


3. **PermalinkUpdate**  
   Периодически обновляет пермалинки отелей, используя таблицу Контент Платформы
   

4. **BillingContractFlagsSynchronizer**  
   Синхронизирует флаги активности контракта из Баланса
   

5. **HotelPublisher**  
   Публикует таблицы в YT, для использования другими сервисами:
    * Белый список отелей, которые можно продавать (используется Серчером и Офферкешом) [//home/travel/prod/hotels_administrator/whitelisted_hotels](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/hotels_administrator/whitelisted_hotels)
    * Комиссионные схемы отелей вместе с их юр. данными (используется Оркестратором) [//home/travel/prod/hotels_administrator/hotel_agreements](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/hotels_administrator/hotel_agreements)
    * Юридическая информация об отеле, в том числе и ОГРН (используется АПИ) [//home/travel/prod/hotels_administrator/hotels_legal_info](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/hotels_administrator/hotels_legal_info)
    * Информация обо всех заключенных договорах - бумажных и офертных (используется Оркестратором) [//home/travel/prod/hotels_administrator/contracts_info](https://yt.yandex-team.ru/hahn/navigation?path=//home/travel/prod/hotels_administrator/contracts_info)
    

### Работа с отелями на бумажных договорах

При работе с бумажными договорами мы исходим из следующих предположений:
1. Бумажные договоры заводятся вручную в Балансе
2. `LegalDetails` в Администраторе создаются на основе этих договоров с помощью [CLI](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/hotels_administrator/tools/administrator_cli), метод `createLegalDetails`  
3. Администратор не делает никаких обновлений в "бумажных" договорах — если нужно сделать какие-то изменения, то их нужно делать напрямую в балансе, после чего вызывать метод `updateLegalDetails` в CLI
4. Запросы на смену "бумажных" реквизитов не могут быть обработаны автоматически. Особенности обработки бумажных договоров можно найти в [HotelConnectionService](https://a.yandex-team.ru/arc/trunk/arcadia/travel/hotels/hotels_administrator/src/main/java/ru/yandex/travel/hotels/administrator/service/HotelConnectionService.java)

# Развешиватель тикетов в стартреке.

Развешиватель преназначен для автоматического произведения каких-либо операций над тикетами стартрека

## Как добавить новую задачу?
1. Создать стартрек [фильтр](https://st.yandex-team.ru/issues)
    - Не использовать сырые запросы
    - Стараться уложить максимальное колличетво логики в фильтр, используя [язык запросов](https://doc.yandex-team.ru/tracker/external/user/query-filter.html)
2. Убедиться, что [Ticket](src/main/java/ru/yandex/market/supportwizard/base/Ticket.java) содержит все нужные поля для вашей задачи
    - В случае отсутствия заэкстендить новое поле от [AbstractField](src/main/java/ru/yandex/market/supportwizard/base/fields/AbstractField.java)
    - Добавить новое поле, сетер и гетер в [Ticket](src/main/java/ru/yandex/market/supportwizard/base/Ticket.java)
    - Добавить новое поле в билдер в [Ticket](src/main/java/ru/yandex/market/supportwizard/base/Ticket.java)
    - Добавить новое поле в функцию `getFieldUpdates` класса [Ticket](src/main/java/ru/yandex/market/supportwizard/base/Ticket.java)
    - Если ваше поле является кастомным и не поддерживается Startrek API, то добавить его как кастомное поле в [StartrekService](src/main/java/ru/yandex/market/supportwizard/service/StartrekService.java)
3. Создать новую `public static Ticket` функцию в [Ticket](src/main/java/ru/yandex/market/supportwizard/base/Ticket.java), которая будет создавать тикет для вашей задачи
4. В пакете [tasks](src/main/java/ru/yandex/market/supportwizard/service/tasks) создать класс для вашей задачи и заэкстендить его от [StartrekTicketManager](src/main/java/ru/yandex/market/supportwizard/service/tasks/StartrekTicketManager.java)
5. В [ScheduleConfig](src/main/java/ru/yandex/market/supportwizard/config/ScheduleConfig.java) создать новое расписание для вашей задачи
6. Написать тесты
7. Добавить описание новой задачи ниже

## Задачи развешивателя

#### Развешивание тикета
Автоматически проставляет вес тикету в соответствии с важностью связанных с тикетом партнеров.

Каждые 10 минут развешивает тикеты, полученные через [фильтр](https://st.yandex-team.ru/filters/filter:48826).

Сейчас фильтр настроен на работу с очередями 

- MBI 
- MARKETPARTNER
- PLSUPPORT
- MARKETINDEXER
- CHIPNDALE 

ID партнеров берутся из тикета, из полей partnerIDs и campaignIDs, находящихся в категории MBI.
Для магазинов метрикой важности является их cpcBudget, который берется из [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/analyst_shops_dict/latest).
Для поставщиков метрика важности - траты за последний месяц, также из таблички в [YT](https://yt.yandex-team.ru/hahn/navigation?path=//home/market/production/mstat/dictionaries/order_billed_amounts/latest).
Суммарная важность парнеров проставляется в поле "Оценка Важности" в категории MBI.

Тикеты также можно развесить [вручную](https://support-wizard.vs.market.yandex.net).


#### История тикета
Автоматически добавляет для тикетов из очередей MBI и PLSUPPORT коментарий с тикетами, которые раньше затрагивали партнеров или компаний, указанных в полях partnerIDs и campaignIDs\
Работает раз в 15 минут\
Добавляет тег `support_history` для уже развешаных тикетов\
Использует [фильтр](https://st.yandex-team.ru/issues/51947) стартрека

#### Локальный деплой приложения
1. Запускаем локально БД сервиса:
```
$ mkdir -p $HOME/docker/volumes/postgres/support_wizard
$ docker run --rm --name pg-support-wizard-docker -e POSTGRES_PASSWORD=support_wizard -e POSTGRES_USER=support_wizard -d -p 5432:5432 -v $HOME/docker/volumes/postgres/support_wizard:/var/lib/postgresql/data/ postgres
```
2. В настройках запуска идеи установить переменную окружения PROPERTIES_DIR  как путь до папки properties.d
3. Настроить TVM по [инструкции](https://wiki.yandex-team.ru/users/serg-turbo/tvm-library-for-mac/)
4. В настройках запуска идеи добавить VM option к запуску
```
-Djava.library.path=/Library/Java/Extensions
-Dspring.profiles.active=local
```


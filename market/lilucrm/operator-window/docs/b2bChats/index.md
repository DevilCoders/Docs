# B2b chats tickets

На текущий момент в системе есть два типа b2b чат тикетов

Для белых магазинов [**b2bShopChat.xml**](https://a.yandex-team.ru/arc_vcs/market/lilucrm/b2bcrm/module_ticket/src/main/resources/b2bcrm/module/ticket/metadata/b2bShopChat.xml?rev=56cf2a1bc65962dbdb8e5cb88507448f4673b24a#L15)
и для поставщиков [**b2bSupplierChat.xml**](https://a.yandex-team.ru/arc_vcs/market/lilucrm/b2bcrm/module_ticket/src/main/resources/b2bcrm/module/ticket/metadata/b2bSupplierChat.xml?rev=56cf2a1bc65962dbdb8e5cb88507448f4673b24a#L14)

## Создание b2b тикетов

Входной точкой системы для создания тикетов служит метод [receiveMessage](https://a.yandex-team.ru/arc_vcs/market/lilucrm/jmf/module_chat/src/main/java/ru/yandex/market/jmf/module/chat/controller/ChatController.java?rev=83caf4400f784cb72729190aaf37fd5f60e982d1#L95) в контроллере 'ChatController'
Внутри контроллера вызывается метод receiveMessage [сервиса](https://a.yandex-team.ru/arc_vcs/market/lilucrm/jmf/module_chat/src/main/java/ru/yandex/market/jmf/module/chat/impl/TransactionalChatsService.java?rev=03a3d112f7aee4ec59209dd2c78bc3e19e5aee00#L60)
После получения сообщений мы сохраняем их в таблицу tbl_chatmessage, по таблице всегда можно узнать приходили
ли вообще сообщения из виджетов,
чтобы понять по какой причине не создались тикеты.
В некотрых ситуациях сообщения приходят с задержкой, таблица поможет нам это увидеть.

Триггер который реагирует на получение таких сообщений вызывает следующий скрипт
скрипт [createTicketOrCommentsOnChatMessage.groovy](https://a.yandex-team.ru/arc_vcs/market/lilucrm/operator-window/src/main/resources/scripts/createTicketOrCommentsOnChatMessage.groovy?rev=5a01858ab82aed34afc12ebd70faac05abce22d7#L73) отвечает за роутинг

Там просходит создание нового тикета при сообщении из чата либо добавление комментариев к существующим тикетам.


## Подробнее о том как работет созадание тикетов


В первую очередь мы проверяем какой тип сообщения приходит. Существуют системные и прочие сообщения.
Мы обрабатывем тот текст который пишет пользовтель.
Системные сообщения обрабатывются по другому в текущем скрипте они пропускаются.

На каждое новое сообщение создается либо тикет либо оно добавляется к старому тикету.
Сначала мы ищем есть ли у нас не архивные тикеты от пользователя, поиск происходит по conversationId.
Так как мы ищем не архивные тикеты это значит что возможен кейс, когда старый тикет закрыт, пользователь 
написал снова и мы заводим уже новый тикет.

Далее, когда мы уже знем есть ли в системе заведенное обращение от пользователя, происходит следующая проверка.
Если сообщение пришло от b2b клиентов
Мы проверяем в рабочие ли часы нам пишут, если нет то в случае открытого тикета, мы добавим к нему комментарий,
в противном случае отправим сообщегние с просьбой написать в рабочее время.


Так как скрипт обрабатывает сообщения не только из b2b чатов, чтобы понять откуда оно пришло мы смотрим на код
очереди, для b2b тикетов зведены очереди со следующими кодами
_b2bShopChat_, _b2bSupplierChat_.  B2b сообщения могут придти из очереди с кодом _courierPlatformChat_

Чтобы сообщения падали на свои очереди, необходимо произвести настройку соответсвия. О ней написано ниже
в "Настройка соответсвия чатов с очередями"

Далее многое будет зависит от кода очереди.
Так как для разных чатов работает разная логика.

Если мы получили сообщение из b2b чатов то они будут обрабатыватся логикой описаной в скрипте
[createB2bTicketOrComments.groovy](https://a.yandex-team.ru/arc_vcs/market/lilucrm/operator-window/src/main/resources/scripts/modules/createB2bTicketOrComments.groovy?rev=7b09f8f64fbd0faa5fad180ba4bba28bded15cb2#L145)


В этом скрипте мы проверяем что нам пишут в рабочее время. Рабочее время берет из настроек самой очереди,
оно хранится в атрибуте serviceTime.
В не рабочее время мы отправляем пользователю отбивку с просьбой написать в рабочие часы. 


Далее идет проверка на то не загружены ли очереди. Проверка работает следующим образом, мы смотрим сколько
у нас обращений в статусе открыт/переоткрыт если их больше чем 
указано в конфигурации (maxUndistributedTicketNumber по дефолту - 1) то считается что операторы перегружены.
В данном случае мы делаем следующую отбивку 

_Мы отвечаем медленнее, чем обычно. Хотите, чтобы вам ответили быстрее?_

и два варианта ответа

_'Да', 'Нет, я подожду'_

Если пользвоатель готов подождать мы заводим тикет, и он поступит в работу по мере освобождения операторов.
Если пользователь желает получить ответ раньше
мы потправляем ему ссылки на ФОС где он может оставить заявку, и заводим тикет но уже в статусе missing.
Данный статус нужен для получения статистики по потерянным обращениям

и создаем тикет в статусе missing. Данный тикет нужен для получения статистики по потреянным обращениям.
Если пользователь предпочитает получить ответ 

Если очередь не перегружена то создание чата будет происходить по другому алгоритму

В первую очередь проверяется есть ли уже в системе тикет связанные с чатом из которого поступают сообщения.
Тикеты ищутся по атрибуту chatConversation, архивные тикеты игнорируются

Если предыдущее обращение найдено и оно не архивно то к нему просто добавляется новое сообщение.

Если обращение найдено не было, то создается новый тикет. 

Первоначальный список атрибутов получаем в скрипте creationChatUtil
в методе getMainAttributesForCreationChatTicket() 
Есть список дефолтных полей, таких как различные таймеры, например 

        waitForOperatorTime: 'PT5M',
        waitingResponseTime: 'PT3M',
        waitingForBotTime  : 'PT15S',
        reopenOnPendingTime: 'PT5M',
        csatResolutionTime : 'PT10M'

данные атрибуты общие в том числе и для не b2b тикетов, остальные поля динамические, зависят например
от очереди на которую падает обращение



## Настройка соответсвия чатов с очередями
Настройка между чатами и очередями настраивается в таблице
tbl_chat в колонке service, это соответсвие необходимо, так как если мы не сматчим чаты с очередями
в последсивии не правильно отработает определение типа создаваемого тикета


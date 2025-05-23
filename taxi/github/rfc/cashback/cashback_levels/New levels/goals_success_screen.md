## Продуктовое описание
Делаем новые персональные цели для всего Яндекса.  
У нас есть сервис, который собирает события со всех сервисов и умеет считать на основе этих событий исполнение некоторых заданий ([mission-control](https://wiki.yandex-team.ru/plus/mc/)).   
Другой сервис позволяет такие задания создавать и по их достижению выдавать награду ([cashback-levels](https://wiki.yandex-team.ru/taxi/backend/client-product/teams/plus-base/projects/plus-levels/)).  
Все задания, которые навешаны на юзера, он видит в Домике Плюса.
Нужно уметь по выполнению задания оповестить юзера об этом с помощью красивого окошка. Окошко будет рисовать вебвью Домика Плюса.
Нам нужно Домик в нужный момент оповестить, чтобы тот показал это красивое окошко.

### Дизайн
[тут](https://www.figma.com/file/U2oPV9QKSZuPZPMezhgTlW/%F0%9F%8E%AF%D0%9F%D0%B5%D1%80%D1%81%D1%86%D0%B5%D0%BB%D0%B8?node-id=1%3A524)

### Требования
1. Показывать нотификации нужно только о заданиях этого сервиса. В Такси - о заданиях Такси, итд
2. В приложении нужно показывать некое уведомление об исполнениии цели, но не пуш, а что-то более качественное: пункт в меню, в Такси - шторку, в других приложениях - что-то свое.
3. По тапу на это уведомление должен открываться вебный домик Плюса с поздравлятельным экраном. В качестве поздравлятельного экрана предлагается использовать карточку с деталями цели, но рисовать в ней другое наполнение (по крайней мере на этапе первого экспа будем использовать истории в домике, которые они умеют открывать по диплинку).

## Как делаем
Способ реализации должно быть можно легко повторить во всех приложениях сервисов, то есть нужна SDK. Выбираем SDK Плюса и делаем в ней.
Логику предлагаю повторить как в [старых персоналках](https://github.yandex-team.ru/taxi/rfc/blob/master/personal-goals/main.md).

### Схема архитектуры
Верхнеуровневая схема взаимодействия клиента - бэка домика - бэка уровней. Скрин из [миро](https://miro.com/app/board/o9J_lipWeBY=/):
<img src="https://jing.yandex-team.ru/files/paradise/photo_2021-11-18%2016.51.18.jpeg">

Еще одна схема [тут](https://miro.com/app/board/o9J_ljMqEek=/)

### 1.1. Запрос клиентом нотификаций: запуск приложения
Так как на момент завершения заказа и, соответственно, исполнения цели приложение может быть скрыто, нужно спрашивать нотификации на старте.

В Такси сейчас встроена наша версия SDK, которая ходит в [ручку sdk-state](https://pages.github.yandex-team.ru/taxi/schemas/Taxi_Documentation/Uservices/plus-sweet-home/api/sdk-state/#40sweet-homev2sdk-state) сервиса plus-sweet-home. В остальные приложения вроде Маркета и Еды встроена новая версия SDK, которая ходить в граф. Но она тоже на старте приложения ходит в ту же sdk-state за балансом. Поэтому сейчас мы расширяем ответ sdk-state информацией о нотификациях, наши клиенты получат нотификации напрямую, а в клиентской части нового SDK нужно будет пробросить нотификации через граф в клиентскую часть.

В ручке есть хидер X-SDK-Client-ID, по нему можно понять, Домик из какого приложения пришел в ручку и использовать это для определения сервиса.

И когда новая SDK откажется от sdk-state в пользу своей новой ручки, нужно будет эту же логику повторить в ней.

Дальше plus-sweet-home пойдет в cashback-levels и добавит его ответ без всякого обогащения.

Пример раздела про нотификации
```json5
{
  "missions": {
    "notifications": [{
      "id": "unique notification id",
      "mission_id": "taxi_first_order",
      
      "title": AttributedText ("Поздравляем! 200 баллов ваши"),
      "description": AttributedText ("Вы сделали первый заказ! Баллы вы можете потратить во всех сервисах Яндекса"),
      
      "status": "new" | "in-progress" | "done",
      "progress": {
        "total": 1,
        "current": 1
      },
      // диплинк на историю в домике из нашего конфига уведомлений
      "deeplink": "yandextaxi://home/levels/notifications/hex_notification_id"
    }]
  }
}
```

### 1.2. Запрос клиентом нотификаций: завершение заказа
По завершению заказа хостовое приложение просит SDK перевызвать sdk-state, чтобы получить новые нотификации (в параметре запроса include можно передавать ["missions"], чтобы возвращалось только поле ответа с уведомлениями). И перевызвать граф для получения начинки вебного домика, если он открыт или лежал какой-то закешированный ответ.  

Не будем придумывать новую ручку только для этого, просто постараемся обновить состояние Домика. Потому что нам нужно помимо нотификации о выполненны целях будет получить и обновленное состояние этой выполненной цели. Чтобы карточка задания, которая будет в роли поздравительного экрана, могла понять, что задание выполнено и нужно рисовать поздравительный экран.

Тут есть такой момент, что после завершения заказа до момент исполнения цели может пройти секунд 5 точно,
поэтому на запрос /sdk-state сразу после завершения заказа уведомления могут и не прийти, это решаем так:  
Если в ответе ручки /sdk-state по завершении заказа в typed_experiments вернулся эксп с делеем (в секундах), то клиент перезапросит /sdk-state через заданное время.  
Значение этого экспа будет задаваться на бэке уровней и браться из эксперимента.  
Если в ручке уведомлений на бэке уровней мы видим, что у пользователя есть задания в процессе выполнения, возвращаем клиентский эксп с делеем.  

Кажется, что проще всего было бы на клиенте перезапрашивать эту ручку только в ретрайном запросе по окончании заказа, а нам на беке возвращать эксп всегда, если он матчится.

### 2. plus-sweet-home идет в cashback-levels за нотификациями
Пример запроса
```json5
{
  "yandex_uid": "1234567",
  "services": ["taxi", "eda"] // В Го возможно придется показывать нотификации по всем сервисам, поэтому массив
}
```
Тот же пример ответа
```json5
{
  "missions": {
    "notifications": [{
      "id": "unique notification id",
      "mission_id": "taxi_first_order",
      
      "title": AttributedText ("Поздравляем! 200 баллов ваши"),
      "description": AttributedText ("Вы сделали первый заказ! Баллы вы можете потратить во всех сервисах Яндекса"),
      
      "status": "new" | "in-progress" | "done",
      "progress": {
        "total": 1,
        "current": 1
      },
      // диплинк на историю в домике из нашего конфига уведомлений
      "deeplink": "yandextaxi://home/levels/notifications/hex_notification_id"
    }]
  }
}
```

По достижении цели мы добавляем запись в табличку нотификаций user_missions_notifications. Сразу по достижении, фактического исполнения начисления баллов можно не ждать. Нужно предусмотреть нотификации и для транзакционных заданий тоже.
А ручка будет идти в эту табличку и искать в ней нотификации по этому юзеру и по нужным сервисам.

Почему не missions_completed: потому что или для транзакционных оповещения не нужны, а если нужны - то становится возможна гонка, что мы покажем только успех на 3, а слодующий успех на 5 не покажем. А еще нам эта табличка пригодится для отправки нотификаций в логброкер.

Примерная схема таблицы
```json5
{
  "id": "mission_notification_1",
  "created": "",  
  "uid": "1234567",
  "mission_id": "taxi_first_order",
  "client_notofication_seen": "new/seen"
}
```

И отдельно про диплинк: за ним не нужно никуда ходить, мы соберем его по формату `%префикс приложения%://home/levels/missions/%id задания%`, например `yandextaxi://home/levels/missions/taxi_first_order`

### 3. Юзер увидел уведомление и клиент шлет подтверждение просмотра - вызывает /4.0/sweet-home/v1/missions/notification_seen
Делаем новую ручку для этого, тоже в plus-sweet-home. Так как нотификации мы доставляем из ручки sdk-state этого сервиса, то и оповещение о просмотре логично слать в него. И для нашей версии SDK все равно придется ходить в plus-sweet-home.
И аналогично - при отказе от sdk-state эту ручку нужно будет тоже перетащить в граф.

Думаю, можно слать подтверждение просмотра как только хостовое приложение отрисовало свои элементы уведомления. Не требовать тапа на уведомление или какого-то взаимодействия с ним.


Пример запроса:
```json5
{
  "notifications": ["<notification_id>"]
}
```

### 4. plus-sweet-home пробрасывает запрос с подверждением просмотра в cashback-levels
А cashback-levels в этой ручке помечает нотификацию как прочитанную.

## Какие вопросы остались
1. seen по нынешним персоналкам шлется по факту показа или по факту взаимодействия юзера со шторкой/пунктом в меню?
2. Ок ли, что новая PlusSDK будет ходить в plus-sweet-home для подтверждения просмотра?

## Рассмотренные альтернативы на разных этапах
1. Сделать собственную SDK для доставки уведомлений - не очень понятно, зачем. Вся история заданий сильно завязана на домик, логично в его же SDK все и сделать. Чем заставлять все сервисы втягивать новую SDK. Даже если ее встроить в виде зависимости в SDK Плюса.
2. Сайлент пуши, то есть инициатором доставки выступает бек. Идеальный вариант, но у нас нет унииверсального способа отправки пушей в любой сервис. Можно было бы через Домик попробовать организовать, но совместно с Димой Поповым пришли к выводу, что это сложное и долгое решение.
3. Установить двустороннее соединение бека с клиентом. Кажется, можно придумать вебсокет между вебвьюхой и беком, но это работает только при открытом Домике.
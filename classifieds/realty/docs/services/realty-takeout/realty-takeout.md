### Балансеры
Клиенты (яндекс пасспорт и яндекс тейкаут) ходят в nginx:
[тестинг](https://realty-takeout.test.vertis.yandex.net)
[прод](https://realty-takeout.vertis.yandex.net)

### Выгрузка пользовательских данных
Было сделано в задаче https://st.yandex-team.ru/REALTYBACK-674.

Используется [асинхронная схема получения персональных данных](https://wiki.yandex-team.ru/passport/takeout/integration/#asinxronnyjjmexanizmvygruzkidannyxszalivkojjdannyxvxranilishhetejjkauta). Яндексовый тейкаут дергает ручку ((http://realty-takeout-api.vrts-slb.test.vertis.yandex.net/swagger/#!/takeout/submitTakeoutJobRoute submit)), которая ставит в очередь задач задачу по выгрузке персональных данных [TakeoutJob](https://github.com/YandexClassifieds/realty/blob/master/realty-takeout/src/main/scala/ru/yandex/realty/takeout/model/TakeoutJob.scala). В ручке используются только tvm сервис тикеты, uid передается в get параметрах.

За выполнение задач по выгрузке отвечает [TakeoutJobWatcher](https://https://a.yandex-team.ru/arc/trunk/arcadia/classifieds/realty/realty-takeout/src/main/scala/ru/yandex/realty/takeout/watcher/TakeoutJobWatcher.scala). За отправку данных в тейкаут отвечает [PassportTakeoutClient](https://github.com/YandexClassifieds/realty/blob/master/realty-takeout/src/main/scala/ru/yandex/realty/takeout/clients/PassportTakeoutClient.scala). TakeoutJob содержит в себе proto модель со списком выполненных шагов по отсылке персональных данных в тейкаут. Когда все данные успешно выгружены в хранилище тейкаута, NotifyPassportStage уведомляет тейкаут об этом и задача переходит в завершенные.

### Категории выгружаемых пользовательских данных
* информация о возовских офферах (не фидовые)
* информация о пользователе из воза

### Добавление новых категорий для выгрузки персональных данных
Чтобы добавить какую-то новую категорию персональных данных надо:
* добавить ее в proto enum JobStages
* реализовать TakeoutJobStage для этой категории


### Удаление пользовательских данных
Было сделано в задаче https://st.yandex-team.ru/REALTYBACK-5087.

Обе ручки принимают [tvm сервис и юзер тикеты](https://wiki.yandex-team.ru/passport/tvm2/theory).

Яндексовый тейкаут ходит в ручку [status](http://realty-takeout-api.vrts-slb.test.vertis.yandex.net/swagger/#!/takeout/takeoutStatusRoute) для получения списка категорий персональных данных с их статусами (доступно к удалению, в процессе удаления или удалено).

Для удаления категорий персональных данных пользователя предназначена ручка [delete](http://realty-takeout-api.vrts-slb.test.vertis.yandex.net/swagger/#!/takeout/takeoutDeleteRoute). Ручка добавляет в очередь задач новые задачи по удалению пользовательских данных, после чего [TakeoutCategoryTaskWatcher](https://a.yandex-team.ru/arc/trunk/arcadia/classifieds/realty/realty-takeout/src/main/scala/ru/yandex/realty/takeout/watcher/TakeoutCategoryTaskWatcher.scala) асинхронно выполняет эти задачи. Очереди задач для выгрузки и удаления персональных данных различные.

### Категории удаляемых пользовательских данных
* пользовательские офферы (не фидовые)
* инфа про скрытые пользовательские офферы
* пользовательские заметки
* списки избранного
* сравнения офферов
* подписки
* заявки на ипотеку (ставим в пальме флаг removed)

### Добавление новых категорий для удаления персональных данных
Чтобы добавить какую-то новую категорию персональных данных надо:
* добавить ее в enum TakeoutCategory
* написать код, который будет отвечать за статус этой категории в TakeoutCategoryManager
* реализовать TakeoutCategoryProcessor, который будет удалять данные по этой категории



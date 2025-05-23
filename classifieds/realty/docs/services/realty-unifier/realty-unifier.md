### Предназначение сервиса

Сервис предназначен для унификации и обогащения "сырого" оффера.
### Архитектура сервиса
![alt text](img/realty-unifier.png)

### Типы сообщений посылаемых в realty-unifier через кафку
- create содержит rawOffer и посылается в рамках процесса унификации оффера в VOS
- reindex посылается в рамках процесса переиндексации (процесс, параллельный процессу унификации): vos-scheduler берет идентификаторы всех активных офферов с шарда и посылает их в кафку с использованием настраиваемого рейт лимитера

### Обработка сообщений

Обработка create:
- унифицируем и обогащаем оффер
- в случае изменений хэша или id группы оффера посылаем унифицированный оффер через кафку в realty-clusterizer
- обновляем состояние оффера в базе

Обработка reindex:
- проверяем на наличие оффера в базе: если оффера нет в базе - пропускаем сообщение, если есть - обрабатываем так же, как create

###### Топик с изменениями сущностей БД

**Проблема**

Существуют различные задачи одного сценария: в случае изменений какой-то сущности в БД нужно как-то на это отреагировать в разных микросервисах.

Например:

* Создавать задачу в АМО при добавлении фотографий
* Отправлять нотификацию при смене статуса

**Задача**

Сделать топик с изменениями сущностей.

**Решение**

1. Храним текущее состояния объектов в "кеше" в YDB
2. Читаем топик YandexDataTransfer
3. Достаем прочитанный объект по ключу из кеша
4. Если объект отличается от лежащего в кеше (и его версия больше лежащего в кеше?) то в одной транзакции:
   а) Формируем объект содержащий предыдущее значение и новое, продьюсим его в Кафку
   б) Обновялем значение в кеше на полученное из YandexDataTransfer
5. Коммитим оффсет в топике YandexDataTransfer

**Модель данных**

Модель данных, которая пишется в топик представляет собой [proto-модель](../../realty-model/src/main/proto/rent/diff_event.proto), состав полей которой совпадает с составом полей таблицы.
Первое время делаем модель не публичной (не частью schema-registry).

**Топики и доступы**

Название топика: "rent-diff-events"

Документация кафки в MDB: [https://docs.yandex-team.ru/classifieds-ops-internal/storages/kafka/mdb#nastrojki-topika-po-umolchaniyu](https://docs.yandex-team.ru/classifieds-ops-internal/storages/kafka/mdb#nastrojki-topika-po-umolchaniyu)

Логин и пароль тестинг: [https://yav.yandex-team.ru/secret/sec-01fnre87ne3afxb77grn44xpmy/explore/versions](https://yav.yandex-team.ru/secret/sec-01fnre87ne3afxb77grn44xpmy/explore/versions)

Логин и пароль прод: [https://yav.yandex-team.ru/secret/sec-01fnrexr7j19th4v7z8qr52r74/explore/versions](https://yav.yandex-team.ru/secret/sec-01fnrexr7j19th4v7z8qr52r74/explore/versions)

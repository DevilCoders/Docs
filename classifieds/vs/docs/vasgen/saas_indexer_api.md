### Индексация документов
Каждый [документ](https://github.com/YandexClassifieds/schema-registry/blob/34e059a2a441365464a2d1165f7bcd439fca9424/proto/vertis/vasgen/document.proto#L53),
[отправляемый на индексацию](https://github.com/YandexClassifieds/schema-registry/blob/ca3be55887a13ec6cb1094cb2b24c9132ceaef57/proto/vertis/vasgen/grpc/receiver.proto#L14-L18),
**должен** иметь следующие поля:
- ID документа
- Версия документа
- Характер изменения в документе: обновление или удаление
- Логическая эпоха
- Время создания данной версии с изменениями
- Время протухания документа

Дополнительно документ может обогащаться
- атрибутами
- текстовыми атрибутами
- векторами(пока только одним)

### Типы индексов для НЕ текстовых атрибутов
|                                 | Pk | Equality | Range | Storage | Factor |
|---------------------------------|----|----------|-------|---------|--------|
| Хранение                        |  + |    +     |   +   |    +    |    +   |
| Поиск по полному совпадению     |  + |    +     |   +   |    -    |    -   |
| Поиск по диапазону              |  - |    -     |   +   |    -    |    -   |
| Сортировка                      |  - |    -     |   +   |    -    |    -   |
| Подсчет статистик               |  - |    -     |   +   |    -    |    -   |
| Использование в полиноме/модели |  - |    -     |   -   |    -    |    +   |

#### @Deprecated
Index.Fulltext     
useInFulltext
alterView

### Просмотр текущей эпохи

Для просмотра текущей эпохи используется `grpc`-ручка `vertis.vasgen.grpc.Saas/CurrentEpoch`.

**Пример вызова (PRESTABLE):**
```http request
grpcurl --plaintext -d '{"domain":{"id":"general"}}' vasgen-saas-indexer-grpc.vrts-slb.test.vertis.yandex.net:80 vertis.vasgen.grpc.Saas/CurrentEpoch
```

**Пример вызова (STABLE через h2p):**
```http request
>> h2p vasgen-saas-indexer-grpc
INFO Local port: 3000
...
grpcurl --plaintext -d '{"domain":{"id":"general"}}' localhost:3000 vertis.vasgen.grpc.Saas/CurrentEpoch
```
### Удаление документов с устаревшей эпохой <a name="epoch-del"></a>

Для удаления документов с устаревшей эпохой используется `grpc`-ручка `vertis.vasgen.grpc.Saas/DeleteOldEpochs`.

**Пример вызова (PRESTABLE):**
```http request
grpcurl --plaintext -d '{"topic":"general-vasgen-indexer", "ytHost":"arnold.yt.yandex.net", "ytPath":"//tmp/makarchuk-aa/main", "epoch":"8"}' vasgen-saas-indexer-grpc.vrts-slb.test.vertis.yandex.net:80 vertis.vasgen.grpc.Saas/DeleteOldEpochs
```

**Параметры:**
* `topic` - имя кафка-топика, куда будут записаны документы, предназначенные для удаления.
* `ytHost` - имя хоста, на котором находится стейт.
* `ytPath` - путь к таблице стейта. Таблица должна содержать поля `Url` и `ProtoMessage`.
* `epoch` - номер эпохи. Все документы с этой или меньшей эпохой будут удалены.

**Возвращает:**  
Число удаленных документов.

**Примечания:**  
1. Запросы к проду нужно выполнять через [h2p](https://wiki.yandex-team.ru/vertis-admin/h2p/#commandlineinterfacecli).  
2. Рекомендуется контролировать количество документов с целевой эпохой до и поле удаления с помощью запросов к `SAAS`:
```http request
curl -H "X-Ya-Service-Ticket: TVM_TICKET" 'http://saas-searchproxy-prestable.yandex.net:17000?service=vasgen_search_lb&kps=1&ms=proto&hr=json&p=0&numdoc=1&text=i_epoch:"8"' | jq .TotalDocCount
```
3. Таблица со стейтом живет в [проде](
https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-stable/vasgen_search_lb/workspace/state/main) и в [тестинге](https://yt.yandex-team.ru/arnold/navigation?path=//home/saas/ferryman-prestable/vasgen_search_lb/workspace/state/main),
но чтобы локи на ней не мешали сохранять стейт рекомендуется её скопировать и работать с копией.
Копию лучше брать непосредственно перед запросом на удаление, когда документы с удаляемой эпохой больше не отправляются, а отправленные уже дошли до индекса.
Чтобы точно не удалить лишнего можно пофильтровать табличку со стейтом руками и оставить в ней только документы с удаляемой эпохой.
   
4. Устаревших эпох может быть несколько, понадобится несколько вызовов.

### Переиндексация всех активных документов

#### Testing <a name="reind-test"></a>
```http request
curl 'general-search-scheduler-http.vrts-slb.test.vertis.yandex.net/run?id=vasgen-reindex-task'
```
#### Prod <a name="reind-prod"></a>
Запросы к проду нужно выполнять через [h2p](https://wiki.yandex-team.ru/vertis-admin/h2p/#commandlineinterfacecli).
```http request
h2p general-search-scheduler-http '/run?id=vasgen-reindex-task'
```

### Поднять эпоху

Можно руками в зукипере:  
Testing: https://zk.test.vertis.yandex.net/editor/data?path=%2Fvasgen%2Fgeneral%2Fsaas%2Fepoch%2Fcurrent

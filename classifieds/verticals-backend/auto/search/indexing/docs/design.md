## [VS-1737](https://st.yandex-team.ru/VS-1737) Auto-index-updater

Сервис-прокси между auto2-shard и vs-receiver, который конвертирует и отправляет офферы на индексацию
в поисковую платформу

### Мотивация

Хотим интегрировать поиск в авто.ру в платформу (на данном этапе – карточку) в поисковую платформу минимальными усилиями.

Из-за того, что часть обогащений оффера происходит в auto2-shard, а офферы на индексацию в платформу сейчас отправляются из
VOS2, то между ответами от платформы и от старого поиска есть существенная разница.

Обогащений для авто несколько десятков, переносить их все как в VOS, так и в другой сервис, долго, нудно,
и не хотелось бы на начальном этапе.

### Ограничения

1. Платформа ожидает получать только значимо изменившиеся документы
2. Платформа ожидает получать документ во внутреннем, доменно-независимом формате ([RawDocument](https://a.yandex-team.ru/arcadia/classifieds/vs/services/vasgen/docs/indexing.md#dokument)),
внутри которого уже может быть ApiOffer
3. shard посылает все документы на реиндексацию каждые 5 минут


### Новый flow индексации
![Архитектура](auto-index-updater-pipeline.png "Architecture")

1. Принимает все офферы от шарда (вся база каждые ~5 мин), после всех обогащений (grpc api)
2. Проверяет какие из них значимо изменились (хранит версии документов, хеши документов, возможно хеши полей в собственной базе)
3. Конвертирует изменившиеся офферы в RawDocument
4. Отправляет изменившиеся офферы в формате RawDocument на индексацию в VS c новой версией
5. Сохраняет в БД версии отправленных документов (принятых vs-receiver)

Так как в будущем возможно, что нам нужно будет индексировать и делать запросы по каким-то искусственным полям,
которые не представлены в ApiOffer, то между auto2-shard и auto-index-updater будет передаваться
обёртка над оффером с этими дополнительными полями.

#### Таблица офферов

____
| Column          | Description                                             |
|-----------------|---------------------------------------------------------|
| offer_id        | id оффера в формате "1102797810-83f884d1"               |
| hash            | хэш от всех полей оффера                                |
| version         | версия документа  в VS                                   |
| status          | Статус: ждёт отправки, отправлен, ждёт удаления, удалён |
| last_updated_dt | Время последнего обновления                             |



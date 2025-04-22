# Индексация
    
## Общее описание

### Глоссарий

**Клиент** – совокупность микросервисов со стороны бизнес-задач,
использующий индексацию и поиск в интересах одной из предметных
областей. Например, _Объявления_.

**Сервис** – совокупность микросервисов со стороны поисковой
инфраструктуры, обеспечивающий индексацию и поиск для документов,
присланных _клиентом_.

**Индексация** – процесс поставки документов из хранилищ _клиента_
до поисковой системы.

**Эпоха** – версия схемы данных. Может меняться при смене типов полей обратно несовместимым образом или "переливках" при аварийных ситуациях.

### Компоненты

![Рис. 1. Жизненный цикл документа](assets/indexing-cycle.png)
Рис. 1. Жизненный цикл документа

`<client>` - микросервис со стороны _клиента_, взаимодействующий
посредством API с _сервисом_.

`receiver` - компонент _сервиса_, занимающийся приёмом и валидацией документов
от клиента.

`YDB` – база данных, использующаяся в качестве хранилища для маппинга полей,
метаинформации обработанных документов и транзакционной очереди 
индексации. 

`indexer` – компонент сервиса, отвечающий за обработку промежуточной
очереди в _YDB_ и преобразование в индексы поступающих документов.

`LB` ([LogBroker](https://logbroker.yandex-team.ru/docs/)) – высокопроизводительная очередь сообщений. Используется
для поставки документов в SaaS.

`SaaS` ([Search-as-a-Service](https://doc.yandex-team.ru/Search/saas/saas-overview/concepts/about.html)) – внешний компонент сервиса, предоставляемый
командой из поискового портала. На момент написания этой документации - "ядро" поискового
сервиса.

`searcher` - компонент сервиса, осуществляющий атрибутивный и полнотекстовый
поиск по заданным клиентом параметрам в индексе (SaaS на момент написания). 

[`broker`](https://github.com/YandexClassifieds/etc-mono/blob/master/services/broker/docs/delivery_guide.md) – внешний компонент сервиса, осуществляющий поставку копий
документов из очереди в персистентное хранилище YT для последующего
анализа и использования.

[`YT`](https://yt.yandex-team.ru/docs/) - систематизированное "холодное" хранилище данных. Туда сливаем лог всех прошедших через индексацию документов с телом документа.

### Роли

Поставкой документов занимается `<client>`. Команда _клиента_ отвечает
за содержимое документа до момента получения `ACK` о приёме документа от
`receiver` после проведения валидации.

`receiver` отвечает за валидацию структуры документа на соответствие
имеющейся в данной эпохе схеме и порядок документов в рамках одного ключа.
`receiver` запишет документ только в том случае, если документ пришёл более
свежий по совокупности параметров эпоха-версия-таймстемп.

`indexer` вычитывает документы из очереди, конвертирует и распределяет их
по топикам назначения.

`SaaS` _eventually_ индексирует отправленные документы и делает их
доступными в поиске.

`searcher` представляет собой поисковый интерфейс для обращения к
проиндексированным документам.

### Документ

Документ – набор полей и их значений, объединённых уникальным в клиенте
первичным ключон.

Документ, представляемый к индексации, представляет собой protobuf-сообщение
в модели RawDocument.

Документ **ДОЛЖЕН** иметь уникальный [ключ](https://github.com/YandexClassifieds/schema-registry/blob/2940be3c81506c574161059ec9c5b50d6997567d/proto/vertis/vasgen/document.proto#L42).

Документ **ДОЛЖЕН** иметь неубывающую [версию документа](https://github.com/YandexClassifieds/schema-registry/blob/2940be3c81506c574161059ec9c5b50d6997567d/proto/vertis/vasgen/document.proto#L44) и возрастающий timestamp.

Документ **ДОЛЖЕН** иметь одно из возможных для него [событий](https://github.com/YandexClassifieds/schema-registry/blob/2940be3c81506c574161059ec9c5b50d6997567d/proto/vertis/vasgen/document.proto#L45).

Документ **ДОЛЖЕН** иметь [логическую эпоху](https://github.com/YandexClassifieds/schema-registry/blob/2940be3c81506c574161059ec9c5b50d6997567d/proto/vertis/vasgen/document.proto#L46)
не меньшую, чем используемая в данный момент актуальная.

Документ **ДОЛЖЕН** иметь [момент времени](https://github.com/YandexClassifieds/schema-registry/blob/2940be3c81506c574161059ec9c5b50d6997567d/proto/vertis/vasgen/document.proto#L48),
в который он был составлен.

Документ **ДОЛЖЕН** иметь одно или более индексируемых полей, которые **ДОЛЖНЫ**
соответствовать схеме, устоявшейся в данной эпохе.

Документ _МОЖЕТ_ иметь [время жизни](https://github.com/YandexClassifieds/schema-registry/blob/2940be3c81506c574161059ec9c5b50d6997567d/proto/vertis/vasgen/document.proto#L47).
Если это поле задано, то после истечения срока жизни документа он будет
_когда-то после_ удалён из индекса.

Документ _МОЖЕТ_ иметь один или более [embedding вектор](https://github.com/YandexClassifieds/schema-registry/blob/2940be3c81506c574161059ec9c5b50d6997567d/proto/vertis/vasgen/document.proto#L49),
которые **ДОЛЖНЫ** соответствовать схеме, устоявшейся в данной эпохе.

Поля и embedding **ДОЛЖНЫ** иметь уникальные имена в пределах устоявшейся
схемы эпохи.

### Гарантии

`receiver` возвращает Ack только в том случае, если валидация документа
пройдена и транзакция с добавлением в очередь YDB завершилась успехом - то есть, документ соответсвует схеме в эпохе и более
свежий по совокупности параметров эпоха-версия-таймстемп.

`indexer` изменяет статус документа в очереди только в том случае, если
конвертация и отправка в LogBroker завершилась успешно.

## Схема БД в YDB

Таблица реестра документов. Реестр хранит в себе актуальные версии документов и временно хранит удалённые в качестве "могилок".

```clickhouse
CREATE TABLE `<client>/index/registry`
(
  hash Uint64, -- хеш от ключа, для распределения по таблеткам
  pk Utf8, -- ключ документа
  version Int64, -- версия
  epoch Int64, -- эпоха
  status Int32, -- статус - жив или могилка
  modify_timestamp Timestamp, -- время последней модификации
  compression Int32, -- тип сжатия документа
  ttl Timestamp, -- время протухания документа
  document String, -- объект RawDocument, сжатый compression

  PRIMARY KEY (hash, pk)
) WITH (
    TTL = Interval("PT0S") ON ttl
);
```

Таблицы очереди и оффсетов. Элементы очередей указывают на pk конкретной версии. Если pk с такой версией уже нет - запись пропускается.

```clickhouse
CREATE TABLE `<client>/queue/$id/elements` -- id: main, emergency, failed...
(
  shard Int32, -- шард в очереди, для размазывания нагрузки по индексерам. Один документ всегда попадает в один шард очереди
  idx Uint64, -- смещение в очереди, монотонно возрастающее
  pk Utf8, -- ключ документа
  epoch Int64, -- эпоха
  version Int64, -- версия документа
  modify_timestamp Timestamp, -- время последней модификации документа

  PRIMARY KEY (shard, idx)
);

CREATE TABLE `<client>/queue/$id/offsets`
(
  groupId Utf8, -- id группы читателей
  shard Int32, -- номер шарда
  idx Uint64, -- последнее прочитанное

  PRIMARY KEY (groupId, shard)
);
```

## Пайплайн

1. `receiver` принимает документ и валидирует его в транзакции, предварительно считав текущее состояние в реестре. В случае успеха он обновляет его статус в реестре и добавляет запись в очередь на обход.

```sql
-- все действия - в сериализуемой транзакции

DECLARE $pk AS Utf8;
DECLARE $version AS Int64;
DECLARE $modify_timestamp AS Timestamp;
DECLARE $epoch AS Int64;
DECLARE $status AS Int32;
DECLARE $compression AS Int32;
DECLARE $ttl AS Timestamp;
DECLARE $ttl_rules AS String;
DECLARE $document AS String;

DECLARE $shard AS Int32;
DECLARE $offset AS Uint64;

REPLACE INTO `<client>/index/registry` (
    hash,
    pk,
    version,
    epoch,
    modify_timestamp,
    status,
    compression,
    ttl,
    document
) SELECT
      Digest::CityHash($pk) as hash,
      $pk as pk,
      $version as version,
      $epoch as epoch,
      $modify_timestamp as modify_timestamp,
      $status as status,
      $compression as compression,
      $ttl as ttl,
      $document as document;
  
UPSERT INTO `<client>/queue/main/elements` VALUES ($shard, $offset, $pk, $version, $modify_timestamp);
```

2. `indexer` вычитывает N записей из очереди по своему оффсету. Шарды назначаются индексерам в зукипере, в один момент в одной группе только один шард может коммитить оффсеты.

```sql
-- получаем текущий оффсет. Если такого нет - то пробуем заинсертить null и двигаемся дальше без условия на индекс.

DECLARE $shard AS Int32;
DECLARE $groupId AS Uint64;

SELECT o.shard, o.idx FROM `<client>/queue/main/elements` AS o WHERE o.groupId = $groupId AND o.shard = $shard;

-- получаем все актуальные записи (для неактуальных r.document будет NULL и мы его пропустим, залоггировав e.pk и e.version)

DECLARE $shard AS Int32;
DECLARE $lastIdx AS Uint64;

SELECT
  e.shard AS shard,
  e.idx AS idx,
  e.pk AS pk,
  e.version AS version,
  r.document AS document,
  r.compression AS compression,
  r.status AS status
FROM `<client>/queue/main/elements` AS e
LEFT JOIN `<client>/index/registry` AS r ON
  r.hash = Digest::CityHash(e.pk) AND
  r.pk = e.pk AND
  r.epoch = e.epoch AND
  r.version = e.version AND
  r.modify_timestamp = e.modify_timestamp
WHERE e.shard = $shard AND e.idx > $lastIdx
ORDER BY shard, idx
LIMIT 100;

-- здесь происходит необходимая обработка в индексере - конвертация, отправка в LB и прочее
-- отправляем сфейлившиеся записи в fail очередь (если есть). fail очереди и прочие обрабатываются аналогичным образом.

DECLARE $failures AS List<Struct<shard: Int32, idx: Uint64, pk: Utf8, version: Int64>>;

REPLACE INTO `<client>/queue/failed/elements`
SELECT * FROM AS_TABLE($failures);

-- коммитим оффсет

DECLARE $groupId AS Utf8;
DECLARE $shard AS Int32;
DECLARE $prevOffset AS Uint64;
DECLARE $newOffset AS Uint64;

UPDATE `<client>/queue/main/offsets`
SET idx = $newOffset
WHERE groupId = $groupId AND shard = $shard AND idx = $prevOffset;
```

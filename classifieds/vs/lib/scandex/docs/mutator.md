# Mutator

Задача модуля - вносить изменения в существующий индекс, сериализовать его 
для последующего использования в качестве поискового движка

- Операция (`SchemaOperation`) - операция над базой в целом. Insert, Update, Upsert, Unset, Remove, Compact.
- Команда (`IndexUpdateCommand`) - информация для индекса об изменении его состояния. 

## Список операций

### Insert. Добавить новый документ key = PK

```scala
type Index // Индекс, значение которого надо установить
type Value // Значение, характерное для данного индекса 

case class Insert[PK](key: PK, fields: Map[Index, Value])
```

Сначала в PrimaryIndex для данного PK создается новый DocumentId на 1 больше предыдущего 
максимального, что не требует перестройки всех индексов.

После этого в каждый из индексов добавляется соответствующее значение

### Remove. Удалить документ id = PK

```scala
case class Remove[PK](key: PK)
```

В `PrimaryIndex[key]` выставляется значение Unset.

После этого выставляется значение Unset для всех `Index[DocumentId]`

### Compact. Упаковать базу

```scala
case object Compact
```

Все документы, помеченные в `PrimaryIndex` как Unset, удаляются физически, размер `PrimaryIndex` 
уменьшается на их число. 

После этого все индексы перестраиваются аналогичным образом.

### Update. Изменить значения текущего документа

```scala
case class Update[PK](key: PK, fields: Map[Index, Value])
```

С помощью `PrimaryIndex[key]` ищется DocumentId, после чего для всех индексов выполняется `Index[DocumentId] = Value`

### Upsert. Изменить или добавить документ

```scala
case class Upsert[PK](key: PK, fields: Map[Index, Value])
```

С помощью `PrimaryIndex[key]` ищется DocumentId. В случае, если за данным ключом документа не значится,
выделяется новый DocumentId. После этого для всех индексов выполняется `Index[DocumentId] = Value`

### Unset. Удалить значение индекса

```scala
case class Unset[PK](key: PK, fields: Seq[Index])
```

С помощью `PrimaryIndex[key]` ищется DocumentId. 
После чего для всех `Index[DocumentId]` выставляется значение Unset

### Необъявленные команды

Возможно, нужны будут команды модификации схемы: добавить индекс, сменить тип индекса,удалить.
Возможно, все это будет делаться с помощью кодогенератора и scandex будет кушать заранее 
подготовленную схему.

### Реализация

Все операции будут порождать набор команд по изменению конкретных индексов. 
Для ускорения работы команды будут объединяться в группы по несколько команд.
Команда Compact всегда будет выполняться изолированно.

```scala
sealed trait IndexUpdateCommand
case class SetValueCommand[T](v: T, id: DocumentId) extends IndexUpdateCommand
case class UnsetValueCommand(id: DocumentId)        extends IndexUpdateCommand
case class RemoveDocuments(ids: Seq[DocumentId])    extends IndexUpdateCommand
```

Операции Insert, Update, Upsert, Unset, Remove будут транслироваться для каждого индекса
в набор команд SetValueCommand & UnsetValueCommand.

Операция Compact для каждого индекса будет транслироваться в команду RemoveDocuments.

# Хранящий индекс

Служит для хранения значений, сопоставленных документам. Позволяет получить 
значения поля [документа](glossary.md#document) по его `DocumentId`.

Наличие значения у поля документа опционально.

```scala
trait Storage[@specialized T] {
  def values(documentId: DocumentId): Task[List[T]]
}
```

## Внутреннее устройство реализации

### StorageIndexImpl

Содержит в себе следующие сегменты:  
- [Прямой индекс](glossary.md#segment-forward), отвечающий на вопрос, какой `ValueIdx` соответствует 
заданному `DocumentId`
- [Хранилище значений](glossary.md#segment-values-storage), отвечающий на вопрос, какое значение поля соответствует
заданному `ValueIdx` 

### Реализация прямого индекса

Реализация описана в документе [ForwardSegment](segment_forward.md)

#### Реализация хранилища значений

Реализация описана в документе [ValueStorageSegment](segment_value.md)

#### Сериализация и десериализация

***TODO*** Описать сериализацию и десериализацию структуры

[cardinality]: glossary.md#cardinality


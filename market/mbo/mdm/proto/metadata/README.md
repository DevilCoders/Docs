## Прото сервис для работы с метаданными БМДМ

### MdmEntityTypeService
Сервис для работы с метадатой сущностей БМДМ, позволяет как извлечь сами метаданные сущности, так и связанных с ней объектов: атрибутов, енам опций.

На данном этапе сервис ничего не знает о внешних связях

#### Методы:
TBD

### MdmAttributeService
Сервис для работы с метадатой автрибутов БМДМ, позволяет как извлечь метаданные атрибутов, так и связанных с ней объектов: енам опций.

На данном этапе сервис ничего не знает о внешних связях

#### Методы:
TBD

### MdmEnumOptionService
Сервис для работы с метадатой енам опций БМДМ, позволяет извлечь метаданные опций

На данном этапе сервис ничего не знает о внешних связях

#### Методы:
TBD

### MdmExternalReferenceService
Сервис для работы с внешними связями объектов метаданных БМДМ. В

#### Методы:
- getExternalReferencesOnlyByFilter - метод позволяет найти внешние связи по фильтру
- updateExternalReferences - позволяет обновить или создать новую внешнюю связь

### Сценарии использования
#### Найти полный набор метаданных для заданной EntityType
1. Находим все метаданные для заданной сушности:
```kotlin
val filter = MdmEntityTypeSearchFilter.newBuilder()
    .addMdmId(mdmEntity.mdmId)
    .setIncludeRelatedData(true) // хотим получить вложенные атрибуты и опции для енамов
    .setShallow(false) // хотим получить вложенные сущности
    .build()
val request = MdmEntityTypesByFilterRequest.newBuilder()
    .setFilter(filter)
    .build()
val response = client.getEntityTypesByFilter(request)
```
2. Находимо все внешние связи для заданной сущности
```kotlin
val filter = MdmExternalReferenceSearchFilter.newBuilder()
    .addPath(
        MdmPathFilter
            .setPath(
                MdmPath.newBuilder()
                    .addSegment(
                        MdmPathSegment.newBuilder()
                            .setMmdId(mdmEntity.mdmId) // задаем только самые верхний сегмент пути
                            .setMdmMetaType(MDM_ENTITY_TYPE)
                    )
            )
            .setCondition(WITH_CHILDREN) // Добаляем всех потомков
    )
    .build()
val request = MdmExternalReferencesByFilterRequest.newBuilder()
    .setFilter(filter)
    .build()
val response = client.getExternalReferencesByFilter(request)
```
 3. Теперь при обходе метаданных из шага 1 мы можем по полученному ответу о внешних связях получить все необходимые данные по ним в данной точке пути

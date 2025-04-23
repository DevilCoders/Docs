# Группы воркфлоу

Запросы позволяют получить список групп воркфлоу и подробную информацию по любой из них.

#### Список групп

```
{{ host }}/{{ api-ver }}/workflow_groups
```

#### Параметры определенной группы

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>
```

## Связанные объекты {#section_wdh_cgt_gbb}

#### Идентификаторы вышестоящих групп

Идентификаторы родительских групп:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/relationships/parents
```

Идентификаторы всех предков группы:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/relationships/ancestors
```

#### Развернутый список вышестоящих групп

Список родительских групп:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/parents
```

Список всех предков группы:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/ancestors
```

#### Идентификаторы вложенных групп

Идентификаторы дочерних групп:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/relationships/children
```

Идентификаторы всех потомков группы:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/relationships/descendants
```

#### Развернутый список вложенных групп

Список дочерних групп:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/children
```

Список всех потомков группы:

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/descendants
```

#### Идентификаторы воркфлоу группы

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/relationships/workflows
```

#### Развернутый список воркфлоу группы

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/workflow
```

#### Идентификаторы пакетов, к которым относится группа

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/relationships/packages
```

#### Развернутый список пакетов, к которым относится группа

```
{{ host }}/{{ api-ver }}/workflow_groups/<id группы>/packages
```


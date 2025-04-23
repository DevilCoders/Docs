# Воркфлоу

Запросы позволяют получить список воркфлоу и подробную информацию по любому из них.

#### Список воркфлоу

```
{{ host }}/{{ api-ver }}/workflows
```

#### Параметры определенного воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>
```

## Связанные объекты {#section_fhg_xcs_gbb}

#### Идентификаторы деплой-групп воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/relationships/deploy_groups
```

#### Развернутый список деплой-групп воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/deploy_groups
```

#### Идентификаторы пакетов, к которым относится воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/relationships/packages
```

#### Развернутый список пакетов, к которым относится воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/packages
```

#### Идентификатор проекта, к которому относится воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/relationships/project
```

#### Параметры проекта, к которому относится воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/project
```

#### Идентификаторы групп, в которые входит воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/relationships/workflow_groups
```

#### Развернутый список групп, в которые входит воркфлоу

```
{{ host }}/{{ api-ver }}/workflows/<id воркфлоу>/workflow_groups
```


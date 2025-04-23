# Пакеты

Запросы позволяют получить список пакетов и подробную информацию по любому из них.

#### Список пакетов

```
{{ host }}/{{ api-ver }}/packages
```

#### Параметры определенного пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>
```

## Связанные объекты {#section_dk2_prl_gbb}

#### Идентификаторы воркфлоу пакета

Только воркфлоу, напрямую подключенные к пакету (без учета групп воркфлоу):

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/workflows
```

Все воркфлоу, подключенные к пакету (с учетом групп воркфлоу):

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/all_workflows
```

#### Развернутый список воркфлоу пакета

Только воркфлоу, напрямую подключенные к пакету (без учета групп воркфлоу):

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/workflows
```

Все воркфлоу, подключенные к пакету (с учетом групп воркфлоу):

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/all_workflows
```

#### Идентификаторы выкладок пакета по деплой-группам

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/deploy_group_deploys
```

#### Развернутый список выкладок пакета по деплой-группам

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/deploy_group_deploys
```

#### Идентификаторы деплой-пар пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/deploy_specifiers
```

#### Развернутый список деплой-пар пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/deploy_specifiers
```

#### Идентификаторы выкладок пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/package_deploys
```

#### Развернутый список выкладок пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/package_deploys
```

#### Идентификаторы пресервисов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/preservices
```

#### Развернутый список пресервисов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/preservices
```

#### Идентификаторы репозиториев пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/repos
```

#### Развернутый список репозиториев пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/repos
```

#### Идентификаторы сервисов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/services
```

#### Развернутый список сервисов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/services
```

#### Идентификаторы подписчиков пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/subscribers
```

#### Развернутый список подписчиков пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/subscribers
```

#### Идентификаторы тегов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/tags
```

#### Развернутый список тегов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/tags
```

#### Идентификаторы тикетов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/tickets
```

#### Развернутый список тикетов пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/tickets
```

#### Идентификаторы версий пакета

```
{{ host }}/{{ api-ver }}/packages/<id пакета>/relationships/versions
```


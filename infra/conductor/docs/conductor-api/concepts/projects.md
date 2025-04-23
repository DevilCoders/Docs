# Проекты

Запросы позволяют получить список проектов и подробную информацию по любому из них.

#### Список проектов

```
{{ host }}/{{ api-ver }}/projects
```

#### Параметры определенного проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>
```

## Связанные объекты

#### Идентификаторы администраторов проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/relationships/admins
```

#### Развернутый список администраторов проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/admins
```

#### Идентификаторы деплой-групп проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/relationships/deploy_groups
```

#### Развернутый список деплой-групп проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/deploy_groups
```

#### Идентификаторы настроек выкладки проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/relationships/deploy_settings
```

#### Развернутый список настроек выкладки проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/deploy_settings
```

#### Идентификаторы групп хостов проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/relationships/groups
```

#### Развернутый список групп хостов проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/groups
```

#### Идентификаторы тегов проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/relationships/tags
```

#### Развернутый список тегов проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/tags
```

#### Идентификаторы воркфлоу проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/relationships/workflows
```

#### Развернутый список воркфлоу проекта

```
{{ host }}/{{ api-ver }}/projects/<id проекта>/workflows
```


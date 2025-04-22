# Тикеты

Запросы позволяют получить список тикетов и подробную информацию по любому из них.

#### Список тикетов

```
{{ host }}/{{ api-ver }}/tickets
```

Вы можете фильтровать тикеты по времени создания или изменения с помощью параметра `filter`:

```
{{ host }}/{{ api-ver }}/tickets?filter[created_at]=<дата1>..<дата2>&filter[updated_at]=<дата3>..<дата4>
```

Даты записываются в формате ISO-8601: `YYYY-MM-DD` или `YYYY-MM-DDThh:mm:ss±hh:mm`.

#### Параметры определенного тикета

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>
```

## Связанные объекты {#section_wts_wcs_gbb}

#### Идентификатор автора тикета

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/relationships/author
```

#### Параметры автора тикета

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/author
```

#### Идентификаторы пакетов тикета

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/relationships/packages
```

#### Развернутый список пакетов тикета

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/packages
```

#### Идентификаторы подписчиков

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/relationships/subscribers
```

#### Развернутый список подписчиков

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/subscribers
```

#### Идентификаторы тасков тиекта

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/relationships/tasks
```

#### Развернутый список тасков тиекта

```
{{ host }}/{{ api-ver }}/tickets/<id тикета>/task
```


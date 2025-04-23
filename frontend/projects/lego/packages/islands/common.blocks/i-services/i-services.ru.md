# i-services

Используется для получения локализованных имени и адреса сервиса по его идентификатору.

## Обзор

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [id](#field-id) | `String` | Идентификатор сервиса. |
| [region](#field-region) | `String` | Регион. |

<a name="elems"></a>

### Элементы блока

| Элемент | Описание |
| ------- | -------- |
| [name](#elem-name) | Имя сервиса. |
| [url](#elem-url) | Адрес сервиса. |

## Подробное описание

### Поля блока

<a name="field-id"></a>

#### Поле `id`

Определяет идентификатор сервиса.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['search', 'market', 'translate'],
    body: [
        ['search', 'market', 'translate'].map(function(id) {
            return {
                block: 'i-services',
                id: id,
                elem: 'url'
            };
        })
    ]
}
```

<a name="field-region"></a>

#### Поле `region`

Определяет регион сервиса.

Тип: `String`.

```js
{
    block: 'x-table',
    head: ['search', 'market', 'translate'],
    body: [
        ['search', 'market', 'translate'].map(function(id) {
            return {
                block: 'i-services',
                id: id,
                region: 'tr',
                elem: 'url'
            };
        })
    ]
}
```

### Элементы блока

<a name="elem-name"></a>

#### Элемент `name`

Определяет имя сервиса.

```js
{
    block: 'x-table',
    head: ['search', 'market', 'translate'],
    body: [
        ['search', 'market', 'translate'].map(function(id) {
            return {
                block: 'i-services',
                id: id,
                elem: 'name'
            };
        })
    ]
}
```

<a name="elem-url"></a>

#### Элемент `url`

Определяет адрес сервиса.

```js
{
    block: 'x-table',
    head: ['search', 'market', 'translate'],
    body: [
        ['search', 'market', 'translate'].map(function(id) {
            return {
                block: 'i-services',
                id: id,
                elem: 'url'
            };
        })
    ]
}
```

# footer

Используется для создания подвала страницы из двух столбцов. Столбцы могут заполняться элементами по умолчанию, произвольными элементами в зависимости от потребностей сервиса, либо оставаться пустыми.

Блок является необязательной частью страницы сервиса.

## Обзор

### Поля блока

| Поле | Тип | Описание |
| ---- | --- | -------- |
| [tld](#field-tld) (req) | `String` | Название домена |
| [region](#field-region) | `String` | Регион |
| [start](#field-start) | `Number` | Год запуска сервиса и знак копирайта Яндекса |
| [statUrl](#field-statUrl) | `String` | Ссылка на статистику. Необходимо для КУБР |
| [content](#field-content) | `String` | Набор собственных ссылок |

req — обязательное поле.

### Поля блока

<a name="field-tld"></a>

#### Поле `tld`

Определяет название домена. Используется для определения содержимого блока (различается для КУБР и Турции). **Обязательное**.

Тип: `String`.

```js
{
    block: 'footer',
    tld: 'ru'
}
```

<a name="field-region"></a>

#### Поле `region`

Определяет регион. 

Тип: `String`.

```js
{
    block: 'footer',
    start: 2018,
    tld: 'com.tr',
    region: 'tr'
}
```

<a name="field-start"></a>

#### Поле `start`

Определяет год запуска сервиса и устанавливает знак копирайта Яндекса.

Тип: `Number`.

```js
{
    block: 'footer',
    tld: 'ru',
    start: 2018
}
```

<a name="field-statUrl"></a>

#### Поле `statUrl`

Определяет ссылку на статистику. Необходимо для КУБР.

Тип: `String`.

```js
{
    block: 'footer',
    tld: 'ru',
    statUrl: '//stat.yandex.ru/stats.xml?ReportID=-225&ProjectID=1'
}
```

<a name="field-content"></a>

#### Поле `content`

Определяет набор собственных ссылок. Если поле не задано, набор определяется ссылками по умолчанию.

Тип: `String`.

```js
{
    block: 'footer',
    content: [
        {
            elem: 'column',
            content: [
                {
                    elem: 'link',
                    url: '#',
                    content: 'Первая ссылка'
                },
                {
                    elem: 'link',
                    url: '#',
                    content: 'Вторая ссылка'
                }
            ]
        },
        {
            elem: 'column',
            elemMods: { side: 'right' },
            content: {
                block: 'copyright',
                content: 'Компания ответственных профессионалов'
            }
        }
    ]
}
```
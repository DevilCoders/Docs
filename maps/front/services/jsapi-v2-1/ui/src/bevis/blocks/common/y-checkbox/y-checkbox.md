# y-checkbox: чекбокс

## Соответствие дизайну

- http://guide.yandex-team.ru/#blocks-check

## Варианты представления

| view          | Описание | Гайд
| ------------- | ---------|-------
| `islet`       | Чекбокс в островном дизайне версии 3.0 | type: normal & size: m
| `islet-large` | Чекбокс увеличенного размера | type: normal & size: l

## Настройки шаблона

<!--BTJSON_API-->

## API блока

<!--JS_API-->

## Примеры: обычный чекбокс

```btjson
{block: 'y-checkbox'},
{block: 'y-checkbox', label: 'Лейбл'},
{block: 'y-checkbox', checked: true, label: 'Выбранный (checked) чекбокс'},
{block: 'y-checkbox', indeterminate: true, label: 'Неопределенный (indeterminate) чекбокс'},
{block: 'y-checkbox', disabled: true, label: 'Заблокированный (disabled) чекбокс'},
{block: 'y-checkbox', disabled: true, checked: true, label: 'Заблокированный  выбранный чекбокс'},
{block: 'y-checkbox', disabled: true,  indeterminate: true, label: 'Заблокированный неопределенный чекбокс'}
```

## Примеры: большой чекбокс

```btjson
{block: 'y-checkbox', view: 'islet-large', label: 'Большой чекбокс'},
{block: 'y-checkbox', view: 'islet-large', checked: true, label: 'Выбранный (checked) большой чекбокс'},
{block: 'y-checkbox', view: 'islet-large', indeterminate: true, label: 'Неопределенный (indeterminate) большой чекбокс'},
{block: 'y-checkbox', view: 'islet-large', disabled: true, label: 'Заблокированный (disabled) чекбокс'},
{block: 'y-checkbox', view: 'islet-large', disabled: true, checked: true, label: 'Заблокированный  выбранный чекбокс'},
{block: 'y-checkbox', view: 'islet-large', disabled: true,  indeterminate: true, label: 'Заблокированный неопределенный чекбокс'}
```

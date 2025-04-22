# i-glue-field_type_inline-bemhtml

Специальный вид поля для текстов, в которых может быть html-код
Отличаются от inline тем, что добавляются в DOM через replace->BEMHTML.apply,
то есть с инициализацией js внутренних блоков

## Пример
``{
    elem: 'model-field',
    js: { name: 'strategyOptionsHint', type: 'inline-bemhtml' }
}
``

Используется в b-campaign-strategy2.js

## Мейнтейнеры
[anyakey](https://staff.yandex-team.ru/)

# Tags

## `type`

Тип может быть  `Tags.TYPE.CHECK`, `Tags.TYPE.RADIO` или `Tags.TYPE.RADIO_CHECK`.
Последний нужен для всяких фильтров, когда есть вариант "Ничего не выбрано", который задается через `value=""`.
В `value` должна быть строка, совпадающая с одним из `value` Tag'ов. Для RADIO и RADIO_CHECK ещё может быть булевое значение.

```typescript
<Tags onChange={ onChange } value={ value } type={ Tags.TYPE.RADIO }>
    <Tag value="value1">Один</Tag>
    <Tag value="value2">Два</Tag>
    <Tag value="value3">Три</Tag>
</Tags>

<Tags onChange={ onChange } value={ value } type={ Tags.TYPE.RADIO_CHECK }>
    <Tag value="">Все</Tag>
    <Tag value="value1">Один</Tag>
    <Tag value="value2">Два</Tag>
    <Tag value="value3">Три</Tag>
</Tags>
```

## Вариант с урлами вместо `onChange`

Например, селектор категорий на морде — это просто несколько ссылок,
одна из которых зачекана.

```typescript
<Tags value={ value } type={ Tags.TYPE.RADIO }>
    <Tag value="value1" url="/1/">Один</Tag>
    <Tag value="value2" url="/2/">Два</Tag>
    <Tag value="value3" url="/3/">Три</Tag>
</Tags>
```


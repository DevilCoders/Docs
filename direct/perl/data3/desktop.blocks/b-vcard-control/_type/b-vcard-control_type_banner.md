# Блок для вывода визитки в баннере

## Параметры блока
```
{
    is_vcard_open: {Boolean}, //визитка открыта
    is_vcard_collapsed: {Boolean} //визитка по смыслу считается открытой и существующей, но спрятана кликом под кнопку "скрыть"
    modelParams: {
        id: this.banner && this.banner.modelId,
        name: 'm-banner',
        parentName: 'm-group',
        parentId: this.group.modelId
    },
    errors: {Array}, //ошибки визитки пришедшие с сервера
    hasCopyFromPrev: {Boolean}, //есть ссылка "скопировать из предыдущей"
    vcard: {Object} //объект с данными визитки
}
```


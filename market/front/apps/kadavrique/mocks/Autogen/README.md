# AutogenApi

[Документация](https://github.yandex-team.ru/market-java/autogeneration).

## uploadPicture

Имитирует загрузку картинки в аватарницу. В стейте объект, ключ: uploadPicture

```
{
    origFileName: 'pin1.jpg',
    url: 'https://avatars.mdst.yandex.net/get-good_partner_images/1397962/87de93a1-2106-43dd-a389-03c3fe9ef445/orig',
}
```

## getContentStateByShopSku

Имитирует поход за состоянием контента для ассортиментной позиции. В стейте объект, ключ: getContentStateByShopSku

```
{
    contentStatus: 'NO_CONTENT' || 'CONTENT_PROCESSING_NEW',
    ssku: shopSku,
    contentData: {
        actual: {
            contentId: shopSku,
            contentType: 'NEW_CONTENT',
            categoryId: 90559,
        },
    },
}
```

## getCategoryRestriction

Возвращает список доступных для выбора категорий psku. В стейте объект, ключ - getCategoryRestriction.

```
{
    allowedType: 'ANY' | 'SINGLE' | 'GROUP',
    allowedCategoriesIds: [123, 456, 789],    
}
```

## getCategoryById

Возвращает параметры категории. В стейте объект, ключ - getCategoryById.
На странице может вызываться несколько раз с разными categoryId, поэтому результат берется из стейта по id категории.

```
{
    '100500': {
        categoryId: 100500,
        name: 'Диктофоны и портативные рекордеры',
        fullCategoryName: 'Все товары/Электроника/Портативная техника/Диктофоны',
        parameters: [],
        groups: [],
    },
}
```

## getContentData

Возвращает данные контента. В стейте объект, ключ - getContentData.

```
{
    categoryId: 90559,
    contentStatus: 'NO_CONTENT',
    parameters: {
        '7351771': ['Какой sku, такой и диктофон'],
        '7893318': ['Восхитительные диктофоны доктора Диктофониуса'],
        '-12': ['generated-by-AT-1581591115792'],
    },}
```

# company-card-with-photo

Карточка компании с фото слева. Использует `company-card`. В качестве данных принимает нормализованный объект компании.
// TODO: описать нормализованный объект компании

```js
{
    block: 'company-card-with-photo',
    url: `${data.env.pathPrefix}/${company.id}/edit/`, // ссылка с заголовка, опциональна
    editPhotoUrl: `${data.env.pathPrefix}/${company.id}/edit/photos/`, // ссылка с заглушки для фото, опциональна, фоллбек на url
    company: {
        id: 42,
        names: [],
        address: {},
        emails: [],
        phones: [],
        urls: [],
        rubrics: []
    }
}
```

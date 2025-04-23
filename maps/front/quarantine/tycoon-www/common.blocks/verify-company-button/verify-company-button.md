# verify-company-button

Кнопка «Это моя компания», триггерящая событие `verifyRequest` со своими js-параметрами в качестве данных.
Используется в `company-card-with-map` для отображения диалога добавления организации к аккаунту (`request-confirm-code-dialog`).

```js
{
    block: 'verify-company-button',
    js: { company } // объект компании
}
```

## Описание

Блок **nameplate** — метка с названием сервиса (шильдик).

### API блока

  * `{String} name` — название сервиса отображаемое на шильдике;
  * `{String} url` — адрес главной страницы сервиса;
  * `{String} service` — ключ сервиса.

Следует указать либо оба поля `name`, `url`, либо поле `service`.
Во втором случае название и адрес сервиса будут получены по ключу из блока
[i-services](../i-services/i-services.ru.md).
Блок `i-service` в этом случае нужно добавить в зависимости.

### Варианты использования блока

Указание `name`, `url`:

```js
{
    block: 'nameplate',
    name: 'Почта',
    url: 'https://mail.yandex.ru/'
}
```

Указание `service`:

```js
[
    { // deps.js
        block: 'i-services'
    },
    {
        block: 'nameplate',
        service: 'mail'
    }
]
```

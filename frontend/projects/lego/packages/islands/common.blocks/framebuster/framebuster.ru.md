## Описание

Блок `framebuster` —  блок, защищающий открытие страниц в `<iframe>` в разных доменах. В случае неразрешенного домена основной страницы (определяется через `document.referrer`) делает софтверный редирект основной странице на страницу, которую пытаются открыть в `<iframe>`.

### JS API
* `{RegExp[]|String[]|RegExp|String} whitelist` – массив или единичное значение строк или регулярных выражений, содержащих доменные имена или маски доменов.

Пример передачи параметра `whitelist` блоку `framebuster`:

```javascript
BEM.DOM.decl("example", {
    onSetMod: {
        js: function() {
            BEM.create({block: 'framebuster'}, {whitelist:[/yandex\.ru$/]});
        }
    }
});
```

### Модификатор блока
Необязательный.

`type` со значением `yandex` – включение в доверенный список доменов `yandex` и `yandex-team`.

Пример добавления метки сервиса для поисковой формы:

```javascript
BEM.DOM.decl("example", {
    onSetMod: {
        js: function() {
            BEM.create({block: 'framebuster', mods:{type: 'yandex'}});
        }
    }
})
```

# i-counter

Вызов счетчиков сервиса [Яндекс.Статистика](http://doc.yandex-team.ru/Stat/guide-manager/concepts/about.xml).

Лего содержит JavaScript-API для вызова счетчиков Яндекс.Статистики. Счетчик может срабатывать на разные события. Чаще всего
это посещение страницы пользователем или клик.

Для того, чтобы вызвать счетчик, необходимо знать `pid` (`id` проекта) и `cid` (`id` счетчика). Эти `id` можно получить
при создании счетчика. Подробное описание [как создать новый счетчик](http://doc.yandex-team.ru/Stat/ManagerGuide/tasks/HowToInstallCounter.xml).

По возможности, для отправки запросов счетчика используется `navigator.sendBeacon`, иначе — вставка тега `script`.

### Счетчик клика на ссылку или показа страницы

В случае клика c заданным параметром `noRedirect` или учета показа динамически создает скрипт с URL системы учета.
В случае клика c незаданным параметром `noRedirect` подменяет `href` на `redir`, потом по таймауту возвращает его обратно.

**Принимаемые параметры**

* `{String} w` — параметры счетчика. **Обязательный**.
* `{HTMLElement} a` — ссылка, клик на которую надо учитывать.
* `{Object} opts`
  * `{Boolean} opts.noRedirect` — обрабатывать клик без редиректа. Значение по умолчанию: `true`.
  * `{Boolean} opts.useLinkHref` — использовать URL в  параметре `data=url` нажатой ссылки вместо `location.href`. Значение по умолчанию: `false`.

**Примеры использования**

```html
<a href="http://meteoinfo.ru" onmousedown="Lego.c('stred/pid=7/cid=433',this)">Гидрометцентр</a>
<script type="text/javascript">Lego.c('stred/pid=7/cid=433')</script>
<a href="http://news.yandex.ru/sport.html" onmousedown="Lego.c('stred/pid=14/cid=73949', this, {noRedirect: true})">Спорт</a>
<image src='...' onmousedown="Lego.c('stred/pid=14/cid=73953', this, {noRedirect: true, useLinkHref: false})"/>
```

### Параметризированный счетчик клика на ссылку или показа
Чтобы вызвать счетчик клика на ссылку или показ страницы, необходимо в JavaScript вызвать функцию `Lego.cp` с вашими параметрами.
В случае клика она подменяет `href` из `redir`, потом по таймауту восстанавливает `href`.
В случае учета показа динамически создает скрипт с URL системы учета.

**Принимаемые параметры**

* `{Number} pi` — номер проекта (pid). **Обязательный**.
* `{Number} ci` — номер счётчика (cid). **Обязательный**.
* `{String} p` — [путь](https://wiki.yandex-team.ru/search-interfaces/counters/#path)
* `{*}  v` — [переменные](https://wiki.yandex-team.ru/search-interfaces/counters/#vars)
* `{String} a` — ссылка, клик на которую надо учитывать.
* `{Object} opts`
  * `{Boolean} opts.noRedirect` — обрабатывать клик без редиректа. Значение по умолчанию: `true`.
  * `{Boolean} opts.useLinkHref` — использовать URL в  параметре `data=url` нажатой ссылки вместо `location.href`. Значение по умолчанию: `false`.

**Примеры использования**

```html
<a href="http://meteoinfo.ru" onclick="Lego.cp(0,1917,'weather.tabs.fotki','my=var',this)">Гидрометцентр</a>
```

или

```html
<script type="text/javascript">Lego.cp(0,1917,'weather.tabs.fotki')</script>
```

### Важно знать

К некоторым блокам счетчик применяется автоматически. По умолчанию это происходит для 10% показов.
Чтобы отменить это поведение, нужно переопределить параметр `show-counters`.

* В BEMHTML, на своем уровне переопределения в файле `common.blocks/i-global/i-global.bemhtml.js`:

```javascript
block('i-global')
    .mode('public-params')
    .elem('show-counters')(function() {
            return 1;
    })
);
```
* Во входном BEMJSON:

```javascript
[
    {
        block: 'i-global',
        params: {
            'show-counters' : false
        }
    },
    {
        block: 'b-page',
         //...
    }
]
```

Подробнее о [i-global](../i-global/i-global.ru.md).

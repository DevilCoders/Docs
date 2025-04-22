# Миграция по МДА для islands 3.x

Изменения, связанные с работой по отрыву МДА в версиях `islands` 3.х затрагивают всего два блока — `i-update-session`и `lang-switcher`.

## i-update-session
[Коммит с изменениями](https://github.yandex-team.ru/lego/islands/commit/2a721cabb620aa2cf5f519b15f937d92334c3446) в [islands@4.x](https://github.yandex-team.ru/lego/islands/tree/support/4.x).

Необходимо изменить логику работы блока `i-update-session`. При наличии куки `mda` со значением `0`
по умолчанию должна использоваться ручка `${protocol}//passport.yandex.${tld}/auth/update/`.

```javascript
/* desktop.blocks/i-update-session/i-update-session.js */

// Добавьте статический метод `hasMda`, возвращающий `false`
// при наличии куки `mda` в значении `0`.
hasMda: function() {
    return !document.cookie.match(/\bmda=0\b/);
},

/* ... */

// В методе `getDefaultParams` в возвращаемом объекте значения
// ключей `path`, `host` будут зависеть от того, есть ли у пользователя 
// кука `mda` в значении `0`
getDefaultParams: function() {
    /* ... */
    var mda = this.hasMda(),
        Glob = BEM.blocks['i-global'];

    return {
        /* ... */
        host: mda ?
            Glob.param('pass-host') :
            location.protocol + '//passport.yandex.' + Glob.param('tld'),
        /* path: '/resign', */
        path: mda ? '/resign' : '/auth/update/',
        /* ... */
    };
},

/* ... */

// Также нужно будет внести соответствующие изменения в метод `start`
start: function() {
    /* ... */
    
    this._url = [
        /* Glob.param('pass-host'), */
        params.host,
        /* ... */
    ].join('');
    
    /* ... */
},

/* ... */
```

## lang-switcher
[Коммит с изменениями](https://github.yandex-team.ru/lego/islands/commit/a225d3f30923738d5353635271f98251efe6e67d) в [islands@4.x](https://github.yandex-team.ru/lego/islands/tree/support/4.x).

Старое API:
`https://tune.yandex.ru/api/lang/v1.1/save.xml`

Новое(MDA=0):
`https://www.yandex.$TLD/portal/set/lang/`. Информация про новое API — [Lang API](https://wiki.yandex-team.ru/tune/api/#langapi). 

При работе блока без МДА все ссылки для переключения языка должны вести
в другие ручки, которые уже зависят от доменов. Включить этот режим предлагается установкой в BEMJSON-параметра `disableMda` в значение `true`:

```js
{
    block: 'lang-switcher',
    disableMda: true
    /* ... */
}
```

Для этого нужно внести следующие правки:
```javascript
/* common.blocks/lang-switcher/lang-switcher.bemhtml */

/* ... */

var disableMda = this.ctx.disableMda,
    tld = this.['i-global'].tld,
    tuneAllUrl = (disableMda ? 'https://tune.yandex.' + tld : this['i-services'].serviceUrl('tune')) + '/lang',
    js = this.extend({
        disableMda: disableMda,
        'secret-key': this['i-global']['secret-key'],
        /* tune: this['i-services'].serviceUrl('tune'), */
        tune: disableMda ? 
            'https://www.yandex.' + tld :
            this['i-services'].serviceUrl('tune')
    }, this.ctx.js);

/* ... */

        // Элемент «ещё»
        {
            block: 'b-menu-vert',
            elem: 'layout-unit',
            mix: [{ block: 'lang-switcher', elem: 'all' }],
            content: {
                block: 'link',
                /* url: this['i-services'].serviceUrl('tune')+'/lang/', */
                url: tuneAllUrl,
                content: this.ctx.moreText || BEM.I18N('lang-switcher', 'all')
            }
        }
```

```javascript
/* common.blocks/lang-switcher/__lang/lang-switcher__lang.bemhtml */

/* ... */

!this.mods.selected, this.elemMods.selected != 'yes' {
    tag: 'a'

    js: {lang: this.ctx._lang.lang, url: this.ctx.url}

    attrs: {
        var ctx = this.ctx,
            lang = ctx._lang.lang,
            glob = this['i-global'],
            sk = glob['secret-key'],
            retpathParam = glob.retpath ? '&retpath=' + encodeURIComponent(glob.retpath) : '',
            /* handler = sk ? ('/api/lang/v1.1/save.xml?intl=' + lang + '&sk=' + sk + retpathParam) : '/lang/'; */
            handler = sk ? 
                (ctx.disableMda ? '/portal/set/lang/' : '/api/lang/v1.1/save.xml') : 
                '/lang/';

            
        handler = sk ? 
            handler + '?intl=' + lang + '&sk=' + sk + retpathParam : 
            handler;

        var urlBase = ctx.disableMda ? 
            'https://www.yandex.' + tld :
            this['i-services'].serviceUrl('tune');

        // Ручку /api/lang/v1.1/save.xml можно использовать только если есть secret-key.
        // https://wiki.yandex-team.ru/tune/api?from=isearch#langapi
        return {
            /* href: ctx.url || (this['i-services'].serviceUrl('tune') + handler), */
            href: ctx.url || (urlBase + handler),
            role: 'button',
            tabindex: 0
        };
    }
}

/* ... */
```

```javascript
/* common.blocks/lang-switcher/lang-switcher.js */

/* ... */

_getUrl: function(lang) {
    return this.params.tune + (this.params.disableMda ? '/portal/set/lang/' : '/api/lang/v1.1/save.xml?') + $.param({
        intl: lang,
        sk: this.params['secret-key'],
        retpath: this.params.retpath || BEM.blocks['i-global'].param('retpath') || window.location.href
    });
}

/* ... */
```

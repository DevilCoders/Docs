# express-http-langdetect

[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/express-http-langdetect/status.svg)](https://drone.yandex-team.ru/project-stub/express-http-langdetect)
Express middleware for [node-http-langdetect](https://github.yandex-team.ru/project-stub/node-http-langdetect)

Designed as an almost 'drop in' replacement for [express-langdetect](https://github.yandex-team.ru/project-stub/express-langdetect)

## How to use
Install: `npm install express-http-langdetect`

Since cookies are used, please don't forget to install and use `cookie-parser`.
There is also optional support [express-http-geobase](https://github.yanex-team.ru/project-stub/express-http-geobase) to
enable more precise language detection using geo region data. To enable this you should just `npm install express-http-geobase`
and `app.use` it before using `express-http-langdetect`. The same for [express-blackbox](https://github.yandex-team.ru/project-stub/express-blackbox).

Usage:
```
app.use(require('express-http-langdetect')(opts));
app.get('/', function (req, res) {
   console.log(req.langdetect);
});
```

`req.langdetect` is an object containing `id` and `name` fields, the result of langdetect `find` method call.
If an error occurred, `req.langdetect.isError` and `req.langdetect.errors` will be filled.

`req.langdetect.errors` is an object with optional fields `list`, `mycookie` and `find` with error details;

### Options
`opts` parameter here is optional. Now it should be an object with following fields (all optional):

- `server` - http-langdetect API server,
- `clientOptions` - node-http-langdetect constructor options,
- `list` - add list of user-relevant languages to `req.langdetect.list` object,
- `availableLanguages` - see below,
- `defaultLanguage` - default service language.
- `fallbackLanguage` - this language is returned in case of errors if `defaultLanguage` is not set.
    It should be an object with language `id` and `name`. Default: `{id: "ru", name: "Ru"}`.
    You may set `fallbackLanguage` to `false` if you don't need any fallback value at all. If fallback is used,
    `req.langdetect.fallbackId` or\and `req.langdetect.fallbackList` will be filled.



`availableLanguages` can be one of the following:

- `string`, that contains all language codes (ids) split with ',' sign (i.e. 'en,ru,tr');
- `Array`, that contains language codes, that is joined using ',' to get a string described above;
- `Object`, that has service TLDs as keys and arrays or strings in format described above;
- `Function`, that accepts express request object and should return any of the above.

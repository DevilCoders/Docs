# node-http-langdetect
Simple node.js client for [http-langdetect](https://github.yandex-team.ru/project-stub/http-langdetect)

## Install
`npm install node-http-langdetect` should be enough.

## Usage
```
var HttpLangdetect = require('node-http-langdetect').HttpLangdetect;

var detector = new HttpLangdetect(server, opts);
detector.find({accept_language: 'us', host: 'yandex.ru'}).then(function (lang) {
    console.log(lang);
});
```

## API
- `HttpLangdetect(server, [opts])` - client instance constructor
    - `server {string|Object}` is http-langdetect API server.
    You may provide a string in format `[protocol://]host[:port]` or an object with both `host` and `port` fields.
    - `opts {Object}` is an object that may contain any [got](https://github.com/sindresorhus/got) option to modify http(s) requests behaviour.

- HttpLangdetect.prototype has all the original http-langdetect api methods. Methods are mapped 'as is', they
accept object with parameters and return a Promise that resolves to object with returned values. The only noticeable
difference here is that `HttpLangdetect.prototype` methods use camelCase method names unstead of the_underscored_one, i.e.
`/v0/find_domain` of http-langdetect turns to `HttpLangdetect.prototype.findDomain`. So, please consult with
http-langdetect documentation to find out method parameters and return values.

Currently supported methods are: `find`, `findWithoutDomain`, `findDomainEx`, `findDomain`, `list`, `getInfo`.

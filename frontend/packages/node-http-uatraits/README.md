# node-http-uatraits
Node.js client for [http-uatraits](https://github.yandex-team.ru/project-stub/http-uatraits)

It is actually a simple wrapper for http-uatraits HTTP JSON API.

## Installation
`npm install node-http-uatraits`

## API
Module exports a single constructor `HttpUatraits(api, [options])`.
Arguments: `api` is api server address (i.e. 'http://uatraits.qloud.yandex.ru'),
`options` may contain any option supported by [got](https://github.com/sindresorhus/got) library.

The only method so far is `detect(ua)`.
It expects either a user-agent string or headers object (name: value).
Header names are case insensitive.

## Example
```
var HttpUatraits = require('./').HttpUatraits;
// Let's use test instance
var uatraits = new HttpUatraits('http://uatraits.qloud.yandex.ru');
uatraits.detect(
    'Mozilla/5.0 (Windows NT 6.1; WOW64; rv:40.0) Gecko/20100101 Firefox/40.1'
).then(function (traits) {
    assert.equal(traits.OSName, 'Windows 7');
    assert.equal(traits.BrowserName, 'Firefox');
});
```

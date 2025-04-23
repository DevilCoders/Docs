# @yandex-int/express-http-uatraits

Express middleware for [@yandex-int/node-http-uatraits][arc-node-http-uatraits].

Designed as a 'drop in' replacement for [@yandex-int/express-uatraits][arc-express-uatraits].

## How to use
Install: `npm install @yandex-int/express-http-uatraits`

Usage:
```
app.use(require('@yandex-int/express-http-uatraits')(opts));
app.get('/', function (req, res) {
   console.log(req.uatraits);
});
```

### Options
`opts` parameter here is optional.
Now it should be an object with following fields (all optional):

- `server` - http-uatraits API server,
- `clientOptions` - http-uatraits constructor options

**Note**
If library-server answers bad (bad request, timeout, etc.), `req.uatraits`
will be filled by [@yandex-int/yandex-useragent][arc-yandex-useragent].
And `req.uatraits.fallback` will be set as `true`. Details of error
will be set at field `req.uatraits.error`.

[arc-express-uatraits]: https://a.yandex-team.ru/arc_vcs/frontend/packages/express-uatraits
[arc-node-http-uatraits]: https://a.yandex-team.ru/arc_vcs/frontend/packages/node-http-uatraits
[arc-yandex-useragent]: https://a.yandex-team.ru/arc_vcs/frontend/packages/yandex-useragent

## Maintenance
Make sure that installed dependencies follow company current regulations on them.

Following npm scripts are included for it this process eaiser:
```
npm run dependencies:direct
# examine result-direct.sh and then run it
grep -v '^#' -B 3 result-direct.sh
sh result-direct.sh

npm run dependencies:indirect
# examine result-all.sh and then run it
grep -v '^#' -B 3 result-all.sh
sh result-all.sh

npm run dependencies:indirect
# examine result-all.sh so there is nothing to do anymore
grep -v '^#' -B 3 result-all.sh
```

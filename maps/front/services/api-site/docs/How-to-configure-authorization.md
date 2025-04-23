## How to configure authorization
### 1. Configuration
In order to configure authorization for your project you need to create three different secrets. Go to the
[resources tab in ABC](https://abc.yandex-team.ru/services/maps-front-api-site/resources/) and create
three new TVM resources named
- `maps-front-api-site-prod`
- `maps-front-api-site-test`
- `maps-front-api-site-dev`

The secrets content is located by [Vault](https://vault.yandex-team.ru/) links contained in
`maps-front-api-site-prod` and `maps-front-api-site-test` resources you have just created.

Now comes the last but not the least. To be able to communicate with Blackbox you need to request grants.
This can be done via [form](https://forms.yandex-team.ru/surveys/4901/).

The last resource `maps-front-api-site-dev` is used for authorization in developing mode. The point is that
when you run `make dev` the TVM daemon is trying to start. It listens locally on 8081 port and responses with
tickets for services specified in `.tvm.json` configuration file. By default the daemon is configured to obtain only
a ticket for Blackbox.

Local TVM daemon needs correct configuration file to successfully start, to configure it properly you need to provide
two parameters: `secret` and `self_tvm_id`. The `secret` is exactly the secret contained in
`maps-front-api-site-dev` resource and `self_tvm_id` is its id.

### 2. Authorization schema
The TVM tickets are obtained in `/server/middlewares/tvm-middleware.ts`, they are then used in
`/server/middlewares/blackbox-middleware.ts` to access Blackbox and put user ticket inside of `Request` object.
The validation is located in `/server/middlewares/auth-middleware.ts`, it calls `next()` if user ticket
is successfully obtained from Blackbox and redirects to Passport otherwise.

You may develop without authorization configured, for this purpose you just need to temporarily comment out or
completely remove the following strings in `app.ts`:
```javascript
// import authMiddleware from './middlewares/auth-middleware';

const app = express()
    // .use(authMiddleware)
```

### 3. Useful links
- [Tvm-daemon wiki page](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/tvm-getting-started/).
- [Blackbox telegram-chat](https://t.me/joinchat/BfrKfRJHbU1vrrsfxUwLWQ)
- [The list of Blackbox ids](https://wiki.yandex-team.ru/passport/tvm2/user-ticket/#0-opredeljaemsjasokruzhenijami)

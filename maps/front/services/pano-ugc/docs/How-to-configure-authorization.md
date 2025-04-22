## How to configure authorization
### 1. Current authorization schema
When you run `make dev` the TVM daemon is trying to start. It listens locally on 8081 port and responses with
tickets for services specified in `.tvm.json` configuration file. By default the daemon is configured to obtain only
a ticket for Blackbox.

The TVM tickets are obtained in `/server/middlewares/tvm-middleware.ts`, they are then used in
`/server/middlewares/blackbox-middleware.ts` to access Blackbox and put user ticket inside of `Request` object.
The validation is located in `/server/middlewares/auth-middleware.ts`, it calls `next()` if user ticket
is successfully obtained from Blackbox and redirects to Passport otherwise.

### 2. Configuration 
The TVM daemon needs correct configuration file to successfully start, to configure it properly you need to provide 
two parameters: `secret` and `self_tvm_id`. The detailed instruction on how to obtain these parameters is located at
[tvm-daemon wiki page](https://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/tvm-getting-started/).

You may develop without authorization configured, for this purpose you just need to temporarily comment out or
completely remove the following strings in `app.ts`:
```javascript
// import tvmMiddleware from './middlewares/tvm-middleware';
// import blackboxMiddleware from './middlewares/blackbox-middleware';
// import authMiddleware from './middlewares/auth-middleware';

const app = express()
    // .use(tvmMiddleware)
    // .use(blackboxMiddleware)
    // .use(authMiddleware)
```

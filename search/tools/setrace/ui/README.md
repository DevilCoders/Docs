# Setrace UI

Relatively new UI of Setrace (2019)


## Run locally

To run UI on your machine, you should follow these steps:

1. Install the dependencies:
```bash
npm ci
```

2. Build the package:
```bash
npm run build              # development
npm run build_production   # production
```

3. Run the server:
```bash
npm start
```

After the first start, you can just use `npm start` (unless you want to add a dependency, of course)


## Configuration

### Server

The server starts on `http://localhost:8000` by default (see `.config/main.js`). You can configure it by setting environment variables `WEBPACK_HOST` and `WEBPACK_PORT`


### Proxy

The server uses a proxy to redirect requests to the backend. It can be configured with variables `SETRACE_PROXY_SCHEME`, `SETRACE_PROXY_HOST`, `SETRACE_PROXY_PORT`


## Known issues

### It's not installing / building, what can I do?!

- Make sure that your npm is configured properly: [npm docs](https://doc.yandex-team.ru/si-infra/npm/npm.html)
- If your NodeJS or npm are too new, downgrade them. I can confirm that it's possible to successfully use UI with `node 10.13.0` and `npm 6.4.1`
- If they're too old, upgrade them. Yep, it's a guessing game
- There are no known cases but check your network macro. It may be `_GENCFG_SETRACE_` causing the problem


### It's not tracing, what can I do?!

Chances are your proxy settings are incorrect.

If you're using `_GENCFG_SETRACE_`, it may be an access issue. Try to run the backend on your machine and reconfigure the proxy.

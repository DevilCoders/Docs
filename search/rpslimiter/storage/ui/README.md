# RPS Limiter UI


## Run

Follow these steps to run UI on your machine:

1. Install the dependencies:
```bash
npm ci
```

2. Build the package:
```bash
npm run build
```

3. Run the server:
```bash
npm start
```


## Configuration

### Server

The server starts on `http://localhost:8000` by default (see `.config/main.js`). You can configure it by setting environment variables `WEBPACK_HOST` and `WEBPACK_PORT`


### Proxy

The server uses a proxy to redirect requests to the backend. It can be configured with variables `RPSLIMITER_PROXY_SCHEME`, `RPSLIMITER_PROXY_HOST`, `RPSLIMITER_PROXY_PORT`


## How to fix problems

- Make sure that your npm is configured properly: [npm docs](https://doc.yandex-team.ru/si-infra/npm/npm.html)
- Adjust versions of your NodeJS and npm
- If you have problems with installation of `@fortawesome`, you may need a token (we are using pro icons, yay). You can get it [here](https://yav.yandex-team.ru/edit/secret/sec-01f4f0n9njje4g23dsfptqewf5/explore/versions).\
  After that, append these lines to your `.npmrc` (`<FONTAWESOME_TOKEN>` is said token):
```
@fortawesome:registry=https://npm.fontawesome.com/
//npm.fontawesome.com/:_authToken=<FONTAWESOME_TOKEN>
```

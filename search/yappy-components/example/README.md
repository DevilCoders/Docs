## YAPPY UI


#### Building from source
1. Fetch sources

```bash
git clone https://github.yandex-team.ru/YAPPY/UI.git yappy-ui
cd yappy-ui
```

2. Install dependencies 

```bash
npm install
```

3. [Launch YAPPY model and proxy services](https://wiki.yandex-team.ru/jandekspoisk/sepe/yappy/howto/dev/local/)

4. Run tests
```bash
YAPPY_PROXY_HOST="localhost" YAPPY_PROXY_PORT=8888 npm test
```

5. Run build

```bash
npm run build             # development
npm run build_production  # production
```


#### Using `webpack-dev-server`
```bash
YAPPY_PROXY_HOST="localhost" YAPPY_PROXY_PORT=8888 npm start  # starts on http://localhost:8000
```
Dev-server host and port can be changed via:
 * `.config/main.js`
 * environment variables (`WEBPACK_HOST`, `WEBPACK_PORT`)


#### Documentation
To generate docs from source run `npm run build_docs` and open resulting `doc/index.html`.

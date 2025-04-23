[![Build Status](https://drone.yandex-team.ru/api/badges/project-stub/express-national-redirect2/status.svg)](https://drone.yandex-team.ru/project-stub/express-national-redirect2)

# express-national-redirect2
National redirect middleware, uses all new and shiny cloud services.

This middleware detects correct domain (TLD) for a visitor using his geo location, language and supported TLDs.
If such domain exists and differs from current (the one visitor has come first), it performs automatic redirect.

## Install
`npm install express-national-redirect2`

## Usage
```
app.use(require('express-national-redirect2')(opts));
```

Opts parameter is optional, it is an object with following fields:
- app.domains {Array} - list of TLDs supported by current application,
- [langdetect.server] {string|Object} - [http-langdetect](https://github.yandex-team.ru/project-stub/http-langdetect) API server,
- [langdetect.clientOptions] {Object} - [node-http-langdetect](https://github.yandex-team.ru/project-stub/node-http-langdetect) options.

# secrets-to-dotenv

Библиотека для формирования `.env` файла с секретами,
полученными из [секретницы](https://yav.yandex-team.ru).

## Установка

```
$ npm install --registry=https://npm.yandex-team.ru @vertis/secrets-to-dotenv
```

## Использование

В корне проекта создать `secrets.config.js` или `secrets.config.json`.
```
{
    "MY_SECRET": 'secret_id:secret_version:secret_key'
}
```

Вызываем
```
const secretsToDotenv = require('secrets-to-dotenv');

await secretsToDotenv();
```

или
```
./node_modules/.bin/secrets-to-dotenv
```

## Опции

**configPath**

Тип: `String`

Дефолт: `path.join(process.cwd(), 'secrets.config')`

Путь до файла с описанием секретов.

```
require('secrets-to-dotenv')({ configPath: '/some/path/secrets.json' })
```

или

```
SECRETS_CONFIG_PATH=/some/path/secrets.json ./node_modules/.bin/secrets-to-dotenv
```

**envPath**

Тип: `String`

Дефолт: `path.join(process.cwd(), '.env')`

Путь до файла `.env`

```
require('secrets-to-dotenv')({ envPath: '/some/path/.env' })
```

или

```
SECRETS_ENV_PATH=/some/path/.env ./node_modules/.bin/secrets-to-dotenv
```

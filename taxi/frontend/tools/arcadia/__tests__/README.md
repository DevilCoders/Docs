# Тестирование локально

Чтобы не ждать сборок и не плодить пул-реквестов, сборки можно проверять локально. Для этого нужно зайти в тест-кейс и рядом с файлом `index.ts` положить файл `.env.arcadia.test` с необходимыми параметрами.

Дальше запускаете команду `npm run arc:tests:run -- testPath=<path>`, где path — это путь от папки `__tests__` до кейса. Например, вот такой путь будет валидный для кейса: `testPath=checker/oneService`.

## Запуск чекера
В файл `.env.arcadia.test` можно положить следующее и запустить:
```dotenv
CHANGED_PROJECTS="services/hiring-frontend-dev-api"
BUILD_BRANCH=
VERSION=
DEPLOY_BRANCH=unstable
```

## Запуск сборки unstable
С unstable вам могут понадобиться токены бота от s3, и docker, чтобы производить операции записи. Если вам это не нужно, то не добавляйте их в дотенв, нужные шаги корректно отвалятся. Описание всех аргументов описано в файле `utils/ci/envs`.

В файл `.env.arcadia.test` можно положить следующее и запустить:
```dotenv
CHANGED_PROJECTS="services/hiring-frontend-dev-api"
BUILD_BRANCH=
VERSION=
DEPLOY_BRANCH=unstable
MAC=1
MOCK=1
```

Сборки custom testing и production запускаются по тому же принципу.
```dotenv
BUILD_BRANCH=hiring-frontend-dev-api
VERSION=0.0.1234
DEPLOY_BRANCH=testing
YAV_TOKEN=
CLOWNDUCTOR_TOKEN=
MOCK=1
```

```dotenv
BUILD_BRANCH=hiring-frontend-dev-api
VERSION=0.0.1234
DEPLOY_BRANCH=production
YAV_TOKEN=
CLOWNDUCTOR_TOKEN=
RELEASE_TICKET=
MOCK=1
```

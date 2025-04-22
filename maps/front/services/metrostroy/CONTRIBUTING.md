# Contribution Guide

## Dependencies
To run the application you will need:
* `make` - usually comes with your OS dev-tools
* `node` - https://nodejs.org/en/download/
* `npm` - comes with `node`
* `docker` - https://docs.docker.com/install/
* `docker-compose` - for macOS comes with `docker`, for other checkout https://docs.docker.com/compose/install/

All the other project dependencies are installed using npm:
```
npm i
```

## Running a Local DB
A local database will be started for you when you type:
```
make db-start
```

This target takes up the stdio of the current terminal, therefore you will need another terminal to run the app in dev mode

## Running in Development Mode

Just run
```
make dev
```
This command will start the ts compiler in watch mode and the node.js application in watch mode

## Окружения и наборы схем
Есть два окружения метростроя:
- production: https://metrostroy.c.maps.yandex-team.ru — сохраняет данные в продакшеновый S3
  (http://metrokit-bundles.s3.mds.yandex.net)
- testing: https://metrostroy.tst.c.maps.yandex-team.ru — сохраняет данные в тестовый S3 (http://metrokit-bundles.s3.
  mdst.yandex.net)

Внутри каждого окружения генерятся по два testing/production-файла, которые доступны на
testing/production-хостах сервисов-потребителей.

Например, в production-окружении Метростроя схемы делятся на две группы:
- http://metrokit-bundles.s3.mds.yandex.net/list-production.json — этот файл доступен для https://yаndex.ru/metro
- http://metrokit-bundles.s3.mds.yandex.net/list-testing.json — этот файл доступен для https://l7test.yandex.ru/metro

В testing-окружении Метростроя так же генерятся похожие файлы:
- http://metrokit-bundles.s3.mdst.yandex.net/list-testing.json
- http://metrokit-bundles.s3.mdst.yandex.net/list-production.json

Но эти два файла не используются в клиентах-потребителях, нужны только для разработки Метростроя.

## Codestyle
See [Yandex Maps codestyle](https://github.com/ymaps/codestyle).

* `eslint` - linter for .js, .jsx files
* `tslint` - linter for .ts, .tsx files
* `stylelint` - linter for stylesheets
* `stylint` - linter for .styl files https://github.com/SimenB/stylint

```
make lint
```

## Releasing to Platform
If the tests and linters pass you and you want to deploy your changes you should first bump the current version:
```
make patch
```
Will bump the patch version of the application. Use patch only when you're fixing bugs, improving performance, refactoring and making
small  changes to the UI.

If you've extended the HTTP API, added new features or substaintaly changed the UI, you should bump the minor version - `make minor`.

When you've bumped the version, you can now build and deploy the app to testing:
```
make release-testing
```

Don't forget to merge the version to trunk:
```
arc pr create --push --no-edit --publish
```
This will create a PR in Arcanum and you will need to merge it.

## Applying DB Migrations in Testing or Production

You will need access to the `yav` entries of the application:
- testing - https://yav.yandex-team.ru/secret/sec-01cr5wcqwn8rz1et4h9f9sep6r
- production - https://yav.yandex-team.ru/secret/sec-01crtdm7fw5sxjksz74pn1522y

To run the migrations to the latest available version use the command:
1. Run the migration in dry-run mode (runs all the migration files and even if it finishes successfully rollsback your changes).
```
 make db-migrate POSTGRES_PASSWORD="<the dbUserPassword field from the secret>" MAPS_STAGE="<testing or production>"
```
2. If everything is OK and the dry-run finishes without any errors, apply the transactions:
```
 make db-migrate POSTGRES_PASSWORD="<the dbUserPassword field from the secret>" MAPS_STAGE="<testing or production>" PGMIGRATE_DRYRUN=0
```

**Important**: Be careful when entering the passwords in the terminal: they will be stored in the history of your terminal.
To avoid this add a space char before `make` to tell your terminal not to store it.

## Hash Salt

Hash salts can be generated with a simple oneliner:
```
node -p "crypto.createHash('sha256').update(Date.now().toString()).update(Math.random().toFixed(32)).digest('hex')"
```

## Updating Test Fixtures

If you're augmenting or extending any of the interfaces, you will probably encounter failing tests. To fix them you will need to update
test's fixtures. Simply run:
```
make fixtures-for-tests
```

This will rewrite some of the files in `resources/test-fixtures`. Examine the diff, if it contains changes that you expect, commit it.

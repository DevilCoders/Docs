# Сборка сервиса монорепы

## Сборка продовой версии сервиса в докере локально

```bash
# <buildType>: stable | unstable — тип сборки в ТС
# <rtcType>: production | testing — тип окружения в няне
# <serviceName>: string — имя папки (например, даже для ln: frontend-dev-api-bot)
# <tag>: string — версия (major.minor.patch)
$ npm run monorepo:service:<buildType>:<rtcType> -- <serviceName> <tag>

# соберётся stable сборка в production окружение няни
$ npm run monorepo:service:stable:production -- frontend-dev-api-bot 0.0.1
```

### Для продакшн окружения в облаке продовой сборки

```bash
# Собираем базовый образ

# $ npm run monorepo:compile-dockerfile:step-build -- --service=<service-name> # собираем докерфайл вашего сервиса
$ npm run monorepo:compile-dockerfile:step-build -- --service=frontend-dev-api-bot
# $ npm run monorepo:service:build:base -- --service=<service-name> --tag=<version> --buildType=<type> # пример ниже, type: stable | unstable
$ npm run monorepo:service:build:base -- --service=frontend-dev-api-bot --tag=0.0.1 --buildType=stable

# Собираем продовый образ, в который кладём сборку сервиса из шагов выше

# $ npm run monorepo:compile-dockerfile:step-production -- --service=<service-name> # собираем продовую версию
$ npm run monorepo:compile-dockerfile:step-production -- --service=frontend-dev-api-bot
# $ npm run monorepo:service:build:production -- --service=<service-name> --tag=<version> --buildType=<type> # пример ниже, type: stable | unstable
$ npm run monorepo:service:build:production -- --service=frontend-dev-api-bot --tag=0.0.1 --buildType=stable
```

### Для тестинг окружения в облаке продовой сборки
```bash
$ npm run monorepo:compile-dockerfile:step-build -- --service=frontend-dev-api-bot
$ npm run monorepo:service:build:base -- --service=frontend-dev-api-bot --tag=0.0.1 --buildType=stable

$ npm run monorepo:compile-dockerfile:step-testing -- --service=frontend-dev-api-bot
$ npm run monorepo:service:build:testing -- --service=frontend-dev-api-bot --tag=0.0.1 --buildType=stable
```

## Сборка unstable версии сервиса в докере локально

```bash
$ npm run monorepo:compile-dockerfile:step-build -- --service=frontend-dev-api-bot
$ npm run monorepo:service:build:base -- --service=frontend-dev-api-bot --tag=0.0.1 --buildType=unstable

$ npm run monorepo:compile-dockerfile:step-testing -- --service=frontend-dev-api-bot
$ npm run monorepo:service:build:testing -- --service=frontend-dev-api-bot --tag=0.0.1 --buildType=unstable
```

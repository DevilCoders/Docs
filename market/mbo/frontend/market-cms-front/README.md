# Market Cms Front

[![oko](https://badger.yandex-team.ru/oko/repo/market-java/market-cms-front/health.svg)](https://oko.yandex-team.ru/repo/market-java/market-cms-front)

## Разработка

### Запуск проекта

При первом запуске приложения, в файл `/etc/hosts` необходимо добавить следующие записи (это необходимо сделать только один раз):

```
127.0.0.1   localhost.msup.yandex-team.ru
127.0.0.1   localhost.msup.yandex.ru
```

Далее устанавливаем зависимости:

```bash
npm ci
```

Запускаем приложение:

```bash
npm start
```

Проект становится доступен по адресу: [https://localhost.msup.yandex.ru:3443/](https://localhost.msup.yandex.ru:3443/)

### Запуск тестов

```bash
npm test
```

### Сборка

Сборка для production

```bash
npm run build:prod
```

Сборка для testing

```bash
npm run build:testing
```

### Дополнительные команды

```bash
# Запуск eslint
npm run lint

# Запуск eslint c fix
npm run lint:fix
```

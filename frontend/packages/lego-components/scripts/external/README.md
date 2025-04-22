# Публикация во внешний мир

Публикация работает в ручном режиме и делится на несколько этапов.

## Публикация пакета во внешний npm

Для того, чтобы иметь возможность опубликовать пакет, у вас должен быть доступ в [yandex](https://www.npmjs.com/org/yandex) организацию.

1. Запускаем скрипт подготовки из корня пакета:

```sh
node ./scripts/external/prepare-external-npm.js
```

2. Публикуем пакет:

```sh
npm publish
```

## Публикация storybook в s3

1. Запускаем скрипт подготовки из корня пакета:

```sh
EXTERNAL=1 node ./scripts/external/prepare-external-storybook.js
```

2. Собираем проект:

```sh
storybook-showcase build
```

3. Загружаем в s3:

> Необходимые ключи можно найти в [yav](https://nda.ya.ru/3UWXvQ).

```sh
FRONTEND_S3_ACCESS_KEY_ID=<KEY> FRONTEND_S3_SECRET_ACCESS_KEY=<KEY> YENV=production static-uploader
```

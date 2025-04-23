# Разработка

## Шаг 1. Установка

```
npm i
```

## ШАГ 2. Генерим env-переменные

Делаем один раз, чтобы загрузить секреты. В корне проекта сформируется .env файл.

```
npm run dev:dotenv
```

## ШАГ 3. Запуск

Далее запускаем приложение

```
npm run dev
```

Приложение будет доступно по тунеллеру.

## Storybook 6

```
npm run storybook:start
```

# Справка

## ENV

Для генерации env-переменных используется библиотека [make-my-env](https://a.yandex-team.ru/arc/trunk/arcadia/frontend/packages/make-my-env).

Конфиг лежит [тут](../.config/env/index.yml).

## TVM

Для локальной разработки используется tvm-демон. Он устанавливается в dev-зависимостях.

Конфиг локального tvm демона лежит [тут](../.tvm.test.json).

Подробнее про tvmtool-bin почитать [тут](ttps://wiki.yandex-team.ru/passport/tvm2/tvm-daemon/).

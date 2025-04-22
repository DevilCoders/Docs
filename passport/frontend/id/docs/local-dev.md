## Разработка в монорепо

### Установка зависимостей
1. Установить зависимости в корне монорепы `npm ci`.
2. Перейти в нужный сервис или пакет и запустить `npm ci` там.

При необходимости можно слинковать необходимые пакеты. Для этого в корне монорепы вызвать
```bash
npx lerna bootstrap --scope @yandex-id/components --scope @yandex-id/id
```

Гипотетически с помощью `npm run deps:install:all` должны слинковаться и поставиться все зависимости, но это чаще не работает, чем работает.

### Локальный запуск сервиса

#### Генерация ENV-переменных
```bash
npm run dev:dotenv --prefix=services/id
```

#### Запуск сервиса
```bash
npm start --prefix=services/id
```

Для удобства в корне репозитория будут команды запуска сервиса, например `npm run dev:id`

### Добавление зависимостей

Для добавления зависимости в корень:

```bash
npm i <package>
```

Для добавления зависимости в пакет или сервис:

```bash
# Пакет
npx lerna add <package> --scope @yandex-int/<package>
# Сервис
npx lerna add <package> --scope @yandex-id/<service>
```

> Для добавления зависимости в `devDependencies` нужно использовать аргумент `--dev`.

### Удаление зависимостей

Для удаления зависимости в корне:

```bash
npm rm <package>
```

Для удаления зависимости в пакете или сервисе нужно руками удалить её в `package.json`, а затем выполнить команду:

```bash
npm run deps:uninstall && npm ci && npx lerna bootstrap --no-ci --scope <package_or_service> --include-dependencies
```

### См. также
Документацию на конкретные сервисы и пакеты см. в readme-файлах в соответствующих папках. Например, документация на [сервис id](../services/id/README.md).

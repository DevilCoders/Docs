# <%= projectName %>

## Подготовка окружения

[Как установить brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/)

```
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12.18.1 версии
nvm install 12.18.1

# Устанавливаем зависимости монорепозитория
npm i

# Устанавливаем зависимости сервиса
cd <%= projectName %>
nvm use
npm run deps

```

Добавляем домен для локальной разработки в `/etc/hosts`

```
# <%= projectName %>
127.0.0.1   local.<%= projectName %>.yandex.ru
::1         local.<%= projectName %>.yandex.ru
```

Сохраняем приватный ключ SSL в файл `ssl/private.pem` из [секрета](ссылка на секрет с приватный ключ).

Сохраняем в корень проекта файл [.tvm.json](ссылка на секрет с файлом tvm)`.

Копируем файл `.env.example` в файл `.env`

## Разработка

```bash
# Локальный запуск
npm run dev
```

По-умолчанию сервис становится доступен по адресу: https://local.<%= projectName %>.yandex.ru

### Плагины VSC

- [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
- [StyleLint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
- [PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## Синхронизация переводов

Для загрузки и обновления переводов используется пакет [`tanker-kit`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-kit). Для его работы требуется установить в переменную среды `TANKER_OAUTH_TOKEN`
Для этого:

1. Получаем OAuth-токен: https://nda.ya.ru/3SjQY7
2. Полученное значение копируем в `.env`

```
...
TANKER_OAUTH_TOKEN=xxxx
```

3. Работаем с tanker-kit при помощи команд

```bash

npm run tanker:pull # Выгрузить переводы
npm run tanker:push # Загрузить переводы
```

## Сборка проекта

```
npm run build
```

## Деплой проекта

```
chmod +x ./scripts/deploy.sh
./scripts/deploy.sh
```

# SEOS

## Подготовка окружения

[Как установить brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/)

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12.18.1 версии
nvm install 12.18.1

# Устанавливаем зависимости монорепозитория
npm i

# Устанавливаем зависимости сервиса

cd services/seos
nvm use
npm i
npm run env

```

## Разработка

```bash
# Локальный запуск
npm run dev
```

По-умолчанию сервис становится доступен по адресу: https://seos.local.yandex.ru

### Плагины VSC

-   [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
-   [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
-   [StyleLint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
-   [PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)
-   [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## Синхронизация переводов

Для загрузки и обновления переводов используется пакет [`tanker-kit`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-kit).

Работаем с tanker-kit при помощи команд

```bash
npm run tanker:pull # Выгрузить переводы
npm run tanker:push # Загрузить переводы
```

## Сборка проекта

```
npm run build
```

## Тесты

```bash
npm run test:unit # Unit тесты
```

# Troubleshooting

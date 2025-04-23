# Админка

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
cd services/contest-alcina
nvm use
npm i

```

Добавляем домен для локальной разработки в `/etc/hosts`

```
# Contest
127.0.0.1   local.contest-alcina.yandex.ru
::1         local.contest-alcina.yandex.ru
```

Сохраняем приватный ключ SSL в файл `ssl/private.pem` из [секрета](https://yav.yandex-team.ru/secret/sec-01f78qxeak1gytet6w2cf7t0mm/explore/version/ver-01f78qxebx3g9zze392vj5g5dh).

Сохраняем в корень проекта файл [.tvm.json](https://yav.yandex-team.ru/secret/sec-01f78yahyq7h3vxpyvxe3me4r3/explore/version/ver-01f7913f1b6jttv56feaxnzpk7)`.

Копируем файл `.env.example` в файл `.env`

## Разработка

```bash
# Локальный запуск
npm run dev
```

По-умолчанию сервис становится доступен по адресу: https://local.contest-alcina.yandex.ru

### Плагины VSC

-   [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
-   [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
-   [StyleLint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
-   [PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)
-   [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

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

# Troubleshooting

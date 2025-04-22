# Сайт участника Contest

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
cd services/contest-participant
nvm use
npm run deps

```

Добавляем домен для локальной разработки в `/etc/hosts`

```
# Contest
127.0.0.1   local.contest.yandex.ru
::1         local.contest.yandex.ru
```

Сохраняем приватный ключ SSL в файл `ssl/private.pem` из [секрета](https://yav.yandex-team.ru/secret/sec-01efxjx813dk41j3ynnycf8frt/explore/version/ver-01efxjx92m4r6sd6r8y1bhk82e).

Сохраняем в корень проекта файл [.tvm.json](https://yav.yandex-team.ru/secret/sec-01enn4gzz82nfpc2xzccgkx6et/explore/version/ver-01enn4h01qsrtpdej88f21qjrc)`.

Копируем файл `.env.example` в файл `.env`

## Разработка

```bash
# Локальный запуск
npm run dev
```

## Storybook

Запуск:

```bash
npm run storybook
```

По-умолчанию сервис становится доступен по адресу: https://local.contest.yandex.ru

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

## Тесты

```bash
npm run test:unit # Unit тесты
npm run test:storybook # Hermione тесты на сторибуке
```

# Troubleshooting

# Контест Интервью

Сервис выгрузки результатов интервью

## Установка

[Как установить brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/)

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12 версии
nvm install 12

# Устанавливаем зависимости монорепозитория
cd frontend
npm i

# Устанавливаем зависимости сервиса
cd services/contest-interview
nvm use
npm run deps

# Задаём переменную окружения для локальной разработки
export NODE_ENV=development
```

Добавляем домен для локальной разработки в `/etc/hosts`

```
# Contest
127.0.0.1   local.contest-interview.yandex-team.ru
::1         local.contest-interview.yandex-team.ru
```

Сохраняем ключи SSL в файлы `ssl/certificate.pem` и `ssl/private_key.pem` из [секрета](https://yav.yandex-team.ru/secret/sec-01eff1zya92qyemhqqv5h2ga36/).

Сохраняем в корень проекта файл `.tvm.json` и в поле `secret` подставляем значение [из секрета](https://yav.yandex-team.ru/secret/sec-01efex23v1pnf3vb94b3cta0k8).

```json
{
  "BbEnvType": 1,
  "clients": {
    "contest-interview": {
      "secret": "xxxx",
      "self_tvm_id": 2021772,
      "dsts": {
        "blackbox": {
          "dst_id": 223
        }
      }
    }
  }
}
```

Также для разработки потребуются токены:

- [CONTEST_API_TOKEN](https://yav.yandex-team.ru/secret/sec-01efkwy4xm7ewheb4amyrz5xgv)

## Разработка

```bash
# Локальный запуск
npm run dev
```

Сервис становится доступен по адресу: https://local.contest-interview.yandex-team.ru

### Плагины VSC

- [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
- [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
- [StyleLint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
- [PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## Синхронизация переводов

Для загрузки и обновления переводов используется пакет [`tanker-kit`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-kit). Для его работы требуется установить в переменную OAuth-токен: https://nda.ya.ru/3SjQY7

```bash
export TANKER_OAUTH_TOKEN=xxxx;

npm run tanker:pull # Выгрузить переводы
npm run tanker:push # Загрузить переводы
```

## Документация

Актуальная информация по проекту [находится на wiki](https://wiki.yandex-team.ru/next-template/docs/)

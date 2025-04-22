# Лендинг Yango Deli

## О проекте

### Окружения

- Production\
  https://deli.yango.com ⋅ https://yango-deli-website.lavka.yandex.net

- Testing\
  https://yango-deli-website.lavka.tst.yandex.net

- Unstable\
  http://yango-deli-website.lavka.dev.yandex.net

- Local\
  https://yango-deli-website.lavka.local.yandex.net:3000

### Инфра

- [ABC группа](https://abc.yandex-team.ru/services/lavkayangodeliwebsite/)
- [Сервис в tariff-editor](https://tariff-editor.taxi.yandex-team.ru/services/35/edit/355554/info)
- [Проект в танкере](https://tanker-beta.yandex-team.ru/project/yango-deli-website)
- [Проект в бункере](https://bunker.yandex-team.ru/yango-deli-website)
- [RUM](https://rum.yandex-team.ru/projects/yango-deli-website)
- [Error-booster](https://error.yandex-team.ru/projects/yango-deli-website)

### Дизайн

- [Yango Deli Landing](https://www.figma.com/file/tgL1Ju5Mzt8bGlrVfZxMkA/Deli?node-id=8%3A11294)
- [Yango Text Style sheet](https://www.figma.com/file/gfkNc7mSgvM2dWim0nBlS1/Yango-text-style-sheet)
- [Yango Deli Images](https://www.figma.com/file/f1l3H6C5iLTdDqiI1EV5jO/Yango-Deli-Images)


## Quick Start

Для работы с проектом потребуются

- [nvm](https://github.com/nvm-sh/nvm)
- node и npm

Чтобы запустить проект локально

- Клонируем репозиторий и переходим в директорию с проектом
  ```bash
  git clone git@github.yandex-team.ru:taxi/frontend-monorepo.git
  cd frontend-monorepo/services/lavka-yango-deli-website
  ```

- Добавляем локальный домен в `/etc/hosts`
  ```bash
  echo '127.0.0.1 yango-deli-website.lavka.local.yandex.net' | sudo tee -a /etc/hosts
  ```

- Устанавливаем необходимую версию node.js через nvm
  ```bash
  nvm install && nvm use
  ```

- Получаем OAuth токен для танкера по [ссылке](https://nda.ya.ru/3SjQY7) и записываем его в `.dev/tanker.token`
  ```bash
  echo -n "Ваш токен" > ./.dev/tanker.token
  ```

- Запускаем скрипт установки
  ```bash
  make setup
  ```

- Запускаем приложение
  ```bash
  make dev
  ```


## Сценарии

- Запустить в _hot reload_ режиме
  ```bash
  HOT_RELOAD=1 make dev
  ```

- Синхронизировать переводы между проектом и танкером
  ```bash
  make tanker-sync
  ```

## Инструкции

- [Обновить изображения](docs)

Фикс проблем линтера:
```bash
npx stylelint "**/*.css" --fix
```

## Troubleshooting

- > У меня в `/etc/hosts` уже присвоен домен для 127.0.0.1, что делать?

  В этом случае необходимо сделать IP алиас с помощью команды:
  ```bash
  sudo ifconfig lo0 alias 127.0.0.2
  ```

  И запускать приложение с переменной окружения `HOSTNAME`
  ```bash
  HOSTNAME=127.0.0.2 make dev
  ```


## Полезные ссылки

- Флоу разработки в монорепе\
  https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/development-flow/

- Как сделать релиз\
  https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/release/

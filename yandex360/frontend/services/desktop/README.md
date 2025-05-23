# Suluguni

Десктоп-клиент Яндекс.Почты

# Разработка

- `npm run dev` — собрать и запустить приложение
- `npm start` — то же, что `dev`, но с линтером
- `npm run lint:fix` — попытаться автоматически исправить ошибки линтера

## Связь с тач-стендом

По умолчанию приложение смотрит на продный хост сулугуни. Можно:

- Использовать более свежий QA-стенд: `NODE_ENV=qa npm run dev`
- Указать любой другой стенд: `YAMAIL_DESKTOP_HOST=vklepov.mailfront4.yandex.ru npm run dev`

После переключения между корпом и не-корпом нужно разлогиниться через верхнее меню приложения.

# Сборка

1. Делаем `npm version patch`, чтобы версии сборок различались, __но__ один раз для сборок одной версии под разные платформы.
2. Собираем через `npm run package:mac:qa`, `npm run package:win:qa`.
3. Сборка выплёвывается в `./dist`.
4. Выполняем  команду `npm run publish:qa`, которая заливает файлы из `./dist` на mdst через s3, файлы будут доступны по ссылке вида `https://desktop.s3.mdst.yandex.net/<filename>`. Для того чтобы все это заработало надо поставить и настроить [aws](https://wiki.yandex-team.ru/mds/s3-api/s3-clients/#awscommandlineinterface).

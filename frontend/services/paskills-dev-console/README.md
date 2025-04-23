# Фронтенд платформы скиллов

## Пререквизиты

-   Node.js

## Сборка

Выполнить следующую команду

```
make build
```

## Разработка и запуск

Выполнить следующие команды.

```
1. npm install
2. make watch
3. npm run dev
```

```
Команды 2 и 3 нужно выполнить параллельно в разных вкладках терминала
```

### stable

-   [Сервис](https://dialogs.yandex.ru/developer)

### I18N

Переводы хранятся в [танкере](https://tanker-beta.yandex-team.ru/project/paskills-dev-console).
Чтобы скачать свежие переводы в код, нужно [получить токен](https://nda.ya.ru/3SjQY7) и сохранить его в .tanker/token.json в кавычках.
Команда скачивания переводов:
```
npx tanker pull
```

Переводы хранятся в src/i18n. Для использования в коде используется [пакет i18n](https://a.yandex-team.ru/arc_vcs/frontend/packages/i18n).

### Как запустить консоль, которая ходит в приемку
#### Почему нельзя просто переопределить хост апи?
Приемочное окружение апи ходит в продовый блекбокс, поэтому и консоли надо ходить в него же, но да него доступа с локальной машины нет, поэтому тунель.


После npm install выполнить скрипть `scripts/patch-blackbox.js`
Далее нужно взять приемочный ssh хост консоли, например `root@dev-console.a4unpan2nrdmlmpo.sas.yp-c.yandex.net` и запустить туннель типо такого `ssh -L 9999:localhost:2 -L 8888:blackbox.yandex.net:80 root@dev-console.a4unpan2nrdmlmpo.sas.yp-c.yandex.net`.
Перед запуском `npm run dev` нужно засетапить следующий набор env переменных:
```
export PASKILLS_API_URL=http://paskills-common-testing.alice.yandex.net/priemka/api
export PASSPORT_API=passport.yandex.ru
export BLACKBOX_API=localhost:8888
export PASKILLS_BLACKBOX_API=localhost:8888
export TVMTOOL_LOCAL_AUTHTOKEN=$(ssh root@dev-console.a4unpan2nrdmlmpo.sas.yp-c.yandex.net "echo \$TVMTOOL_LOCAL_AUTHTOKEN")
export PASKILLS_QUASAR_UI_URL=https://yandex.ru/quasar
```
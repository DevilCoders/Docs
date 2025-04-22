i18n-migrator
=============

Утилита для миграции кейсетов на новый формат [i18n]

## Установка

```sh
npm install -g @yandex-int/i18n-migrator --registry=http://npm.yandex-team.ru
```

## Описание

В наличии две команды:

* [Transform](#transform) – для преобразовний между форматами
* [Upload](#upload) – для загрузки ключей на всех языках в [tanker]

Все опции для всех команд можно посмотреть с помощью команды `help`.

```sh
i18n-migrator --help
```

### Transform

Пример работы:

```sh
find adapters -name "adapter-time.priv-i18n" | xargs i18n-migrator transform --move="src/features/Time/Time.i18n"
✔ — Time transformed and moved
````

### Upload

Пример работы:

```sh
i18n-migrator upload  src/features/Time/Time.i18n
ℹ — Time: found locales: [be, en, id, kk, ru, tr, tt, uk, uz]
✔ — Time uploaded
```

[i18n]: https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/i18n#i18n
[tanker]: https://tanker.yandex-team.ru

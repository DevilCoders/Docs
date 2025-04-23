[![oko health](https://oko.yandex-team.ru/badges/repo.svg?repoName=yandex360/frontend/services/webmail-api&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/webmail-api)
[![oko health](https://oko.yandex-team.ru/badges/repoSecurity.svg?repoName=yandex360/frontend/services/webmail-api&vcs=arc)](https://oko.yandex-team.ru/arc/yandex360/frontend/services/webmail-api)

# APIv1/v2
Новый клёвый API

## Запуск dev-версии
```sh
git clone git@github.yandex-team.ru:Daria/api.git
cd api
make
make start
```

## Сборка ресурса с конфигом для облаков
```sh
make upload-settings
```

## Выкатка в Qloud
```sh
npm run deploy 1.2.3 MAILAPI-123
npm run deploy-canary 1.2.3 MAILAPI-123
```

### Cборка

Для сборки нового пакета нужно

```sh
npm run package 1.2.3 MAILAPI-123
# или
npm run package major MAILAPI-123
# или
npm run package minor MAILAPI-123
# или
npm run package patch MAILAPI-123
```

## Структура

В проекте есть два `package.json`, в корне и в папке `server`.
  * `package.json`:
    * `dependencies` — модули необходимые для сборки пакета;
    * `devDependencies` — модули для разработки и тестирования (`nodemon`, `mocha` и т.п.);
    * `optionalDependencies` — не используются;
  * `server/package.json`:
    * `dependencies` — модули для работы приложения в проде.
    * `devDependencies`/`optionalDependencies` — не используются.

### Настройки (`configs/`)
Настройки живут YAML-файлах в папке `configs` и компилируются в файлы
`configs/config.<environment>.json` скриптом `tools/configs.js`.
При изменении YAML-файлов нужно пересобрать настройки командой `make configs`.

### Приложение (`server/`)
Express-приложение. Монтируется на путь `/api/`.

  * `app` — приложение;
  * `middlewares` — глобальные миддлвари, (создание конфига, ядра и т.п.);
  * `lib` — расширение классов Duffman-а;
  * `services`/`models` — сервисы и модели;
  * `routes` — роутер приложения:
    * `v2/*` — ручки APIv2;
    * для APIv3 нужно будет создавать ручки в папке `v3`;
  * `helpers` — разные хелперы.

### Роутер (`server/routers/`)
Настройка роутинга. При установке пакета создаётся симлинк в папке `/etc/duffman/init.d/`.

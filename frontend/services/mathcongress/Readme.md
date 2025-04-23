# Сайт Математического конгресса

## Подготовка окружения

[Как установить brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/)

```
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12 версии
nvm install 12

# Устанавливаем зависимости монорепозитория
npm i

# Устанавливаем зависимости сервиса
cd services/mathcongress
nvm use
npm run deps
```

## Задаём OAuth-секрет:

1. Сначала нужно залогиниться в тестовом паспорте под аккаунтом `yndx-icm-test` (креды [на Вики](https://wiki.yandex-team.ru/bliss/mathcongress/#korporativnyepolzovateli))
2. Затем нужно пройти по ссылке https://oauth-test.yandex.ru/client/e172e17743724a9abc3615cab8df173b
3. Скопировать значение из поля "Пароль"
4. Скопировать файл `.env.example` в `.env` в корне проекта и установить значение переменной окружения `YANDEX_CLIENT_SECRET`

## Задаём OAuth-токен для YQL:

1. Заходим в [секретницу](https://yav.yandex-team.ru/secret/sec-01ew0cqdsnh1c3cr69dkwvxce0/explore/versions)
2. Копируем значение переменной yql_token
3. В файле `.env` устанавливаем значение переменной окружения `YQL_TOKEN`

## Задаём креды для доступа в S3:

1. Заходим в [секретницу](https://yav.yandex-team.ru/secret/sec-01ea8a1cngey078hfxpbr88vn7/explore/versions)
2. Копируем значение переменной s3_access_key и s3_secret_access_key
3. В файле `.env` устанавливаем значение переменной окружения `AWS_ACCESS_KEY_ID` и `AWS_SECRET_ACCESS_KEY`

## Задаём UID для обращения к тестовому бэкенду:

1. Берем любой UID с [wiki](https://wiki.yandex-team.ru/bliss/mathcongress/#korporativnyepolzovateli) страницы проекта (Продовый паспорт - Логины).
2. В файле `.env` устанавливаем значение переменной окружения `UID`

## Добавляем домен для локальной разработки в `/etc/hosts`

```
# Mathcongress
127.0.0.1   local.icm2022.yandex.org
::1         local.icm2022.yandex.org
127.0.0.1   local.icm2022.yandex.ru
::1         local.icm2022.yandex.ru
```

### Добавляем сертификаты

Создаём директорию `ssl/` в корне проекта. В неё сохраняем ключи SSL в файлы `certificate.pem` и `private_key.pem` из [секрета](https://yav.yandex-team.ru/secret/sec-01fgxzkr25f6krwc7bdpzsz4g4/).

### Добавляем конфиг для TVM

Сохраняем в корень проекта файл `.tvm.json`. TVM-секрет получаем [здесь](https://abc.yandex-team.ru/services/mathcongress/resources/?show-resource=18885075) (нужно получить роль TVM менеджера в [ABC](https://abc.yandex-team.ru/services/mathcongress/)).

```(json)
{
  "BbEnvType": 1,
  "clients": {
    "mathcongress": {
      "secret": "XXXX",
      "self_tvm_id": 2020244,
      "dsts": {
        "blackbox": {
          "dst_id": 224
        },
        "api": {
          "dst_id": 2020743
        },
        "mediaplatform": {
          "dst_id": 2009968
        }
      }
    }
  }
}
```

## Разработка

```bash
# Локальный запуск
npm run dev
```

Сервис становится доступен по адресам:

-   https://local.icm2022.yandex.org/account
-   https://local.icm2022.yandex.ru/account

##Сборка

### Testing

Приложение выкатывается **автоматически** в тестовое окружение после успешного merge в `trunk`.
Версия приложения соответствует версии в `package.json`. Она так же изменяется **автоматически** - увеличивается минорная версия ([подробнее о правилах версионирования для `/services/*`](https://a.yandex-team.ru/arc_vcs/frontend/docs/faq/packages-autopublish.md#особенности-версионирования-сервисов--services--4)).

Если возникает необходимость собрать версию вручную (локально), это можно сделать с помощью команды

```
npm run tools:deploy
```

Скрипт подскажет, какие переменные окружения необходимо установить. Все переменные окружения, кроме `VERSION`, хранятся в [секретнице](https://yav.yandex-team.ru/secret/sec-01e8ycm1sh4q6ma7jrejjt7dhr/).

Задать переменные окружения:

```bash
export VERSION=xx.y
```

Собранный образ руками выкатывается в testing через интерфейс YD.

### Production

Выкладка на prod происходит в ручном режиме - через интерфейс YD.

### Плагины VSC

-   [EditorConfig](https://marketplace.visualstudio.com/items?itemName=editorconfig.editorconfig)
-   [Path Intellisense](https://marketplace.visualstudio.com/items?itemName=christian-kohler.path-intellisense)
-   [StyleLint](https://marketplace.visualstudio.com/items?itemName=stylelint.vscode-stylelint)
-   [PostCSS Language Support](https://marketplace.visualstudio.com/items?itemName=csstools.postcss)
-   [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode)

## Синхронизация переводов

Для загрузки и обновления переводов используется пакет [`tanker-kit`](https://github.yandex-team.ru/search-interfaces/frontend/tree/master/packages/tanker-kit). Для его работы требуется установить в переменную OAuth-токен: https://nda.ya.ru/3SjQY7

```bash
export TANKER_OAUTH_TOKEN=xxxx;

npm run tanker:pull # Выгрузить переводы
npm run tanker:push # Загрузить переводы
```

## Design by Contract

Рядом с приложением поднимается DbC-сервер, расположенный в файле `contract-server.ts`. Именно к этому серверу приложение обращается за данными при локальной разработке. Конфигурация обработчиков запросов является контрактом для проектирования бэкенда.

Поднять сервер локально можно при помощи команды `npm run start:contract`, после чего он станет доступен по адресу http://localhost:8080/v1/ping.

## Документация

Актуальная информмация по проекту [находится на wiki](https://wiki.yandex-team.ru/bliss/mathcongress/)

## Troubleshooting

1. Локально не логинит и в консоле `blackbox status: ACCESS_DENIED`
   **Решение**: почисти куки

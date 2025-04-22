# Фронтенд сервиса Автоматизация лендингов парков

## Хосты

[Сервис в Tariff Editor]()

* NGINX - [hiring-parks-landing](/services/hiring-parks-landing/etc/nginx/sites-available/hiring-parks-landing.conf)
* dev - [https://parks-landing.taxi.localhost.yandex.ru:4002](https://parks-landing.taxi.localhost.yandex.ru:4002)
* unstable - [parks-landing.taxi.dev.yandex.ru](https://parks-landing.taxi.dev.yandex.ru)
* testing - [parks-landing.taxi.tst.yandex.ru](https://parks-landing.taxi.tst.yandex.ru)
* stable - [parks-landing.taxi.yandex.ru](https://parks-landing.taxi.yandex.ru)

P.S. prestable не нужен, он не для публичного захода пользователей. Вместо prestable используется testing.

## Конфиги
Cписок стран и городов для лендинга можно изменить в конфиге `HIRING_API_SUGGESTS_ACQUISITION_LANDING_CITIES`:
* [Prod](https://tariff-editor.taxi.yandex-team.ru/dev/configs/edit/HIRING_API_SUGGESTS_ACQUISITION_LANDING_CITIES)
* [Testing](https://tariff-editor.taxi.tst.yandex-team.ru/dev/configs/edit/HIRING_API_SUGGESTS_ACQUISITION_LANDING_CITIES)

## Подготовка
Для работы потребуется Node.js 10.

Для локальной разработки мы используем [NVM](https://github.com/nvm-sh/nvm).

Устанавливаем NVM, а затем:
```bash
# Устанавливаем Node.js 10 версии
nvm install 10

# Переключаемся на эту версию
nvm use 10
```

## Настройка проекта

```bash
# склонировать проект
git clone git@github.yandex-team.ru:taxi/frontend-monorepo.git

# перейти в папку с проектом
cd services/hiring-parks-landing/

# инициализировать проект: установить зависимости и собрать проект
npm run init

# подтянуть файлы локализации
npm run locale:init
```

Далее [нужно скопировать ключ для Sales Force](https://yav.yandex-team.ru/secret/sec-01f91txqz283srpmx8k4gw4q2r/explore/version/ver-01f91txqzjgc1gzc8tv3re8b8m), а затем создать файл окружения `.env` со следующим содержимым:
```
SALESFORCE_TOKEN=<значение_ключа>
```

## Запуск

```bash
npm run dev
```

Смотреть после запуска тут: [https://parks-landing.taxi.localhost.yandex.ru:4002](https://parks-landing.taxi.localhost.yandex.ru:4002/).

## Сборка

- `npm run build:production`

## Релиз

[Как собирать и катить релиз](https://wiki.yandex-team.ru/taxi/efficiency/dev/frontend/rtc/fast-create-service/#razrabotka)

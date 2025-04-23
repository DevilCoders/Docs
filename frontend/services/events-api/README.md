# events-api
[![Build Status](https://drone.yandex-team.ru/api/badges/montserrat/events-api/status.svg)](https://drone.yandex-team.ru/montserrat/events-api) [![OKO health](https://badger.yandex-team.ru/oko/repo/montserrat/events-api/health.svg)](https://oko.yandex-team.ru/repo/montserrat/events-api)

**Бэкенд проекта Events на Node.js**

- [Документация](https://swagger-ui.yandex-team.ru/?url=https://testing.events-api.common.yandex.net/v1/docs)
- Тестинг: https://https://testing.events-api.common.yandex.net/v1/
- Продакшен: https://events-api.common.yandex.net/v1/

### Требования

- Nodejs v8.9.3+
- Postgres v10+

### Быстрый старт

```bash
# Устанавливаем зависимости
npm install

# Создаём локальную базу данных в PostgreSQL если будем с ней работать
createdb events-api;

# Накатываем миграции если нужно
npm run migrate

# Запускаем тесты
npm test

# Или запускаем бекенд как http-сервис
c переменными NODE_TLS_REJECT_UNAUTHORIZED=0 OFF_AUTH=true NODE_ENV=testing
POSTGRES_URI_EXTERNAL POSTGRES_URI FEATURE_IMPORT_BTN=true
SENDER_AUTH_USER . их значения лежат в [Секретнице](https://yav.yandex-team.ru/secret/sec-01dz9e47bfmy2dnkk5nwybe7wq/explore/versions)
npm run dev
```

### Соглашения по разработке
- Ветки именуются в формате `EVENTSDEV-1045` (Номер задачи в трекере);
- В описание ПР при необходимости описать проделанную работу;
- Для каждой новой ручки/сервиса/модели пишутся unit и интеграционные тесты; 
- Мерж пулл-реквеста (ПР) в dev-ветку возможен, если:
    - Получен апрув ✅ от ревьюверов;
    - Успешно пройдены тесты;
    - Подтянуты изменения из dev с помощью ребейза (`git pull --rebase upstream dev`);
  
### Разработка

В терминале psql можно выполнить команду: `SET search_path TO events;`, чтобы схема *events* (все таблицы лежат в этой схеме) была по умолчанию.

#### Создание новой миграции

Если нужно изменить структуру таблиц в базе данных, можно использовать механизм миграций [sequelize-cli](https://github.com/sequelize/cli).
Для создания новой миграции нужно выполнить команду, которая создаст файл миграции (*db/migrations/\*.js*):

```bash
npm run migrate:create -- --name create-users-table
```

Примеры структуры миграции можно посмотреть в документации sequelize-cli.
Для применения всех миграциий (которые еще не накатаны) нужно выполнить команду:

```bash
NODE_ENV={env} POSTGRES_URI={dbUri} npm run migrate
```

#### Обновление базового докер репозитория

```bash
cd docker/events-api-base
docker build -t registry.yandex.net/montserrat/events-api-base:latest ./
docker push registry.yandex.net/montserrat/events-api-base:latest
```

#### Документация

Документация написана на [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.0.md).
Для валидации документа удобно использовать online-редактор [swagger-editor](https://swagger-editor.common.yandex.ru).

Писать документацию в одном файле не удобно из-за ее размеров, было принято решение разбить документацию на части ([туториал](https://azimi.me/2015/07/16/split-swagger-into-smaller-files.html)).
Исходники лежат в директории `docs/source`, при мерже ПР дрон выполняет команду для генерации документации (`npm run docs:generate`). 

#### Мониторинги

Инвайт для вступления в чат с мониторингами: [events-monitoring](https://t.me/joinchat/E6k4fRazsodwGAwMAglrFw).

Настройки мониторингов находятся в файле `.monitorado.yml`.
О работе с monitorado подробнее можно прочитать [в документации](https://github.yandex-team.ru/toolbox/monitorado).

### Дополнительная информация 

Урл тестовой базы и токен для тестового рассылятора можно посмотреть в [Секретнице](https://yav.yandex-team.ru/secret/sec-01dz9e47bfmy2dnkk5nwybe7wq/explore/version/ver-01dz9e47byw1mjcxxysra5tnwf)

---

*Powered by [generator-spine](https://github.yandex-team.ru/toolbox/generator-spine).*

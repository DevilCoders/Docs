# Новая админка для сайта Академии Яндекса на основе Strapi

ABC: [Медуза (медиаплатформа)](https://abc.yandex-team.ru/services/meduza/)

CMS: [Strapi v3](https://docs-v3.strapi.io/)

[Документация](https://wiki.yandex-team.ru/new-site-academy/)

## Подготовка окружения

[Как установить brew](https://wiki.yandex-team.ru/spec/devops/kakustanovitbrew/)

```bash
# Устанавливаем NVM (не забываем выполнить инструкции от Brew в секции Caveats)
brew install nvm

# Устанавливаем Node.js 12.22.12 версии
nvm install 12.22.12

# Устанавливаем зависимости в /arcadia/frontend
npm ci --registry=https://npm.yandex-team.ru

# Устанавливаем зависимости сервиса
cd services/meduza-strapi
nvm use
npm install

# Устанавливаем конфиги и секреты
npm install -g --registry=https://npm.yandex-team.ru @yandex-int/make-my-env (устанавливаем make-my-env глобально)
npm run env
```

По умолчанию make-my-env подтянет креды в .env для подключения к базе данных тестинга, однако для разработки рекомендуется установить собственную версию Postgres

```bash
# Устанавливаем postgres
brew install postgresql

# Запускаем
brew services start postgresql

# Открываем консоль для настройки установленной базы
psql postgres
```

В открытой консоли Postgres выполняем

```sql
-- создаем новую роль
CREATE ROLE meduzastrapiadmin WITH LOGIN PASSWORD '1234567';

-- выдаем ей права на создания новых баз данных
ALTER ROLE meduzastrapiadmin CREATEDB;
```

После этого меняем содержимое .env с

```
DATABASE_HOST=....
DATABASE_USERNAME=....
DATABASE_PASSWORD=....
DATABASE_NAME=....
DATABASE_PORT=....
DATABASE_CERT=....
ADMIN_JWT_SECRET=....
JWT_SECRET=....
```

на

```
DATABASE_USERNAME=meduzastrapiadmin
DATABASE_PASSWORD=1234567
APP_KEYS={то что сгенерировалось}
JWT_SECRET={то что сгенерировалось}
ADMIN_JWT_SECRET={то что сгенерировалось}
JWT_SECRET={то что сгенерировалось}
```

Хост и порт указывать больше не нужно, т.к. в конфиге по умолчанию забиты хост и порт на которых postgres запускается локально.

Далее, необходимо создать базу данных:

1. Устанавливаем [pgAdmin4](https://www.pgadmin.org/download/);
2. Придумываем мастер пароль;
3. Делаем правый клик по строчке _Servers_, выбираем _Register_ => _Server..._
4. Вкладка **General**:
    1. **Name:** Любое имя на английском языке
5. Вкладка **Connection**:
    1. **Host Name/ Address:** 127.0.0.1
    2. **Port:** 5432
    3. **Maintenance Database:** postgres (Всегда!)
    4. **Username:** {ваш юзернейм}
6. Нажимаем **Save**.
7. Правый клик по строчке _Databases_ => _Create_ => _Database..._
8. Вводим в поле **Name** meduzastrapi.

## Запуск

```bash
# Собираем фронт админки
npm run build

# Локальный запуск в режиме разработки с перезапуском сервера при изменениях
npm run dev
```

Сервис становится доступен по адресам:

- https://strapi.local.yandex.ru/ - апишка
- https://strapi.local.yandex.ru/admin - админка

## Доступ в админку (Не актуально до https://st.yandex-team.ru/ACADEMYDEV-134)

На вход в даминку реализована паспортная авторизация, локально проходит через [тестовый паспорт](https://passport-test.yandex.ru). Но для того, чтобы получилось доступ в нее, нужно выдать роль на соответствующий логин в тестовом паспорте через IDM.

Если используется локальная база, то это можно сделать дернув ручку интеграции с IDM:

```bash
# Выдаст роль суперпользователя
# Замените PASSPORT_TEST_LOGIN_HERE в данных на свой логин в тестовом паспорте
curl -X POST \
  https://strapi.local.yandex.ru/idm/add-role \
  -H 'content-type: application/x-www-form-urlencoded' \
  -d 'role=%7B%22group%22%3A%20%22strapi-super-admin%22%7D&fields=%7B%22external_passport_login%22%3A%20%22PASSPORT_TEST_LOGIN_HERE%22%7D&login=robot-elvis&path=%2Fgroup%2Fsuper%2F'
```

Если используется база тестинга, то же самое можно сделать через [интерфейс IDM](https://idm.yandex-team.ru/system/meduza-admin-strapi-test). Нужно запросить необходимую роль, указать в качестве сотрудника робота @robot-elvis, а для поля "Внешний паспортный логин" свой логин в тестовом паспорте.

## Выкатка в testing

Адрес тестинга: [https://academy-strapi-testing.common.yandex.ru](https://academy-strapi-testing.common.yandex.ru/admin)

Пока что приложение можно выкатить только вручную (локально), собрав докер-образ у себя на машине (нужно, чтобы был установлен Докер).

Это можно сделать с помощью команды

```bash
npm run tools:deploy
```

Скрипт подскажет, какие переменные окружения необходимо установить. Все переменные окружения, кроме `VERSION`, хранятся в [секретнице](https://yav.yandex-team.ru/secret/sec-01fpd69dn4v6d7s62bz60xw178).

Задать переменные окружения:

```bash
export VERSION=xx.y
```

Собранный образ руками выкатывается в testing через интерфейс YD.

## Как добавлять пакеты (Информация на 27.04)

В данный момент мы не можем добавлять пакеты через классический npm install {package_name}. Если возникает необходимость добавить в проект новый пакет, необходимо сделать следующее:

1. Скачать файлы пакета;
2. Перенести их в папку vendor/ в правильную подпапку (лучше категоризировать пакеты, например: плагины Strapi лучше класть в подпапку @strapi, пакеты, связанные с React, в подпапку @react и т.д.);
3. Внести в package.json соответствующего пакета поле private: true;
4. Изменить файлы .eslintignore и .stylelintignore в вышестоящей директории: добавить туда исключения для своего пакета, если таких не имеется;
5. Поправить стили в пакетах, или добавить туда игнорирование линтера.

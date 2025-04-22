# Как развернуть локально shiftinator

## Установка зависимостей и получение доступов

----------------------------------------------------------------

```bash
cd frontend
npm install
# npm install --legacy-peer-deps --force в случае ошибки
pip3 install tvmtool-bin -i https://pypi.yandex-team.ru/simple
cd ../backend
python3 -m venv venv
source venv/bin/activate
pip3 install -r requirements.txt
```

Попросить управляющего продуктом добавить в разработку в ABC(необходимо будет подождать несколько часов, чтобы все доступы проросли) и поделиться папкой tvm, которую разместить в папку backend

## Создать dev.yaml и .env.local

----------------------------------------------------------------

```bash
cp backend/config/development.yaml backend/config/dev.yaml
touch frontend/.env.local
```

В dev.yaml указываем:

- [Nanny token](https://nanny.yandex-team.ru/ui/#/oauth)
- [Staff и Startrek token](https://wiki.yandex-team.ru/tools/support/startrek/api/tokenfortracker/)
- TVM token, который находится в backend/tvm/tvm-token

В .env.local записываем

```text
NEXT_PUBLIC_SHIFT_API_BASEURL="http://localhost:8000/"
SHIFT_ENV=prestable
```

## Создаем тестовую базу

----------------------------------------------------------------

Скачать PostgreSQL

Авторизоваться под superuser

```bash
psql -U postgres
```

Создать пользователя и базу данных

```SQL
CREATE USER shiftinator_admin;
CREATE DATABASE shiftinator_test_db OWNER shiftinator_admin;
ALTER USER shiftinator_admin WITH PASSWORD 'shiftinator_password';
```

Выполнить миграции

```bash
cd backend
alembic upgrade head
alembic revision --autogenerate
```

## Запуск

----------------------------------------------------------------

### TVM daemon

```bash
. backend/tvm/tvm.sh
```

### Backend

```bash
cd backend/
uvicorn --host 'localhost' app.main:app
```

### Frontend

```bash
npm run dev
```

Приложение будет запущено на [localhost:3000](http://localhost:3000)

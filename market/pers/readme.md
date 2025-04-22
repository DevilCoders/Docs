# Бекэнды персональных сервисов маркета

Направления:
- grade - отзывы (создание, выдача в ЛК), ачивки
- static - отзывы (выдача)
- qa - вопросы, ответы, комментарии
- author - агитации, экспертизы, видео
- pay - платёжный сервис для ugc контента
- basket - избранное
- comparison - сравнения
- history - история просмотров (прокси к рекомендациям), счётчик просмотров статей
- feedback - фидбек по заказам (превращается в отзывы)
- model-params - выдача для обзоров на товары

### Как писать код
Сначала нужно сгенерировать проект для ide командой `ya ide idea` c любимыми параметрами.
Или можно воспользоваться скриптом https://a.yandex-team.ru/arc/trunk/arcadia/market/pers/common/src/main/bin/persidea.sh

Ветку для разработки обычно называем по имени тикета (можно с суффиксами, если несколько pr на задачу). 
В названии PR должен быть указан тикет.

Сборка проекта через `ya make -t`

### Как проверять код
Прогон тестов через `ya make -tt` (лушче поближе к целевому сервису, не из корня)

Прогон выбранного тесте через `ya make -tt -F *SelectedTestName*`

Также тесты прогоняются в CI и перед релизом, так что ошибку не пропустим.

### Как запустить локально
В каждом модуле есть скрипт `local-start.sh`

Если нужна отладка - запускаем c `--debug-port=6666` (или любой любимый порт)

Для запуска нужны переменные окружения из [секрета](https://yav.yandex-team.ru/secret/sec-01f8w3grxh1madbsbhz8ayrhbb/explore/versions).
В нём дев-токены и пароли к дев-базам. Доступ к секрету можно запросить у [команды](https://abc.yandex-team.ru/services/marketpers).

Обычно для проверки достаточно локальной pg БД.
Если по какой-то причине нужна тестовая и нет паролей от тестовой БД - пишите команде.

### Как релизить
Дашборд релизов: https://tsum.yandex-team.ru/pipe/projects/pers

Есть релизные пайплайны, а также каждый проект можно выкатить из пользовательской ветки `users/$USER/branch`

### Локальная pg БД
#### Линукс
```
# Название пакета может быть немного другим
apt install postgresql-12

# подключение к СУБД
sudo -u postgres psql

# запуск/останов СУБД
service postgresql start
service postgresql stop
```
#### Мак
```
#Название пакета может меняться. Либо postgresql@12, либо просто postgresql.
brew install postgresql@12

# запуск постгри как сервиса
brew services start postgresql@12

# разовый запуск (обычно не нужно, и БД просто будет висеть как сервис)
pg_ctl -D /usr/local/var/postgresql@12 start

# Подключаемся в первый раз
psql -d template1

# Создаём БД со своим логином
create database #your_login#

# Выходим, и теперь можно подключиться просто как
psql
```

#### Скрипт для создания заглушек для всех БД
Заходим в psql, и создаём все базы разом. 
Далее можно накатить на них таблицы через скрипты `liquibase.sh` в каталогах сервисов (руководствуясь ридми).
```
CREATE DATABASE pers_qa_db;
CREATE USER pers_qa WITH ENCRYPTED PASSWORD 'pers_qa';
GRANT ALL PRIVILEGES ON DATABASE pers_qa_db TO pers_qa;

CREATE DATABASE pers_basket_db;
CREATE USER pers_basket WITH ENCRYPTED PASSWORD 'pers_basket';
GRANT ALL PRIVILEGES ON DATABASE pers_basket_db TO pers_basket;

CREATE DATABASE pers_author_db;
CREATE USER pers_author WITH ENCRYPTED PASSWORD 'pers_author';
GRANT ALL PRIVILEGES ON DATABASE pers_author_db TO pers_author;

CREATE DATABASE pers_pay_db;
CREATE USER pers_pay WITH ENCRYPTED PASSWORD 'pers_pay';
GRANT ALL PRIVILEGES ON DATABASE pers_pay_db TO pers_pay;

CREATE DATABASE pers_comparison_db;
CREATE USER pers_comparison WITH ENCRYPTED PASSWORD 'pers_comparison';
GRANT ALL PRIVILEGES ON DATABASE pers_comparison_db TO pers_comparison;

CREATE DATABASE pers_feedback_db;
CREATE USER pers_feedback WITH ENCRYPTED PASSWORD 'pers_feedback';
GRANT ALL PRIVILEGES ON DATABASE pers_feedback_db TO pers_feedback;

CREATE DATABASE pers_grade_db;
CREATE USER pers_grade WITH ENCRYPTED PASSWORD 'pers_grade';
GRANT ALL PRIVILEGES ON DATABASE pers_grade_db TO pers_grade;
ALTER USER pers_grade WITH SUPERUSER;
```

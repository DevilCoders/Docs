****Название сервиса****
%%
fleet-communications
%%

****Какую продуктовую проблему решает сервис?****
%%
Обеспечение коммуникаций между диспетчерской и водительским приложением (в первой итерации только в виде рассылок из диспетчерской водителям)
%%

****Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?****
%%
В текущий момент коммуникации работают через старый код в шарпах, который является ненадежным и плохо масштабируется
%%

****Как именно сервис будет решать поставленные перед ним задачи?****
%%
Принимать заявку на рассылку из диспетчерской, сохранять ее для переиспользования и создавать stq-задачу для отправки рассылки в сервис feeds
%%

****Разрабатывается один сервис или система?****
%%
Один сервис
%%

****С кем взаимодействует сервис?****
%%
Сервис feeds, сервис parks (для фильтрации водителей по критериям)
%%

****Какие базы использует?****
%%
Postgres fleet-communications
%%

****Какие периодические процессы?****
%%
Нет
%%

**Планируется обработка персональных данных**
%%
Нет
%%

****Какие данные и по какой схеме сервис будет хранить в базе?****
%%
CREATE SCHEMA fleet_communications;

SET SEARCH_PATH TO fleet_communications;

CREATE TYPE driver_status AS ENUM
    ('working', 'online');

CREATE TYPE mailing_status AS ENUM
    ('created', 'sent', 'cancelled');

CREATE TABLE mailing_templates (
    id                     TEXT           NOT NULL PRIMARY KEY,
    park_id                TEXT           NOT NULL,
    work_rule              TEXT               NULL,
    status                 driver_status      NULL,
    excl_contractor_ids    TEXT[]             NULL,
    incl_contractor_ids    TEXT[]             NULL,
    message                TEXT           NOT NULL,
    created_at             TIMESTAMPTZ    NOT NULL,
    created_by             BIGINT         NOT NULL,
    last_sent_at           TIMESTAMPTZ    NOT NULL,
);

CREATE INDEX ON mailing_templates (park_id, created_at);

CREATE INDEX ON mailing_templates (park_id, last_sent_at);

CREATE TABLE mailings (
    id                 TEXT           NOT NULL PRIMARY KEY,
    park_id            TEXT           NOT NULL,
    template_id        TEXT           NOT NULL,
    created_at         TIMESTAMPTZ    NOT NULL,
    created_by         BIGINT         NOT NULL,
    status             mailing_status NOT NULL,
    updated_at         TIMESTAMPTZ        NULL,

    FOREIGN KEY template_id REFERENCES mailing_templates (id)
);

CREATE INDEX ON mailings (park_id, created_at);

CREATE INDEX ON mailings (park_id, template_id, created_at);

Таблица mailing_templates заполняются до создания stq-задачи
Таблица mailings заполняется из stq
Таблицы используются для формирования истории рассылок
%%

****Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?****
%%
Очень малый объем <1 Гб
%%

****Какие операции над данными заложены?****
%%
Добавление, изменение
%%

****Есть ли какой-то стейт в памяти, как он обновляется и валидируется?****
%%
Нет стейта
%%

****Какая нагрузка ожидается?****
%%
Малая нагрузка <1 рпс
%%

****Какие фолбеки предусмотрены на сам этот сервис?****
%%
Нет
%%

****Какие фолбеки предусмотрены внутри этого сервиса на взаимодействие с другими сервисами?****
%%
Stq-очередь для ретраев рассылки
%%

****Какие возможности масштабируемости закладываются?****
%%
Нет
%%

****Какие точки отказа есть в сервисе?****
%%
Сервисы feeds, parks, база данных
%%

****Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить****
%%
Количество совершенных рассылок и количество водителей, которым приходят рассылки
%%

****Укажите технические метрики****
%%
Стандартные
%%

****Какая функциональность ожидается в сервисе в будущем?****
%%
Двустороннее общение между водительским приложением и диспетчерской
%%

****Какое изменение нагрузки планируется?****
%%
Медленное повышение РПС
%%

****Активно ли будет изменяться сервис?****
%%
Нет
%%

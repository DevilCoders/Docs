****Название сервиса****
%%
fleet-traffic-fines
%%

****Какую продуктовую проблему решает сервис?****
%%
Получение и показ штрафов, наложенных на ТС, принадлежащие паркам
В дальнейшем возможность автоматической оплаты
%%

****Почему нельзя решить эту задачу без разработки нового сервиса существующими решениями?****
%%
Сервис fleet-fines разрабатывался под интеграцию с другим партнером и имеет не вполне подходящую архитектуру
fleet-fines планируется перестать использовать
%%

****Как именно сервис будет решать поставленные перед ним задачи?****
%%
Использовать периодические процессы для актуализации информации
%%

****Разрабатывается один сервис или система?****
%%
Один сервис
%%

****С кем взаимодействует сервис?****
%%
YT, Внешнее API, фронтенд Fleet
%%

****Какие базы использует?****
%%
Postgres fleet-traffic-fines, YT
%%

****Какие периодические процессы?****
%%
https://miro.com/app/board/uXjVONMheR0=/?invite_link_id=752148547356
(См. приложенную к тикету картинку)
%%

**Планируется обработка персональных данных**
%%
Нет
%%

****Какие данные и по какой схеме сервис будет хранить в базе?****
%%
CREATE SCHEMA fleet_traffic_fines;

SET SEARCH_PATH TO fleet_traffic_fines;

CREATE DOMAIN decimal4 AS decimal(19, 4);

CREATE TABLE cars (
    park_id             TEXT        NOT NULL,
    car_id              TEXT        NOT NULL,
    license_plate       TEXT        NOT NULL,
    registraction_cert  TEXT        NOT NULL,
    updated_at          TIMESTAMPTZ NOT NULL,
    is_active           BOOLEAN     NOT NULL,
    is_rental           BOOLEAN     NOT NULL,

    PRIMARY KEY (park_id, car_id)
);

CREATE INDEX ON cars (license_plate, registraction_cert);

CREATE TYPE fine_status AS ENUM
                    ('paid', 'issued');

CREATE TABLE fines (
    fine_uin                   TEXT         NOT NULL PRIMARY KEY,
    license_plate              TEXT         NOT NULL,
    registraction_certificate  TEXT         NOT NULL,
    updated_at                 TIMESTAMPTZ  NOT NULL,
    status                     fine_status  NOT NULL,
    number_of_photos           INT          NOT NULL,
    payment_details            JSONB        NOT NULL,
    issued_at                  DATE         NOT NULL,
    offense_at                 TIMESTAMPTZ  NULL,
    discount_until             DATE         NULL,
    collection_at              DATE         NULL,
    amount                     decimal4     NOT NULL,
    paid_amount                decimal4     NULL,
    discounted_amount          decimal4     NULL,
    fiscal_status              TEXT         NULL,
    offense_address            TEXT         NULL,
    article                    TEXT         NULL
);

CREATE INDEX ON fines (license_plate, registraction_cert);

CREATE TABLE park_fines (
    park_id             TEXT         NOT NULL,
    car_id              TEXT         NOT NULL,
    fine_uin            TEXT         NOT NULL,
    status              fine_status  NOT NULL,
    issued_at           TIMESTAMPTZ  NOT NULL,
    driver_id           TEXT         NULL,

    PRIMARY KEY (park_id, car_id, fine_uin)
);

CREATE INDEX ON park_fines (park_id, issued_at);

CREATE INDEX ON park_fines (park_id, car_id, issued_at);

CREATE INDEX ON park_fines (park_id, status, issued_at);
%%

****Какой объем данных будет храниться и какой объем будет изменяться в единицу времени?****
%%
До 100000 активных арендных машин в месяц - До 500000 штрафов в месяц, если каждый штраф занимает порядка 2 Кб в базе - до 1 Гб в месяц новых штрафов
+ < 5 Гб на запись информации о активных машинах
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
Относительно редкие запуски периодических процессов
<1 рпс на ручке показа информации о штрафах
%%

****Какие фолбеки предусмотрены на сам этот сервис?****
%%
Нет фолбеков
%%

****Какие фолбеки предусмотрены внутри этого сервиса на взаимодействие с другими сервисами?****
%%
Ретраи запросов во внешнее API через stq-очередь
%%

****Какие возможности масштабируемости закладываются?****
%%
Нет
%%

****Какие точки отказа есть в сервисе?****
%%
База данных, stq-agent
Внешнее API (влияет только на периодические процессы)
%%

****Укажите ключевые продуктовые метрики сервиса, за которыми планируете следить****
%%
Количество собранных штрафов, количество активных арендных машин
%%

****Укажите технические метрики****
%%
Стандартные
%%

****Какая функциональность ожидается в сервисе в будущем?****
%%
Возможность выгрузки платежной информации о штрафах, возможность автоматической оплаты штрафов
%%

****Какое изменение нагрузки планируется?****
%%
Медленное повышение РПС на получении штрафов
%%

****Активно ли будет изменяться сервис?****
%%
Да
%%

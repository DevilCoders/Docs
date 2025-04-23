# HROOM

Телеграм бот, который развёрнут на logrus01vd в скрине под логином xavescor
Это произошло, так как в какой-то момент в deploy перестала пинговаться wiki-api и для
безгеморного решения бот был перенесён на логрус.

Все ключи, необходимые для работы бота, находятся в секретнице
https://yav.yandex-team.ru/secret/sec-01dghsy4vbrnscdatw6c8zgpv1/explore/versions
tvm приложение для работы с gozora лежит в https://abc.yandex-team.ru/services/telegrambothroom/resources/?view=consuming&layout=table&supplier=14

Переменные окружения для запуска бота должны выглядеть как-то так.
[https://jing.yandex-team.ru/files/xavescor/Untitled.png]

БД: https://yc.yandex-team.ru/folders/foo1u3d3tolioc5qidpk/managed-postgresql/cluster/mdb8blarkdfp6mba79r3?section=overview
Схема БД:
```sql
    -- auto-generated definition
create table "Users"
(
    id           serial
        constraint users_pk
            primary key,
    is_active    boolean,
    telegram_id  bigint,
    day          integer,
    num          integer,
    quest_time   timestamp,
    username     varchar(255),
    cron_enabled boolean default false not null
);

alter table "Users"
    owner to hroom;

```

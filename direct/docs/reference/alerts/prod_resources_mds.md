# direct.prod_resources.mds

Агрегирует проверки по сервисам:

- avatars
- mds
- s3

## Описание { #description }

Алёрт на утилизацию квоты в сервисах-хранилищах MDS.

## Диагностика { #diagnostics }

Найти в [Dispenser](https://dispenser.yandex-team.ru/db/projects) нужный сервис и посмотреть утилизацию квот.  
Например, Canvas: <https://dispenser.yandex-team.ru/db/projects/canvas>

## Решение { #solution }

Действуй по ситуации. Иногда достаточно просто перераспределить квоту.  
Сомневаешься — сходи к Жене [mokeev@](https://staff.yandex-team.ru/mokeev) как эксперту по заказу железа в Директе.

## Подробности { #details }

Примеры тикетов:

- [DIRECTADMIN-8973: Заказать место в canvas s3](https://st.yandex-team.ru/DIRECTADMIN-8973) — (2020 год) забрали квоту у directadmin
- [DIRECTADMIN-9325: Заказать место в canvas s3 (2021-04)](https://st.yandex-team.ru/DIRECTADMIN-9325) — (2021 год) перераспределили квоту внутри проекта Canvas
- [DIRECTADMIN-9835: Горит алёрт abc_canvas:direct.solomon-alert.mds-usage-s3](https://st.yandex-team.ru/DIRECTADMIN-9835) — (2022 год) заметили, что стали быстрее расходовать место. Поэтому не только добавили места, но и исследовали, почему тренд изменился
- [DIRECTADMIN-9836: Горит алёрт abc_BannerStorage:direct.solomon-alert.mds-usage-mds](https://st.yandex-team.ru/DIRECTADMIN-9836) — (2022 год) ожидаемый рост, добавили ресурсов из копилки [directadmin](https://dispenser.yandex-team.ru/db/projects/directadmin)

## Ссылки { #links }

- Juggler: <https://juggler.yandex-team.ru/project/direct.prod/aggregate?host=direct.prod_resources&service=mds&project=direct.prod>

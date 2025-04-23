# Stands

Директория с актуальными версиями стэндов для Я.Транспорта.
Живут на 2-х dev-машинках: sith.sas.yp-c.yandex.net (Owner [Евгений Матвеев](https://staff.yandex-team.ru/evmatveev)), busanalytics.vla.yp-c.yandex.net (Owner [Виктор Матюхин](https://staff.yandex-team.ru/vam1543))

Стэнды:
Стенд | Описание | Доки | Где запущен | Развитие
--------|--------|--------|--------|--------
Check_realese | Старинный стэнд для проверки релизов статики в дататестинге (отвалившиеся города, порча данных, и т.д.) | https://wiki.yandex-team.ru/viktormatjuxin/20170412-kirilltasks/#checkrelease | sith.sas.yp-c.yandex.net | [Общая таска](https://st.yandex-team.ru/BUSANALYTICS-557)
tracks | Основной стенд для анализа потока по клиду за определенную дату с треками | https://wiki.yandex-team.ru/viktormatjuxin/20170412-kirilltasks/#vjuvertrekov | sith.sas.yp-c.yandex.net, busanalytics.vla.yp-c.yandex.net | [Общая таска](https://st.yandex-team.ru/BUSANALYTICS-557)
XML_diff | Парсер XML от поставщика по Питеру, Ленинградской области, Петрозаводску, Пскову и Великому Новгороду | https://wiki.yandex-team.ru/viktormatjuxin/20170412-kirilltasks/#xmldiff | sith.sas.yp-c.yandex.net | [Общая таска](https://st.yandex-team.ru/BUSANALYTICS-557)

Стенд tracks ходит в 2 машинки и запущено 3 версии: 
- sith.sas.yp-c.yandex.net - 1 штука. БД с данными лежит в Я.Облаке в [PostgeSQL кластере](https://yc.yandex-team.ru/folders/mdb-junk/managed-postgresql) (пока в Junk sith_DB_vN, т.к. квоты пока не дали)
- busanalytics.vla.yp-c.yandex.net - 2 штуки
    - 1 БД лежит локально на машинке в PostgreSQL
    - 1 БД лежит в Я.Облаке в [PostgeSQL кластере](https://yc.yandex-team.ru/folders/mdb-junk/managed-postgresql) (пока в Junk busanalytics_DB_vN, т.к. квоты пока не дали)

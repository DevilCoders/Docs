Аналитика по привязанным картам
===============================

Делали в тикете — [PASSP-22110](https://st.yandex-team.ru/PASSP-22110)

Скрипт на YQL в файле [cards_has_uids.yql](cards_has_uids.yql)

Задача YQL_RUN в Сэндбоксе — https://sandbox.yandex-team.ru/scheduler/14091/view

Запускаем от группы PASSPORT-PROFILE каждый день в 10 утра.

Данные берем из
* Связки из Социализма — [hahn.//home/passport/production/socialism/crypta-dump](https://yt.yandex-team.ru/hahn/navigation?path=//home/passport/production/socialism/crypta-dump)
* Портальные аккаунты — [hahn.//statbox/heavy-dict/passport_userdata](https://yt.yandex-team.ru/hahn/navigation?path=//statbox/heavy-dict/passport_userdata)
* Привязки карт из билинга — [hahn.//home/balance/prod/trust/bindings/bindings](https://yt.yandex-team.ru/hahn/navigation?path=//home/balance/prod/trust/bindings/bindings)
* Карты из билинга [hahn.//home/balance/prod/trust/bindings/card](https://yt.yandex-team.ru/hahn/navigation?path=//home/balance/prod/trust/bindings/card)

Доступ получали в трасте — https://wiki.yandex-team.ru/Trust/yt/#kakpoluchitdostup

Результаты пишем
* С группировкой по uid в YT [hahn.//home/passport/production/cards/uids_has_cards](https://yt.yandex-team.ru/hahn/navigation?path=//home/passport/production/cards/uids_has_cards)
* В отчет [https://stat.yandex-team.ru/Passport.All/own/cards/cards_has_uids](https://stat.yandex-team.ru/Passport.All/own/cards/cards_has_uids) (stat.Passport.All/own/cards/cards_has_uids/daily)

Для доступа на чтение запрашиваем в YT роль passport-production-cards-uids_has_cards-read

## Возможные проблемы и пути решения

* Не сгенерировался дамп Крипты. Перезапускаем задачу после того как сформируем дамп
* Чтобы пересчитать предыдущие дни клонируем таску и прописываем в переменную today нужную дату
* Если перестала обновляться табличка в Трасте (пример смотри в [TRUSTDUTY-1234](https://st.yandex-team.ru/TRUSTDUTY-1234)), то пишем дежурным в очередь [TRUSTDUTY](https://st.yandex-team.ru/trustduty)

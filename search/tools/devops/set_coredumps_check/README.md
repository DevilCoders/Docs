Скрипт set_coredumps_check
==========================

Скрипт для настройки проверки "coredumps" ( https://st.yandex-team.ru/SEPE-14356 ) для пачки Nanny-сервисов.
Написано в рамках задач
* https://st.yandex-team.ru/SEARCH-4897
* https://st.yandex-team.ru/BEGEMOT-258
* https://st.yandex-team.ru/SEARCH-6247

Создаёт новую агрегатную проверку, выпиливая из конфигурации остальных проверок проверку "coredumps".

Нотификации настроены на Telegram как на наиболее удобный способ получения подобной информации (не спамит почту,
mutable одной кнопкой, доступно вне офиса).

Использование
=============

Напечатать дифф конфигурации:

    ./set_coredumps_check -s production_noapache_ -b noapache -u mvel,avitella -d -m 'Set coredumps check'

Добавление ключа `-c` (`--commit`) применит изменения к сервисам.

По всем вопросам использования писать mvel@.
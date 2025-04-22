# Xiva

[![OKO health](https://badger.yandex-team.ru/oko/repo/morda/xiva/health.svg)](https://oko.yandex-team.ru/repo/morda/xiva)


# Notes
 Сервер ксивы для сбора потерявшихся клиентов раз в 20 минут (+10 минут рандома) рвет соединение с клиентом.
 Потерявшиеся - так или иначе закрытые соединения без уведомления пользователей.

# Поднять dev-инстанс
git clone git@github.yandex-team.ru:morda/xiva.git && cd xiva-d0 && make dev

pharma
==============

Проект предоставляет факторы про номера телефонов

lbcpharma
---
Logbroker-клиент заливает события про номера телефонов в базу.

Окружения
-------------
1. prod

    Заливщик читает продные топики, пишет в продную базу.

    API читает из продной базы

2. testing

    Заливщик читает тестовые топики, пишет в продную базу.

    API читает из продной базы, отвечает только про ограниченный список телефонов.

3. dev

    Заливщик читает тестовые топики, пишет в тестовую базу.

    API читает из тестовой базы

Куда задавать вопросы
-------------
passport-dev@yandex-team.ru

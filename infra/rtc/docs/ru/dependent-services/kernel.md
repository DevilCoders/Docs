# Linux kernel

В RTC используется ядро Linux со своим собственным набором патчей направленных на улучшение изоляции workload сервисов. Подробности в [wiki](https://wiki.yandex-team.ru/kernel/).

Ядро выкладывается на кластер в фоне, ребутая сервера один за другим. Такой процесс называется роллингом и выполняется с помощью [Maxwell](./walle.md#maxwell).


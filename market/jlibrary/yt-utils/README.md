# О библиотеке
Библиотека предоставляет набор статически типизированных API
поверх существующих API системы хранения данных YT,
тем самым облегчая использование данных API.

В настоящий момент поддерживаются следующая функциональность:
1. Конфигурация YT HTTP API (через библиотеку iceberg)
2. Конфигурация YT RPC API (через библиотеку ytclient)
3. Описание атрибутов и схемы таблиц (статических и динамических)
4. Обертка вокруг YT HTTP API
5. Обертка вокруг YT RPC API

# Зависимости
Библиотека yt-utils зависит от библиотеки java-ytclient,
которая свою очередь зависит от protobuf версии 3.
Если в вашем проекте используется protobuf версией ниже 3,
то нужно учитывать этот факт. При явном задании версии protobuf
версии 2 можно использовать из этой библиотеки все, кроме rpc api,
которая работает исключительно с третьей версией protobuf.

## Сборка и тестирование
[ya.make](https://wiki.yandex-team.ru/yatool/make/)

## Релизы в ЦУМе

[pipeline](https://tsum.yandex-team.ru/pipe/projects/jlibrary/pipelines/market-libraries), 
[dashboard](https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/market-libraries)

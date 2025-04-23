# General-gateway api

## Адреса
Тестинг: http://general-gateway-api.vrts-slb.test.vertis.yandex.net
Прод: http://general-gateway-api.vrts-slb.prod.vertis.yandex.net

## Принципы

1. Никакой бизнес-логики в сервисе.
gateway предназначен только для проксирования запросов в бекенды, 
и облегчения получения связанных данных.

2. Никакой проверки прав доступа.
Все проверки прав осуществляются в конечном сервисе.
gateway проксирует юзер-тикеты во все бекенды.
(возможно добавятся какие-то еще базовые поля про пользователя)

3. Предпочитать батчевое апи при походах в бекенд.

4. Все листинги (чего угодно) должны поддерживать пагинацию и содержать лимит по умолчанию.

## User-ticket

Если кратно, то user-ticket - это короткоживущий токен авторизованного пользователя. 
Если подробнее: https://wiki.yandex-team.ru/passport/tvm2/user-ticket/
Что бы выполнить GQL запрос под авторизованным пользователем, нужно передать заголовок `x-ya-user-ticket`.
Для удобства передать заголовки можно использую вкладку HTTP HEADERS в http://general-gateway-api.vrts-slb.test.vertis.yandex.net/playground 
Получить user-ticket можно с помощью утилиты `tvmknife`.
Все шаги нужно выполнять на своей виртуалке в qyp (https://qyp.yandex-team.ru), доступов с ноутбука до blackbox нет:
1) Установить tvmknife: https://wiki.yandex-team.ru/passport/tvm2/debug/#tvmknife
2) Получаем oauth токен: https://oauth.yandex.ru/authorize?response_type=token&client_id=be4044964e7243f4b6dd1b6785e78cd3
3) Получаем user-ticket (используется tvm_id от wisp): `./ya tool tvmknife get_user_ticket oauth --tvm_id 2021610 -b blackbox-mimino.yandex.net -t <oauth-token>`

Инструкция с подробностями как это работает: https://clubs.at.yandex-team.ru/passport/3706

# Полезные ссылки про GraphQL

https://principledgraphql.com/
https://www.apollographql.com/blog/graphql/basics/designing-graphql-mutations/
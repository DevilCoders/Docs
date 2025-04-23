[Документация по офлайн метрике почтового поиска](https://wiki.yandex-team.ru/Pochta/analytics/offline-mail-search/)

## Как использовать

В основном в качестве кубика нирваны:

https://nirvana.yandex-team.ru/operation/414c81a0-b2aa-4590-86f2-f1e5c94ce544/overview

`-b basket.json -s google -a basket400 -u http://localhost -o out.json -r 0 -t 0`

-b корзина

-s название системы

-a аккаунт

-u url скрепера

-o результат

-r количество ретраев

-t задержка между ретраями, секунды.

-f доля нескачанных (из-за неполадок) серпов, после которой скрипт упадет. Рекомендованное значение 0.01.

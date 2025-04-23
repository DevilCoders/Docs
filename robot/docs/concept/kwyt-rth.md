# Kwyt и RTHub

**RTHub** — это сервис для потоковой обработки данных на основе [YQL](https://yql.yandex-team.ru/docs/yt/). Принимает на входе protobuf-сообщения из pq/logbroker, применяет к ним YQL-скрипт (или несколько YQL-скриптов), результат так же в виде protobuf-сообщений отдаёт в одну или несколько выходных очередей. Для выполнения YQL-запросов над inmemory данными используется библиотека purecalc.

О том, как работает сервис, можно прочитать подробнее на [странице](https://docs.yandex-team.ru/robot/concept/rthub). 

***Kwyt** — это система хранения данных, а также вьюер, чтобы просматривать данные о страницах. В частности, архивы всех проиндексированных страниц хранятся в архиве на YT Kwyt-pages. Данные об отдельных страниц можно посмотреть при помощи вьюера, а для выкачивания больших объемов данных можно воспользоваться [утилитами скачивания данных](https://docs.yandex-team.ru/robot/concept/kwyt_selectql).

## Обратная связь

* [Telegram KwYT & RTHub](https://t.me/joinchat/B_BNDg7bNV2B8A2KDUgrQw)
* [Очередь в STARTREK](http://st.yandex-team.ru/KWYT)
* [Ответственные](https://abc.yandex-team.ru/services/kwyt/)


7.8.232
-------

[vlad-savinov](http://staff/vlad-savinov) 2022-07-29 18:55:25+03:00

7.8.231
-------

[vlad-savinov](http://staff/vlad-savinov) 2022-07-29 18:52:24+03:00

7.8.230
-------
 * ISEARCH-7328: фикс бага с клиентом для helpdesk

bugfix: session is a cached property  [ https://a.yandex-team.ru/arc/commit/9793372 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-29 18:40:28+03:00

7.8.229
-------
 * ISEARCH-7328: миграция для helpdesk, bugfix и переименование индексатора

rename help/services & add migration & bug fix  [ https://a.yandex-team.ru/arc/commit/9792560 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-29 17:08:29+03:00

7.8.228
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7328: прорастить helpdesk в конфиг и добавить правило колдуна

helpdesk added to config and isearch_rules  [ https://a.yandex-team.ru/arc/commit/9791614 ]

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7386: Чиним падающие индексации

Поправляю баги с индексацией  [ https://a.yandex-team.ru/arc/commit/9791326 ]

* [gg0sha](http://staff/gg0sha)

 * INFRADEV-8634: новый source для индексации help

INFRADEV-8634: новый source для индексации help  [ https://a.yandex-team.ru/arc/commit/9791307 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-29 14:58:00+03:00

7.8.227
-------
 * ISEARCH-7386: исправление стат факторов, из-за которых падает сериализация

fix stat factor  [ https://a.yandex-team.ru/arc/commit/9788207 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-28 22:19:56+03:00

7.8.226
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7386: Доделываем фасеты для карт

Убрал булы из факторов, добавил верный капиталайз  [ https://a.yandex-team.ru/arc/commit/9787583 ]

[shadchin](http://staff/shadchin) 2022-07-28 19:54:57+03:00

7.8.225
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7386: Протаскивание фасетов, факторов и русскоязычного типа в сниппет комнат

Добавил в тело и в сниппет для комнат перевод на русский  [ https://a.yandex-team.ru/arc/commit/9787030 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-28 17:50:00+03:00

7.8.224
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7385: Поиск по карте офиса ищет во всех коллекциях `map` - комнаты, оборудование, переговорки

Добавил правила для коллекций переговорок и оборудования  [ https://a.yandex-team.ru/arc/commit/9785898 ]

[shadchin](http://staff/shadchin) 2022-07-28 15:54:29+03:00

7.8.223
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7362: Настраиваю индексацию для тестинга еще раз

Исправляю очепятки  [ https://a.yandex-team.ru/arc/commit/9778339 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-27 13:41:15+03:00

7.8.222
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7362: Настраиваю индексацию для тестинга

Очепятка  [ https://a.yandex-team.ru/arc/commit/9775209 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-27 12:47:03+03:00

7.8.221
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7362: Настраиваю индексации на тестинге ещё раз

Добавил название репо для каждого класса, создал словаь типов комнат, переключил комнаты и оборудование на свои словари  [ https://a.yandex-team.ru/arc/commit/9774710 ]

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7367: делаем новую ревизию активной автоматически для doc

fix doc  [ https://a.yandex-team.ru/arc/commit/9774639 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-26 18:25:28+03:00

7.8.220
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7362: Настраиваю индексации на тестинге

Поправил настройки  [ https://a.yandex-team.ru/arc/commit/9773320 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-26 16:10:16+03:00

7.8.219
-------
 * ISEARCH-7019: исправляем хендлер на docs

fix handler  [ https://a.yandex-team.ru/arc/commit/9773113 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-26 15:34:15+03:00

7.8.218
-------
 * ISEARCH-7019: начинаем принимать пуши от docs на удаление страниц

listen_docs & DocsLogbrokerHandler & yaml refactoring  [ https://a.yandex-team.ru/arc/commit/9772468 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-26 14:31:03+03:00

7.8.217
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7362: Настраиваю индексации

Добавил базовые настройки                     [ https://a.yandex-team.ru/arc/commit/9772239 ]
 * ISEARCH-7362: Переименовал maps->map

Удалил старые названия

Переименовал сервис  [ https://a.yandex-team.ru/arc/commit/9762276 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-26 13:56:25+03:00

7.8.216
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7379: обновить saas push client

update saas push client  [ https://a.yandex-team.ru/arc/commit/9760897 ]

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7362: Создал новые индексации для офисов

Создал новый индексатор для того, что есть в офисах, отнаследовал от этого базового индексатора индексатор для всех комнат, переговорок и оборудования  [ https://a.yandex-team.ru/arc/commit/9759706 ]

* [shadchin](http://staff/shadchin)

 * Remove simplejson

Модуль `json` из стандартной библиотеки Python 3, это и есть `simplejson`                                                                                       [ https://a.yandex-team.ru/arc/commit/9731584 ]
 * Cleanup and fix ya.make

Некоторые таргеты не были подключены к автосборке, например тесты на ачивку, соотвественно они протухли из-за последнего рефакторинга и никто не заметил  [ https://a.yandex-team.ru/arc/commit/9731571 ]
 * Revert commit r9730846

YT пока не умеет в такие аннотации                                                                                                                         [ https://a.yandex-team.ru/arc/commit/9731539 ]
 * Apply pyupgrade --py310-plus                                                                                                                                                       [ https://a.yandex-team.ru/arc/commit/9730846 ]
 * Apply pyupgrade --py39-plus                                                                                                                                                        [ https://a.yandex-team.ru/arc/commit/9730832 ]
 * Apply pyupgrade --py36-plus                                                                                                                                                        [ https://a.yandex-team.ru/arc/commit/9730827 ]
 * Apply pyupgrade --py3-plus                                                                                                                                                         [ https://a.yandex-team.ru/arc/commit/9730811 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-22 19:47:26+03:00

7.8.215
-------
 * Fix telemetry_host for b2b prestable  [ https://a.yandex-team.ru/arc/commit/9730736 ]

[shadchin](http://staff/shadchin) 2022-07-16 18:31:36+03:00

7.8.214
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7367: делаем новую ревизию активной автоматически для doc external

make new revisions for doc external active one  [ https://a.yandex-team.ru/arc/commit/9727670 ]
 * ISEARCH-7350: назвать сортировку кондуктора так же, как и остальные

rename conductor sort                                  [ https://a.yandex-team.ru/arc/commit/9726863 ]

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7357: Подбираю вес для нормальной релевантности колдунщика

Changed additional weight for Moebius wizard  [ https://a.yandex-team.ru/arc/commit/9727135 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-15 16:25:51+03:00

7.8.213
-------

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7357: искусственно поднимаем релевантность колдунщику от мебиуса триггером

Fixed Moebius wizard  [ https://a.yandex-team.ru/arc/commit/9725258 ]
 * ISEARCH-7357: fixed bugs with the Trigger All

Fixed bug with the All trigger                             [ https://a.yandex-team.ru/arc/commit/9725249 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-15 13:12:28+03:00

7.8.212
-------
 * ISEARCH-7214: фиксим взятие лока при снятии индексации с паузы

fix for lock  [ https://a.yandex-team.ru/arc/commit/9722666 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-14 18:06:58+03:00

7.8.211
-------
 * ISEARCH: при `plainjson` выводим релевантность float до 3х знаков

do not cast relevance to int in plainjson  [ https://a.yandex-team.ru/arc/commit/9720924 ]
 * ISEARCH-7214: небольшой фикс обновления статуса при снятии индексации с паузы

fix                            [ https://a.yandex-team.ru/arc/commit/9720842 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-14 15:02:12+03:00

7.8.210
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7214: cancel celery tasks in case of pausing

cancel celery tasks in case of pausing  [ https://a.yandex-team.ru/arc/commit/9720104 ]

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7250: optimized number of api requests to the Staff and fixed bugs with http

Replaced http module call_with_retry method so the project can be built  [ https://a.yandex-team.ru/arc/commit/9719989 ]

* [shadchin](http://staff/shadchin)

 * ISEARCH-7167 Remove devexp  [ https://a.yandex-team.ru/arc/commit/9715660 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-14 13:33:36+03:00

7.8.209
-------
 * ISEARCH-7364: починить deafult ranking model

return default ranking model  [ https://a.yandex-team.ru/arc/commit/9715334 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-13 16:24:18+03:00

7.8.208
-------
 * ISEARCH-7214: `last_wiki_since` меняем на `last_wiki_pk`

last_wiki_since --> last_wiki_pk  [ https://a.yandex-team.ru/arc/commit/9710785 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-13 13:04:29+03:00

7.8.207
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7214: передаем `fetch_id` через `kwargs` для обновления `last_wiki_since`

pass fetch_id through the kwargs  [ https://a.yandex-team.ru/arc/commit/9703559 ]
 * ISEARCH-7359: поддержать kwargs в `Indexer`

add kwargs to the indexer                                               [ https://a.yandex-team.ru/arc/commit/9703557 ]
 * ISEARCH-7359: поддержать kwargs во всех `do_%` методах

support kwargs in every do_% method                          [ https://a.yandex-team.ru/arc/commit/9703111 ]

* [kirpadmitriy](http://staff/kirpadmitriy)

 * ISEARCH-7250: optimized number of api requests to Staff

Added resolve many uids method, modified get users method  [ https://a.yandex-team.ru/arc/commit/9702282 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-11 16:46:49+03:00

7.8.206
-------
 * ISEARCH-7356: убираем домены connect из б2б

remove departments from b2b  [ https://a.yandex-team.ru/arc/commit/9694221 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-08 15:33:09+03:00

7.8.205
-------
 * Fetch all person in walk  [ https://a.yandex-team.ru/arc/commit/9685840 ]

[shadchin](http://staff/shadchin) 2022-07-07 07:41:42+03:00

7.8.204
-------
 * ISEARCH: фиксим не ascii cookie в ABInfoStep

fix non ascii cookie  [ https://a.yandex-team.ru/arc/commit/9678359 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-05 18:58:21+03:00

7.8.203
-------
 * Add log  [ https://a.yandex-team.ru/arc/commit/9675862 ]

[shadchin](http://staff/shadchin) 2022-07-05 15:31:25+03:00

7.8.202
-------
 * ISEARCH-7284: небольшой фикс хождения в blackbox

fix blackbox request  [ https://a.yandex-team.ru/arc/commit/9672856 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-04 21:12:00+03:00

7.8.201
-------
 * ISEARCH-7284: добавляем user_ticket для хождения в этушку

zomb user ticket for at  [ https://a.yandex-team.ru/arc/commit/9670703 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-07-04 17:22:54+03:00

7.8.200
-------
 * Временно уменьшаем периодичность индексаций idm.groups

временно уменьшаем периодичность индексаций групп idm  [ https://a.yandex-team.ru/arc/commit/9640280 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-28 01:47:09+03:00

7.8.199
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7214: исправляем tp на dt в постановке индексации на паузу

фикс постановки индексации вики на паузу  [ https://a.yandex-team.ru/arc/commit/9628542 ]

* [sumekenov](http://staff/sumekenov)

 * Don't use portalytics

ISEARCH-7278  [ https://a.yandex-team.ru/arc/commit/9625324 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-24 13:26:12+03:00

7.8.198
-------
 * ISEARCH-7314: поддержка remove_old_scopes

поддержка эксперимента

поддержка эксперимента                         [ https://a.yandex-team.ru/arc/commit/9623022 ]
 * ISEARCH-7299: расставил все точки над е

расставил все точки на е                                                 [ https://a.yandex-team.ru/arc/commit/9616363 ]
 * Правлю доку: как включить оценки на новой вертикали

добавляем информацию о добавлении оценок на новую вертикаль  [ https://a.yandex-team.ru/arc/commit/9615491 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-22 20:25:41+03:00

7.8.197
-------
 * ISEARCH-7299: `content` --> `description`

content --> description       [ https://a.yandex-team.ru/arc/commit/9614707 ]
 * ISEARCH-7298: миграция для оценок в мебиусе

moe migration for marks     [ https://a.yandex-team.ru/arc/commit/9614397 ]
 * ISEARCH-7299: убираем все, кроме описания, в `z_ns_hidden`

z_ns_hidden  [ https://a.yandex-team.ru/arc/commit/9614039 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-21 14:48:12+03:00

7.8.196
-------
 * ISEARCH-7298: регулярная реиндексация мебиуса в тестинге

cron for moebius  [ https://a.yandex-team.ru/arc/commit/9607481 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-20 12:24:33+03:00

7.8.195
-------
 * ISEARCH-7299: фиксим сериализацию cover

yet another test  [ https://a.yandex-team.ru/arc/commit/9606461 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-19 19:25:00+03:00

7.8.194
-------
 * ISEARCH-7299: фиксим cover для мебиуса v2

fix cover  [ https://a.yandex-team.ru/arc/commit/9606400 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-19 18:34:35+03:00

7.8.193
-------
 * ISEARCH-7299: фиксим cover для мебиуса

fix cover field  [ https://a.yandex-team.ru/arc/commit/9605364 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-18 19:35:16+03:00

7.8.192
-------
 * ISEARCH-7299: исправляем баг в факторе rating

fix rating factor moe  [ https://a.yandex-team.ru/arc/commit/9605340 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-18 19:08:55+03:00

7.8.191
-------

[vlad-savinov](http://staff/vlad-savinov) 2022-06-18 17:51:35+03:00

7.8.190
-------

[vlad-savinov](http://staff/vlad-savinov) 2022-06-18 17:28:55+03:00

7.8.189
-------
 * ISEARCH-7299: исправлю опечатку в body для мебиуса

fix typo  [ https://a.yandex-team.ru/arc/commit/9605142 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-18 17:03:40+03:00

7.8.188
-------
 * ISEARCH-7299: новые поля в snippet и факторы

updated snippet and factors  [ https://a.yandex-team.ru/arc/commit/9605117 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-18 14:45:44+03:00

7.8.187
-------
 * ISEARCH-7299: добавляем колдунщики в moebius

moebius wizards & search added to config  [ https://a.yandex-team.ru/arc/commit/9594187 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-16 11:52:55+03:00

7.8.186
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7298: возвращаем moebius в конфиг

moebius added to config  [ https://a.yandex-team.ru/arc/commit/9592789 ]

* [sumekenov](http://staff/sumekenov)

 * Re-update the formula training YQL Code  [ https://a.yandex-team.ru/arc/commit/9589692 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-15 23:13:32+03:00

7.8.185
-------
 * Fix view push logs in Deploy and pushes/push/XXX/meta.json endpoint  [ https://a.yandex-team.ru/arc/commit/9588104 ]

[shadchin](http://staff/shadchin) 2022-06-15 07:56:16+03:00

7.8.184
-------

[vlad-savinov](http://staff/vlad-savinov) 2022-06-10 15:07:42+03:00

7.8.183
-------

[vlad-savinov](http://staff/vlad-savinov) 2022-06-10 14:24:17+03:00

7.8.182
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7299: temp config fix

config fix  [ https://a.yandex-team.ru/arc/commit/9571530 ]

* [shadchin](http://staff/shadchin)

 * Fix celery logs in YD

Вернул логи в YD для селери  [ https://a.yandex-team.ru/arc/commit/9570843 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-09 16:48:03+03:00

7.8.181
-------
 * ISEARCH-7214: logging added

logging  [ https://a.yandex-team.ru/arc/commit/9565076 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-08 17:26:22+03:00

7.8.180
-------
 * ISEARCH-7214: fix last_wiki_since update

fix last_wiki_since update  [ https://a.yandex-team.ru/arc/commit/9560009 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-07 18:43:36+03:00

7.8.179
-------
 * ISEARCH-7214: fix _get_lock

fix lock acquisition  [ https://a.yandex-team.ru/arc/commit/9559288 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-07 17:05:23+03:00

7.8.178
-------
 * Return logs in YP  [ https://a.yandex-team.ru/arc/commit/9557902 ]

[shadchin](http://staff/shadchin) 2022-06-07 14:29:48+03:00

7.8.177
-------
 * Fix celery-beat in testing  [ https://a.yandex-team.ru/arc/commit/9555620 ]

[shadchin](http://staff/shadchin) 2022-06-07 06:35:10+03:00

7.8.176
-------
 * Add logs for supervisord v.2  [ https://a.yandex-team.ru/arc/commit/9555040 ]

[shadchin](http://staff/shadchin) 2022-06-06 23:19:50+03:00

7.8.175
-------
 * ISEARCH-7298: исправление ошибок в индексаторе Мебиуса

fix pagination  [ https://a.yandex-team.ru/arc/commit/9554332 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-06 19:51:28+03:00

7.8.174
-------

[shadchin](http://staff/shadchin) 2022-06-06 19:28:01+03:00

7.8.173
-------

[shadchin](http://staff/shadchin) 2022-06-06 19:14:00+03:00

7.8.172
-------

[shadchin](http://staff/shadchin) 2022-06-06 17:54:16+03:00

7.8.171
-------

* [mamatkasym](http://staff/mamatkasym)

 * Create Moebius indexation classes

limit snippet lang  [ https://a.yandex-team.ru/arc/commit/9541940 ]

[uruz](http://staff/uruz) 2022-06-03 12:00:57+03:00

7.8.170
-------

* [mamatkasym](http://staff/mamatkasym)

 * Create Moebius indexation classes

fix errors  [ https://a.yandex-team.ru/arc/commit/9540437 ]

[uruz](http://staff/uruz) 2022-06-02 20:06:16+03:00

7.8.169
-------

* [mamatkasym](http://staff/mamatkasym)

 * Create Moebius indexation classes

correct saas service name  [ https://a.yandex-team.ru/arc/commit/9539598 ]

[uruz](http://staff/uruz) 2022-06-02 18:03:55+03:00

7.8.168
-------

* [uruz](http://staff/uruz)

 * ISEARCH-7291: Поправить апдейт статусов pushrecord по статусам pushinstance  [ https://a.yandex-team.ru/arc/commit/9538691 ]

* [mamatkasym](http://staff/mamatkasym)

 * ISEARCH-7258 Create Moebius indexation classes

added new search service  [ https://a.yandex-team.ru/arc/commit/9538687 ]

[uruz](http://staff/uruz) 2022-06-02 16:28:11+03:00

7.8.167
-------

[uruz](http://staff/uruz) 2022-06-02 14:48:26+03:00

7.8.166
-------

[uruz](http://staff/uruz) 2022-06-02 13:09:56+03:00

7.8.165
-------

* [mamatkasym](http://staff/mamatkasym)

 * ISEARCH-7258 Create Moebius indexation classes

fix get_objects method

seperate client class

fetch all courses with pagination

improve client class

added url field

added moebious snippet

created moebous intexer class  [ https://a.yandex-team.ru/arc/commit/9534667 ]

[uruz](http://staff/uruz) 2022-06-01 22:19:04+03:00

7.8.164
-------
 * ISEARCH-7284: Перейти на авторизацию в Этушке по TVM  [ https://a.yandex-team.ru/arc/commit/9533376 ]

[uruz](http://staff/uruz) 2022-06-01 18:24:47+03:00

7.8.163
-------

* [mamatkasym](http://staff/mamatkasym)

 * ISEARCH-7262 Починить индексацию idm

remove url field from snippet  [ https://a.yandex-team.ru/arc/commit/9530594 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-06-01 13:36:17+03:00

7.8.162
-------

* [mamatkasym](http://staff/mamatkasym)

 * ISEARCH-7262 Починить индексацию idm

check name value type  [ https://a.yandex-team.ru/arc/commit/9528650 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-31 23:42:36+03:00

7.8.161
-------

* [mamatkasym](http://staff/mamatkasym)

 * ISEARCH-7262 Починить индексацию idm, fix errors

fix key errors  [ https://a.yandex-team.ru/arc/commit/9528016 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-31 20:12:04+03:00

7.8.160
-------
 * ISEARCH-7214: fix cleanup

fix cleanup  [ https://a.yandex-team.ru/arc/commit/9527850 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-31 19:50:10+03:00

7.8.159
-------
 * ISEARCH-7214: fixing stage cancellation in case of pausing

fix stage cancelation in case of paused indexation  [ https://a.yandex-team.ru/arc/commit/9526200 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-31 16:12:58+03:00

7.8.158
-------

* [mamatkasym](http://staff/mamatkasym)

 * ISEARCH-7262 Починить индексацию idm

changed pagination  [ https://a.yandex-team.ru/arc/commit/9521137 ]

[uruz](http://staff/uruz) 2022-05-30 18:34:33+03:00

7.8.157
-------
 * ISEARCH-7214: paused indexation

initial  [ https://a.yandex-team.ru/arc/commit/9519153 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-30 14:27:57+03:00

7.8.156
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7276: revision activation fix

fixing revision activation after an indexation is done  [ https://a.yandex-team.ru/arc/commit/9512782 ]
 * ISEARCH-7243: logging

logging even without dry run                                            [ https://a.yandex-team.ru/arc/commit/9476039 ]

* [sumekenov](http://staff/sumekenov)

 * Add code for creating learning pool for intranet in FML

Add YQL scripts for uploading FML pool  [ https://a.yandex-team.ru/arc/commit/9494447 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-27 17:40:31+03:00

7.8.155
-------
 * ISEARCH-7243: correct logging

correct logging  [ https://a.yandex-team.ru/arc/commit/9475075 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-19 15:35:58+03:00

7.8.154
-------
 * ISEARCH-7243: export_marks, selecting only non-empty uids

selecting only marks with non empty uids  [ https://a.yandex-team.ru/arc/commit/9473581 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-19 12:43:27+03:00

7.8.153
-------
 * ISEARCH-7243: fixing export_marks command

fixing export marks  [ https://a.yandex-team.ru/arc/commit/9472909 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-19 11:02:52+03:00

7.8.152
-------
 * ISEARCH-7260: Добавить параметров валидации с saas_push  [ https://a.yandex-team.ru/arc/commit/9470332 ]

[uruz](http://staff/uruz) 2022-05-18 16:47:40+03:00

7.8.151
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7243: testing

removing requests for testing purposes  [ https://a.yandex-team.ru/arc/commit/9470003 ]

* [mamatkasym](http://staff/mamatkasym)

 * ISEARCH-7257 Create Moebius API client and test it

added moebius endpoint api                                                                                  [ https://a.yandex-team.ru/arc/commit/9469734 ]
 * ISEARCH-6990  Fix the BegemotStep error with the empty query

Fix the BegemotStep error with the empty query

override get_future and process_response methods  [ https://a.yandex-team.ru/arc/commit/9469534 ]

* [uruz](http://staff/uruz)

 * Translated docs  [ https://a.yandex-team.ru/arc/commit/9463711 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-05-18 16:07:07+03:00

7.8.150
-------

* [uruz](http://staff/uruz)

 * ISEARCH-7249: Test if http -> https helps  [ https://a.yandex-team.ru/arc/commit/9448425 ]

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7243: timeout added for the sandbox task  [ https://a.yandex-team.ru/arc/commit/9448421 ]

[uruz](http://staff/uruz) 2022-05-12 20:32:28+03:00

7.8.149
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7240: adding new fields                                                                                                               [ https://a.yandex-team.ru/arc/commit/9443528 ]
 * ISEARCH-7243: фиксы по выдаче ачивки

Remove f-string skipped at previous commit

Add more info for logs

Add exception to handle empty uids  [ https://a.yandex-team.ru/arc/commit/9443123 ]
 * ISEARCH-7235: do not highlight layer in suggest                                                                                               [ https://a.yandex-team.ru/arc/commit/9442934 ]

[uruz](http://staff/uruz) 2022-05-11 21:05:57+03:00

7.8.148
-------

* [zhukoff-pavel](http://staff/zhukoff-pavel)

 * Implement manager for intrasearch achievement with id 1292

Менеджер для обновления ачивок в ачивнице. ISEARCH-7179.  [ https://a.yandex-team.ru/arc/commit/9388481 ]

[uruz](http://staff/uruz) 2022-04-22 20:13:03+03:00

7.8.147
-------
 * PR from branch users/uruz/feature/remove-so-rule

Remove SO from schedule

Remove SO rules  [ https://a.yandex-team.ru/arc/commit/9387827 ]
 * ISEARCH-7105: Fix suggest answer                                                            [ https://a.yandex-team.ru/arc/commit/9387566 ]

[uruz](http://staff/uruz) 2022-04-22 18:43:00+03:00

7.8.146
-------
 * ISEARCH-7105: Fix defaults  [ https://a.yandex-team.ru/arc/commit/9383034 ]

[uruz](http://staff/uruz) 2022-04-21 21:22:14+03:00

7.8.145
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * build config moved

build config moved                                    [ https://a.yandex-team.ru/arc/commit/9381843 ]
 * ISEARCH-7214: retry on 429 at wiki indexer

retry on 429 at wiki indexer  [ https://a.yandex-team.ru/arc/commit/9375829 ]

* [uruz](http://staff/uruz)

 * releasing version 7.8.142                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9376696 ]
 * ISEARCH-7105: fix for charset                                                                                                                                                                        [ https://a.yandex-team.ru/arc/commit/9376629 ]
 * releasing version 7.8.141                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9376065 ]
 * releasing version 7.8.140                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9375047 ]
 * ISEARCH-7105: Add optional port + parse text/plain to avoid preflight requests                                                                                                                       [ https://a.yandex-team.ru/arc/commit/9375025 ]
 * releasing version 7.8.139                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9374290 ]
 * ISEARCH-7105: Fix error if zero + better handle errors                                                                                                                                               [ https://a.yandex-team.ru/arc/commit/9374140 ]
 * releasing version 7.8.138                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9371522 ]
 * ISEARCH-7105: Fix CORS credentials                                                                                                                                                                   [ https://a.yandex-team.ru/arc/commit/9371511 ]
 * releasing version 7.8.137                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9371484 ]
 * ISEARCH-7105: Cors fixes 2                                                                                                                                                                           [ https://a.yandex-team.ru/arc/commit/9371459 ]
 * releasing version 7.8.136                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9370379 ]
 * ISEARCH-7105: Cors fixes                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9370098 ]
 * releasing version 7.8.135                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9358476 ]
 * ISEARCH-7105: Reorder middleware                                                                                                                                                                     [ https://a.yandex-team.ru/arc/commit/9358463 ]
 * releasing version 7.8.134                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9357894 ]
 * ISEARCH-7105: Change migration                                                                                                                                                                       [ https://a.yandex-team.ru/arc/commit/9357834 ]
 * releasing version 7.8.133                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9353366 ]
 * ISEARCH-7105: Ручка оценок для нового саджеста

refactor FormApiVIew

auth in api

style fixes in migration

new migration, names inside the model are fixed

api marks from suggest                 [ https://a.yandex-team.ru/arc/commit/9353320 ]
 * releasing version 7.8.132                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9352732 ]
 * ISEARCH-7132: Make werewolfing login adjustable                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/9352578 ]
 * releasing version 7.8.131                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9334658 ]
 * Revert "ISEARCH-7196: Убрать лишние поля стаффа из ручек выдачи"

This reverts commit 27704fd9ce353c1d046c2322e08add0d84c7938f, reversing
changes made to 098509c0797bb5c67159566e4cf0c82d315d5f68.  [ https://a.yandex-team.ru/arc/commit/9334617 ]
 * releasing version 7.8.130                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9329817 ]
 * ISEARCH-7131: Немного документации                                                                                                                                                                   [ https://a.yandex-team.ru/arc/commit/9329806 ]
 * ISEARCH-7192: Возможность убрать определенные страницы из поиска                                                                                                                                     [ https://a.yandex-team.ru/arc/commit/9329608 ]
 * ISEARCH-7131: Fix highlighting issue                                                                                                                                                                 [ https://a.yandex-team.ru/arc/commit/9324401 ]
 * releasing version 7.8.129                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9319635 ]
 * releasing version 7.8.128                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9319585 ]
 * ISEARCH-7131: Restrict highting fields                                                                                                                                                               [ https://a.yandex-team.ru/arc/commit/9319560 ]
 * releasing version 7.8.127                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9319375 ]
 * ISEARCH-7196: Убрать лишние поля стаффа из ручек выдачи                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/9319318 ]
 * releasing version 7.8.126                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9302170 ]
 * releasing version 7.8.125                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9300912 ]
 * releasing version 7.8.124                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9297743 ]
 * releasing version 7.8.123                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9296115 ]
 * releasing version 7.8.122                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9295946 ]
 * releasing version 7.8.121                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9292674 ]
 * releasing version 7.8.120                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9292574 ]
 * releasing version 7.8.119                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9292200 ]
 * releasing version 7.8.118                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9290908 ]
 * releasing version 7.8.117                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9287569 ]
 * releasing version 7.8.116                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9286060 ]
 * releasing version 7.8.115                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9285311 ]
 * releasing version 7.8.114                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9283058 ]
 * releasing version 7.8.113                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9282819 ]
 * releasing version 7.8.112                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9282249 ]
 * releasing version 7.8.111                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9281965 ]
 * releasing version 7.8.110                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9275796 ]
 * releasing version 7.8.109                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9275603 ]
 * releasing version 7.8.108                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9274355 ]
 * ISEARCH-7156: Отключить обработку событий облачных организаций Трекера                                                                                                                               [ https://a.yandex-team.ru/arc/commit/9274291 ]
 * releasing version 7.8.107                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9274123 ]
 * releasing version 7.8.106                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9264827 ]
 * releasing version 7.8.105                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9264588 ]
 * releasing version 7.8.104                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9263808 ]
 * releasing version 7.8.103                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9261488 ]
 * releasing version 7.8.102                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9260895 ]
 * releasing version 7.8.101                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9260763 ]
 * releasing version 7.8.100                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9260432 ]
 * releasing version 7.8.99                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9260179 ]
 * releasing version 7.8.98                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9257669 ]
 * releasing version 7.8.97                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9256164 ]

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Docs for new source

ISEARCH-7131 Docs for new source                                            [ https://a.yandex-team.ru/arc/commit/9308781 ]
 * ISEARCH-7131 Fix facet label

ISEARCH-7131 Fix facet label                                                    [ https://a.yandex-team.ru/arc/commit/9302126 ]
 * ISEARCH-7131 Fix facets values

ISEARCH-7131 Fix facets values                                                [ https://a.yandex-team.ru/arc/commit/9300857 ]
 * ISEARCH-7131 Add logs for facets

ISEARCH-7131 Add emit attrs                                                 [ https://a.yandex-team.ru/arc/commit/9296936 ]
 * ISEARCH-7131 Unescape title and body

ISEARCH-7131 Unescape title                                             [ https://a.yandex-team.ru/arc/commit/9295849 ]
 * ISEARCH-7131 Fix updated type in snippet

ISEARCH-7131 Fix updated type in snippet                            [ https://a.yandex-team.ru/arc/commit/9292636 ]
 * ISEARCH-7131 Fix snippet

ISEARCH-7131 Fix snippet                                                            [ https://a.yandex-team.ru/arc/commit/9292552 ]
 * ISEARCH-7131 Add checking error code to get person

ISEARCH-7131 Add checking error code to get person        [ https://a.yandex-team.ru/arc/commit/9292108 ]
 * ISEARCH-7131 Add supress if no login in staff

ISEARCH-7131 Add supress if no login in staff                  [ https://a.yandex-team.ru/arc/commit/9290844 ]
 * ISEARCH-7161 Fix ya make

ISEARCH-7161 Fix ya make                                                            [ https://a.yandex-team.ru/arc/commit/9287551 ]
 * ISEARCH-7183 Enable presearch steps if empty is query

ISEARCH-7183 Enable presearch steps if empty is query  [ https://a.yandex-team.ru/arc/commit/9287547 ]
 * ISEARCH-7131 Fix scope name

ISEARCH-7131 Fix scope name                                                      [ https://a.yandex-team.ru/arc/commit/9286946 ]
 * ISEARCH-7173 Add feature enable_stackoverflow

ISEARCH-7173 Add feature enable_stackoverflow                  [ https://a.yandex-team.ru/arc/commit/9285992 ]
 * ISEARCH-7161 Add snippet and wizard for stackoverflow

ISEARCH-7161 Add wizard for stackoverflow              [ https://a.yandex-team.ru/arc/commit/9285978 ]
 * ISEARCH-7131 Add saas abstract to default settings

Add saas abstract to default settings                     [ https://a.yandex-team.ru/arc/commit/9285275 ]
 * ISEARCH-7173 Fix order of scopes

ISEARCH-7173 Fix order of scopes                                            [ https://a.yandex-team.ru/arc/commit/9285205 ]
 * ISEARCH-7131 Add new destionation alias

ISEARCH-7131 Add new destionation alias                              [ https://a.yandex-team.ru/arc/commit/9283001 ]
 * ISEARCH-7131 Add logbroker host for new services

ISEARCH-7131 Add logbroker host for new services            [ https://a.yandex-team.ru/arc/commit/9282791 ]
 * Add timeouts for staffapi

Add timeouts for staffapi                                                          [ https://a.yandex-team.ru/arc/commit/9282188 ]
 * ISEARCH-7131 Fix deprecated for stack overflow

ISEARCH-7131 Fix deprecated for stack overflow                [ https://a.yandex-team.ru/arc/commit/9281913 ]
 * ISEARCH-7131 Fix telementry host

ISEARCH-7131 Fix telementry host                                            [ https://a.yandex-team.ru/arc/commit/9275778 ]
 * ISEARCH-7131 Fix saas clients params for new services

ISEARCH-7131 Fix saas clients params for new services  [ https://a.yandex-team.ru/arc/commit/9275419 ]
 * ISEARCH-6515 Renew saas push

ISEARCH-6515 Renew saas push                                                    [ https://a.yandex-team.ru/arc/commit/9273956 ]
 * ISEARCH-7131 Fix fetch object

ISEARCH-7131 Fix fetch object                                                  [ https://a.yandex-team.ru/arc/commit/9264797 ]
 * ISEARCH-7131 Fix no date in object and add logging

ISEARCH-7131 Fix no date in object and add logging        [ https://a.yandex-team.ru/arc/commit/9264475 ]
 * Fix type of object id

Fix type of object id                                                                  [ https://a.yandex-team.ru/arc/commit/9263612 ]
 * ISEARCH-7131 Fix source singular

ISEARCH-7131 Fix source singular                                            [ https://a.yandex-team.ru/arc/commit/9261308 ]
 * ISEARCH-7131 Fix source url in api client

ISEARCH-7131 Fix source url in api client                          [ https://a.yandex-team.ru/arc/commit/9261305 ]
 * ISEARCH-7131 Fix models in migration

ISEARCH-7131 Fix models in migration                                    [ https://a.yandex-team.ru/arc/commit/9260866 ]
 * ISEARCH-7131 New maxmemory policy for redis

ISEARCH-7131 New maxmemory policy for redis                      [ https://a.yandex-team.ru/arc/commit/9260723 ]
 * ISEARCH-7131 Fix migration name

ISEARCH-7131 Fix migration name                                              [ https://a.yandex-team.ru/arc/commit/9260587 ]
 * ISEARCH-7131 Add migrations to ya make

ISEARCH-7131 Add migrations to ya make                                [ https://a.yandex-team.ru/arc/commit/9260414 ]
 * ISEARCH-7131 Add permission for stackoverflowsearch

ISEARCH-7131 Add permission for stackoverflowsearch      [ https://a.yandex-team.ru/arc/commit/9260144 ]
 * ISEARCH-7131 Add intrasearch-so to settings api saas

ISEARCH-7131 Add intrasearch-so to settings api saas    [ https://a.yandex-team.ru/arc/commit/9257655 ]
 * ISEARCH-7165 Fix bug with admin

ISEARCH-7165 Fix bug with admin                                              [ https://a.yandex-team.ru/arc/commit/9256088 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-04-21 18:22:30+03:00

7.8.144
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * build config moved

build config moved                                    [ https://a.yandex-team.ru/arc/commit/9381843 ]
 * ISEARCH-7214: retry on 429 at wiki indexer

retry on 429 at wiki indexer  [ https://a.yandex-team.ru/arc/commit/9375829 ]

* [uruz](http://staff/uruz)

 * releasing version 7.8.142                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9376696 ]
 * ISEARCH-7105: fix for charset                                                                                                                                                                        [ https://a.yandex-team.ru/arc/commit/9376629 ]
 * releasing version 7.8.141                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9376065 ]
 * releasing version 7.8.140                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9375047 ]
 * ISEARCH-7105: Add optional port + parse text/plain to avoid preflight requests                                                                                                                       [ https://a.yandex-team.ru/arc/commit/9375025 ]
 * releasing version 7.8.139                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9374290 ]
 * ISEARCH-7105: Fix error if zero + better handle errors                                                                                                                                               [ https://a.yandex-team.ru/arc/commit/9374140 ]
 * releasing version 7.8.138                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9371522 ]
 * ISEARCH-7105: Fix CORS credentials                                                                                                                                                                   [ https://a.yandex-team.ru/arc/commit/9371511 ]
 * releasing version 7.8.137                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9371484 ]
 * ISEARCH-7105: Cors fixes 2                                                                                                                                                                           [ https://a.yandex-team.ru/arc/commit/9371459 ]
 * releasing version 7.8.136                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9370379 ]
 * ISEARCH-7105: Cors fixes                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9370098 ]
 * releasing version 7.8.135                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9358476 ]
 * ISEARCH-7105: Reorder middleware                                                                                                                                                                     [ https://a.yandex-team.ru/arc/commit/9358463 ]
 * releasing version 7.8.134                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9357894 ]
 * ISEARCH-7105: Change migration                                                                                                                                                                       [ https://a.yandex-team.ru/arc/commit/9357834 ]
 * releasing version 7.8.133                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9353366 ]
 * ISEARCH-7105: Ручка оценок для нового саджеста

refactor FormApiVIew

auth in api

style fixes in migration

new migration, names inside the model are fixed

api marks from suggest                 [ https://a.yandex-team.ru/arc/commit/9353320 ]
 * releasing version 7.8.132                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9352732 ]
 * ISEARCH-7132: Make werewolfing login adjustable                                                                                                                                                      [ https://a.yandex-team.ru/arc/commit/9352578 ]
 * releasing version 7.8.131                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9334658 ]
 * Revert "ISEARCH-7196: Убрать лишние поля стаффа из ручек выдачи"

This reverts commit 27704fd9ce353c1d046c2322e08add0d84c7938f, reversing
changes made to 098509c0797bb5c67159566e4cf0c82d315d5f68.  [ https://a.yandex-team.ru/arc/commit/9334617 ]
 * releasing version 7.8.130                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9329817 ]
 * ISEARCH-7131: Немного документации                                                                                                                                                                   [ https://a.yandex-team.ru/arc/commit/9329806 ]
 * ISEARCH-7192: Возможность убрать определенные страницы из поиска                                                                                                                                     [ https://a.yandex-team.ru/arc/commit/9329608 ]
 * ISEARCH-7131: Fix highlighting issue                                                                                                                                                                 [ https://a.yandex-team.ru/arc/commit/9324401 ]
 * releasing version 7.8.129                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9319635 ]
 * releasing version 7.8.128                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9319585 ]
 * ISEARCH-7131: Restrict highting fields                                                                                                                                                               [ https://a.yandex-team.ru/arc/commit/9319560 ]
 * releasing version 7.8.127                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9319375 ]
 * ISEARCH-7196: Убрать лишние поля стаффа из ручек выдачи                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/9319318 ]
 * releasing version 7.8.126                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9302170 ]
 * releasing version 7.8.125                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9300912 ]
 * releasing version 7.8.124                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9297743 ]
 * releasing version 7.8.123                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9296115 ]
 * releasing version 7.8.122                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9295946 ]
 * releasing version 7.8.121                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9292674 ]
 * releasing version 7.8.120                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9292574 ]
 * releasing version 7.8.119                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9292200 ]
 * releasing version 7.8.118                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9290908 ]
 * releasing version 7.8.117                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9287569 ]
 * releasing version 7.8.116                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9286060 ]
 * releasing version 7.8.115                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9285311 ]
 * releasing version 7.8.114                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9283058 ]
 * releasing version 7.8.113                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9282819 ]
 * releasing version 7.8.112                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9282249 ]
 * releasing version 7.8.111                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9281965 ]
 * releasing version 7.8.110                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9275796 ]
 * releasing version 7.8.109                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9275603 ]
 * releasing version 7.8.108                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9274355 ]
 * ISEARCH-7156: Отключить обработку событий облачных организаций Трекера                                                                                                                               [ https://a.yandex-team.ru/arc/commit/9274291 ]
 * releasing version 7.8.107                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9274123 ]
 * releasing version 7.8.106                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9264827 ]
 * releasing version 7.8.105                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9264588 ]
 * releasing version 7.8.104                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9263808 ]
 * releasing version 7.8.103                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9261488 ]
 * releasing version 7.8.102                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9260895 ]
 * releasing version 7.8.101                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9260763 ]
 * releasing version 7.8.100                                                                                                                                                                            [ https://a.yandex-team.ru/arc/commit/9260432 ]
 * releasing version 7.8.99                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9260179 ]
 * releasing version 7.8.98                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9257669 ]
 * releasing version 7.8.97                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/9256164 ]

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Docs for new source

ISEARCH-7131 Docs for new source                                            [ https://a.yandex-team.ru/arc/commit/9308781 ]
 * ISEARCH-7131 Fix facet label

ISEARCH-7131 Fix facet label                                                    [ https://a.yandex-team.ru/arc/commit/9302126 ]
 * ISEARCH-7131 Fix facets values

ISEARCH-7131 Fix facets values                                                [ https://a.yandex-team.ru/arc/commit/9300857 ]
 * ISEARCH-7131 Add logs for facets

ISEARCH-7131 Add emit attrs                                                 [ https://a.yandex-team.ru/arc/commit/9296936 ]
 * ISEARCH-7131 Unescape title and body

ISEARCH-7131 Unescape title                                             [ https://a.yandex-team.ru/arc/commit/9295849 ]
 * ISEARCH-7131 Fix updated type in snippet

ISEARCH-7131 Fix updated type in snippet                            [ https://a.yandex-team.ru/arc/commit/9292636 ]
 * ISEARCH-7131 Fix snippet

ISEARCH-7131 Fix snippet                                                            [ https://a.yandex-team.ru/arc/commit/9292552 ]
 * ISEARCH-7131 Add checking error code to get person

ISEARCH-7131 Add checking error code to get person        [ https://a.yandex-team.ru/arc/commit/9292108 ]
 * ISEARCH-7131 Add supress if no login in staff

ISEARCH-7131 Add supress if no login in staff                  [ https://a.yandex-team.ru/arc/commit/9290844 ]
 * ISEARCH-7161 Fix ya make

ISEARCH-7161 Fix ya make                                                            [ https://a.yandex-team.ru/arc/commit/9287551 ]
 * ISEARCH-7183 Enable presearch steps if empty is query

ISEARCH-7183 Enable presearch steps if empty is query  [ https://a.yandex-team.ru/arc/commit/9287547 ]
 * ISEARCH-7131 Fix scope name

ISEARCH-7131 Fix scope name                                                      [ https://a.yandex-team.ru/arc/commit/9286946 ]
 * ISEARCH-7173 Add feature enable_stackoverflow

ISEARCH-7173 Add feature enable_stackoverflow                  [ https://a.yandex-team.ru/arc/commit/9285992 ]
 * ISEARCH-7161 Add snippet and wizard for stackoverflow

ISEARCH-7161 Add wizard for stackoverflow              [ https://a.yandex-team.ru/arc/commit/9285978 ]
 * ISEARCH-7131 Add saas abstract to default settings

Add saas abstract to default settings                     [ https://a.yandex-team.ru/arc/commit/9285275 ]
 * ISEARCH-7173 Fix order of scopes

ISEARCH-7173 Fix order of scopes                                            [ https://a.yandex-team.ru/arc/commit/9285205 ]
 * ISEARCH-7131 Add new destionation alias

ISEARCH-7131 Add new destionation alias                              [ https://a.yandex-team.ru/arc/commit/9283001 ]
 * ISEARCH-7131 Add logbroker host for new services

ISEARCH-7131 Add logbroker host for new services            [ https://a.yandex-team.ru/arc/commit/9282791 ]
 * Add timeouts for staffapi

Add timeouts for staffapi                                                          [ https://a.yandex-team.ru/arc/commit/9282188 ]
 * ISEARCH-7131 Fix deprecated for stack overflow

ISEARCH-7131 Fix deprecated for stack overflow                [ https://a.yandex-team.ru/arc/commit/9281913 ]
 * ISEARCH-7131 Fix telementry host

ISEARCH-7131 Fix telementry host                                            [ https://a.yandex-team.ru/arc/commit/9275778 ]
 * ISEARCH-7131 Fix saas clients params for new services

ISEARCH-7131 Fix saas clients params for new services  [ https://a.yandex-team.ru/arc/commit/9275419 ]
 * ISEARCH-6515 Renew saas push

ISEARCH-6515 Renew saas push                                                    [ https://a.yandex-team.ru/arc/commit/9273956 ]
 * ISEARCH-7131 Fix fetch object

ISEARCH-7131 Fix fetch object                                                  [ https://a.yandex-team.ru/arc/commit/9264797 ]
 * ISEARCH-7131 Fix no date in object and add logging

ISEARCH-7131 Fix no date in object and add logging        [ https://a.yandex-team.ru/arc/commit/9264475 ]
 * Fix type of object id

Fix type of object id                                                                  [ https://a.yandex-team.ru/arc/commit/9263612 ]
 * ISEARCH-7131 Fix source singular

ISEARCH-7131 Fix source singular                                            [ https://a.yandex-team.ru/arc/commit/9261308 ]
 * ISEARCH-7131 Fix source url in api client

ISEARCH-7131 Fix source url in api client                          [ https://a.yandex-team.ru/arc/commit/9261305 ]
 * ISEARCH-7131 Fix models in migration

ISEARCH-7131 Fix models in migration                                    [ https://a.yandex-team.ru/arc/commit/9260866 ]
 * ISEARCH-7131 New maxmemory policy for redis

ISEARCH-7131 New maxmemory policy for redis                      [ https://a.yandex-team.ru/arc/commit/9260723 ]
 * ISEARCH-7131 Fix migration name

ISEARCH-7131 Fix migration name                                              [ https://a.yandex-team.ru/arc/commit/9260587 ]
 * ISEARCH-7131 Add migrations to ya make

ISEARCH-7131 Add migrations to ya make                                [ https://a.yandex-team.ru/arc/commit/9260414 ]
 * ISEARCH-7131 Add permission for stackoverflowsearch

ISEARCH-7131 Add permission for stackoverflowsearch      [ https://a.yandex-team.ru/arc/commit/9260144 ]
 * ISEARCH-7131 Add intrasearch-so to settings api saas

ISEARCH-7131 Add intrasearch-so to settings api saas    [ https://a.yandex-team.ru/arc/commit/9257655 ]
 * ISEARCH-7165 Fix bug with admin

ISEARCH-7165 Fix bug with admin                                              [ https://a.yandex-team.ru/arc/commit/9256088 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-04-21 18:15:03+03:00

7.8.143
-------
 * build config moved

build config moved  [ https://a.yandex-team.ru/arc/commit/9381843 ]

[vlad-savinov](http://staff/vlad-savinov) 2022-04-21 18:07:48+03:00

7.8.142
-------
 * ISEARCH-7105: fix for charset  [ https://a.yandex-team.ru/arc/commit/9376629 ]

[uruz](http://staff/uruz) 2022-04-20 18:42:51+03:00

7.8.141
-------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7214: retry on 429 at wiki indexer

retry on 429 at wiki indexer  [ https://a.yandex-team.ru/arc/commit/9375829 ]

[uruz](http://staff/uruz) 2022-04-20 16:55:57+03:00

7.8.140
-------
 * ISEARCH-7105: Add optional port + parse text/plain to avoid preflight requests  [ https://a.yandex-team.ru/arc/commit/9375025 ]

[uruz](http://staff/uruz) 2022-04-20 15:17:10+03:00

7.8.139
-------
 * ISEARCH-7105: Fix error if zero + better handle errors  [ https://a.yandex-team.ru/arc/commit/9374140 ]

[uruz](http://staff/uruz) 2022-04-20 13:47:03+03:00

7.8.138
-------
 * ISEARCH-7105: Fix CORS credentials  [ https://a.yandex-team.ru/arc/commit/9371511 ]

[uruz](http://staff/uruz) 2022-04-19 21:12:53+03:00

7.8.137
-------
 * ISEARCH-7105: Cors fixes 2  [ https://a.yandex-team.ru/arc/commit/9371459 ]

[uruz](http://staff/uruz) 2022-04-19 20:57:53+03:00

7.8.136
-------
 * ISEARCH-7105: Cors fixes  [ https://a.yandex-team.ru/arc/commit/9370098 ]

[uruz](http://staff/uruz) 2022-04-19 17:32:47+03:00

7.8.135
-------
 * ISEARCH-7105: Reorder middleware  [ https://a.yandex-team.ru/arc/commit/9358463 ]

[uruz](http://staff/uruz) 2022-04-15 19:48:22+03:00

7.8.134
-------
 * ISEARCH-7105: Change migration  [ https://a.yandex-team.ru/arc/commit/9357834 ]

[uruz](http://staff/uruz) 2022-04-15 18:08:24+03:00

7.8.133
-------
 * ISEARCH-7105: Ручка оценок для нового саджеста

refactor FormApiVIew

auth in api

style fixes in migration

new migration, names inside the model are fixed

api marks from suggest  [ https://a.yandex-team.ru/arc/commit/9353320 ]

[uruz](http://staff/uruz) 2022-04-14 20:12:22+03:00

7.8.132
-------
 * ISEARCH-7132: Make werewolfing login adjustable  [ https://a.yandex-team.ru/arc/commit/9352578 ]

[uruz](http://staff/uruz) 2022-04-14 18:13:54+03:00

7.8.131
-------
 * Revert "ISEARCH-7196: Убрать лишние поля стаффа из ручек выдачи"

This reverts commit 27704fd9ce353c1d046c2322e08add0d84c7938f, reversing
changes made to 098509c0797bb5c67159566e4cf0c82d315d5f68.  [ https://a.yandex-team.ru/arc/commit/9334617 ]

[uruz](http://staff/uruz) 2022-04-11 13:52:02+03:00

7.8.130
-------
 * ISEARCH-7192: Возможность убрать определенные страницы из поиска  [ https://a.yandex-team.ru/arc/commit/9329608 ]
 * ISEARCH-7131: Fix highlighting issue                              [ https://a.yandex-team.ru/arc/commit/9324401 ]

[uruz](http://staff/uruz) 2022-04-08 21:16:36+03:00

7.8.129
-------

[uruz](http://staff/uruz) 2022-04-06 20:58:04+03:00

7.8.128
-------
 * ISEARCH-7131: Restrict highting fields  [ https://a.yandex-team.ru/arc/commit/9319560 ]

[uruz](http://staff/uruz) 2022-04-06 20:41:28+03:00

7.8.127
-------

* [uruz](http://staff/uruz)

 * ISEARCH-7196: Убрать лишние поля стаффа из ручек выдачи  [ https://a.yandex-team.ru/arc/commit/9319318 ]

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Docs for new source

ISEARCH-7131 Docs for new source  [ https://a.yandex-team.ru/arc/commit/9308781 ]

[uruz](http://staff/uruz) 2022-04-06 19:39:40+03:00

7.8.126
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix facet label

ISEARCH-7131 Fix facet label  [ https://a.yandex-team.ru/arc/commit/9302126 ]

[uruz](http://staff/uruz) 2022-04-01 18:50:05+03:00

7.8.125
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix facets values

ISEARCH-7131 Fix facets values  [ https://a.yandex-team.ru/arc/commit/9300857 ]

[uruz](http://staff/uruz) 2022-04-01 15:50:56+03:00

7.8.124
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add logs for facets

ISEARCH-7131 Add emit attrs  [ https://a.yandex-team.ru/arc/commit/9296936 ]

[uruz](http://staff/uruz) 2022-03-31 20:14:31+03:00

7.8.123
-------

[uruz](http://staff/uruz) 2022-03-31 15:54:34+03:00

7.8.122
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Unescape title and body

ISEARCH-7131 Unescape title  [ https://a.yandex-team.ru/arc/commit/9295849 ]

[uruz](http://staff/uruz) 2022-03-31 15:23:04+03:00

7.8.121
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix updated type in snippet

ISEARCH-7131 Fix updated type in snippet  [ https://a.yandex-team.ru/arc/commit/9292636 ]

[uruz](http://staff/uruz) 2022-03-30 20:00:57+03:00

7.8.120
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix snippet

ISEARCH-7131 Fix snippet  [ https://a.yandex-team.ru/arc/commit/9292552 ]

[uruz](http://staff/uruz) 2022-03-30 19:38:59+03:00

7.8.119
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add checking error code to get person

ISEARCH-7131 Add checking error code to get person  [ https://a.yandex-team.ru/arc/commit/9292108 ]

[uruz](http://staff/uruz) 2022-03-30 18:21:04+03:00

7.8.118
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add supress if no login in staff

ISEARCH-7131 Add supress if no login in staff  [ https://a.yandex-team.ru/arc/commit/9290844 ]

[uruz](http://staff/uruz) 2022-03-30 15:09:28+03:00

7.8.117
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7161 Fix ya make

ISEARCH-7161 Fix ya make                                                            [ https://a.yandex-team.ru/arc/commit/9287551 ]
 * ISEARCH-7183 Enable presearch steps if empty is query

ISEARCH-7183 Enable presearch steps if empty is query  [ https://a.yandex-team.ru/arc/commit/9287547 ]
 * ISEARCH-7131 Fix scope name

ISEARCH-7131 Fix scope name                                                      [ https://a.yandex-team.ru/arc/commit/9286946 ]

[uruz](http://staff/uruz) 2022-03-29 20:02:22+03:00

7.8.116
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7173 Add feature enable_stackoverflow

ISEARCH-7173 Add feature enable_stackoverflow      [ https://a.yandex-team.ru/arc/commit/9285992 ]
 * ISEARCH-7161 Add snippet and wizard for stackoverflow

ISEARCH-7161 Add wizard for stackoverflow  [ https://a.yandex-team.ru/arc/commit/9285978 ]

[uruz](http://staff/uruz) 2022-03-29 15:43:33+03:00

7.8.115
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add saas abstract to default settings

Add saas abstract to default settings  [ https://a.yandex-team.ru/arc/commit/9285275 ]
 * ISEARCH-7173 Fix order of scopes

ISEARCH-7173 Fix order of scopes                         [ https://a.yandex-team.ru/arc/commit/9285205 ]

[uruz](http://staff/uruz) 2022-03-29 13:38:05+03:00

7.8.114
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add new destionation alias

ISEARCH-7131 Add new destionation alias  [ https://a.yandex-team.ru/arc/commit/9283001 ]

[uruz](http://staff/uruz) 2022-03-28 21:03:30+03:00

7.8.113
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add logbroker host for new services

ISEARCH-7131 Add logbroker host for new services  [ https://a.yandex-team.ru/arc/commit/9282791 ]

[uruz](http://staff/uruz) 2022-03-28 20:02:38+03:00

7.8.112
-------

* [mfgnik](http://staff/mfgnik)

 * Add timeouts for staffapi

Add timeouts for staffapi  [ https://a.yandex-team.ru/arc/commit/9282188 ]

[uruz](http://staff/uruz) 2022-03-28 18:14:18+03:00

7.8.111
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix deprecated for stack overflow

ISEARCH-7131 Fix deprecated for stack overflow  [ https://a.yandex-team.ru/arc/commit/9281913 ]

[uruz](http://staff/uruz) 2022-03-28 17:30:16+03:00

7.8.110
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix telementry host

ISEARCH-7131 Fix telementry host  [ https://a.yandex-team.ru/arc/commit/9275778 ]

[uruz](http://staff/uruz) 2022-03-25 20:09:39+03:00

7.8.109
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix saas clients params for new services

ISEARCH-7131 Fix saas clients params for new services  [ https://a.yandex-team.ru/arc/commit/9275419 ]

[uruz](http://staff/uruz) 2022-03-25 19:16:22+03:00

7.8.108
-------
 * ISEARCH-7156: Отключить обработку событий облачных организаций Трекера  [ https://a.yandex-team.ru/arc/commit/9274291 ]

[uruz](http://staff/uruz) 2022-03-25 15:50:31+03:00

7.8.107
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-6515 Renew saas push

ISEARCH-6515 Renew saas push  [ https://a.yandex-team.ru/arc/commit/9273956 ]

[uruz](http://staff/uruz) 2022-03-25 14:59:52+03:00

7.8.106
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix fetch object

ISEARCH-7131 Fix fetch object  [ https://a.yandex-team.ru/arc/commit/9264797 ]

[uruz](http://staff/uruz) 2022-03-23 16:59:20+03:00

7.8.105
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix no date in object and add logging

ISEARCH-7131 Fix no date in object and add logging  [ https://a.yandex-team.ru/arc/commit/9264475 ]

[uruz](http://staff/uruz) 2022-03-23 16:21:09+03:00

7.8.104
-------

* [mfgnik](http://staff/mfgnik)

 * Fix type of object id

Fix type of object id  [ https://a.yandex-team.ru/arc/commit/9263612 ]

[uruz](http://staff/uruz) 2022-03-23 13:24:49+03:00

7.8.103
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix source singular

ISEARCH-7131 Fix source singular                    [ https://a.yandex-team.ru/arc/commit/9261308 ]
 * ISEARCH-7131 Fix source url in api client

ISEARCH-7131 Fix source url in api client  [ https://a.yandex-team.ru/arc/commit/9261305 ]

[uruz](http://staff/uruz) 2022-03-22 20:45:34+03:00

7.8.102
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Fix models in migration

ISEARCH-7131 Fix models in migration  [ https://a.yandex-team.ru/arc/commit/9260866 ]

[uruz](http://staff/uruz) 2022-03-22 17:29:48+03:00

7.8.101
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 New maxmemory policy for redis

ISEARCH-7131 New maxmemory policy for redis  [ https://a.yandex-team.ru/arc/commit/9260723 ]
 * ISEARCH-7131 Fix migration name

ISEARCH-7131 Fix migration name                          [ https://a.yandex-team.ru/arc/commit/9260587 ]

[uruz](http://staff/uruz) 2022-03-22 16:51:04+03:00

7.8.100
-------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add migrations to ya make

ISEARCH-7131 Add migrations to ya make  [ https://a.yandex-team.ru/arc/commit/9260414 ]

[uruz](http://staff/uruz) 2022-03-22 15:42:13+03:00

7.8.99
------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add permission for stackoverflowsearch

ISEARCH-7131 Add permission for stackoverflowsearch  [ https://a.yandex-team.ru/arc/commit/9260144 ]

[uruz](http://staff/uruz) 2022-03-22 14:57:33+03:00

7.8.98
------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7131 Add intrasearch-so to settings api saas

ISEARCH-7131 Add intrasearch-so to settings api saas  [ https://a.yandex-team.ru/arc/commit/9257655 ]

[uruz](http://staff/uruz) 2022-03-21 20:49:34+03:00

7.8.97
------

* [mfgnik](http://staff/mfgnik)

 * ISEARCH-7165 Fix bug with admin

ISEARCH-7165 Fix bug with admin  [ https://a.yandex-team.ru/arc/commit/9256088 ]

[uruz](http://staff/uruz) 2022-03-21 16:00:09+03:00

7.8.96
------

* [eartqk](http://staff/eartqk)

 * ISEARCH-7131: added migrations and celery tasks, fixed header  [ https://a.yandex-team.ru/arc/commit/9255228 ]

* [maratik](http://staff/maratik)

 * ARCANUM-5472: ISEARCH migration  [ https://a.yandex-team.ru/arc/commit/9248904 ]

[uruz](http://staff/uruz) 2022-03-21 13:37:28+03:00

7.8.95
------

* [eartqk](http://staff/eartqk)

 * ISEARCH-7131: Indexation for Stackoverflow

Added source base and api client for stackoverflow  [ https://a.yandex-team.ru/arc/commit/9235587 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-5510 prepare migration from .devexp.json to a.yaml (intranet)  [ https://a.yandex-team.ru/arc/commit/9231012 ]

[uruz](http://staff/uruz) 2022-03-15 16:27:02+03:00

7.8.94
------
 * ISEARCH-7132: remove wrong line  [ https://a.yandex-team.ru/arc/commit/9220515 ]

[uruz](http://staff/uruz) 2022-03-10 18:44:20+03:00

7.8.93
------
 * ISEARCH-7132: Wrong place for language block  [ https://a.yandex-team.ru/arc/commit/9218681 ]

[uruz](http://staff/uruz) 2022-03-10 13:17:41+03:00

7.8.92
------
 * ISEARCH-7132: Fixes  [ https://a.yandex-team.ru/arc/commit/9218568 ]

[uruz](http://staff/uruz) 2022-03-10 12:59:33+03:00

7.8.91
------

* [vlad-savinov](http://staff/vlad-savinov)

 * Suggest atushka layer serializer fix

suggest_atushka_serializer naming fixed  [ https://a.yandex-team.ru/arc/commit/9200032 ]

[uruz](http://staff/uruz) 2022-03-03 15:22:51+03:00

7.8.90
------
 * PR from branch users/uruz/feature/ISEARCH-7132

ISEARCH-7132: Поддержать прокачку серпов от имени TVM-2 приложения

tmp  [ https://a.yandex-team.ru/arc/commit/9198093 ]

[uruz](http://staff/uruz) 2022-03-03 03:08:16+03:00

7.8.89
------

* [vlad-savinov](http://staff/vlad-savinov)

 * suggest layer at renamed to atushka

at renamed to atushka                                      [ https://a.yandex-team.ru/arc/commit/9192743 ]
 * collect_factors_for_pool fix for single query

collect_factors_for_pool fixed for single query  [ https://a.yandex-team.ru/arc/commit/9183926 ]

[uruz](http://staff/uruz) 2022-03-01 18:00:34+03:00

7.8.88
------

* [vlad-savinov](http://staff/vlad-savinov)

 * Suggest attr  support added into at clubs indexer

adding suggest attr into at clubs indexer  [ https://a.yandex-team.ru/arc/commit/9179790 ]

[uruz](http://staff/uruz) 2022-02-24 21:08:27+03:00

7.8.87
------
 * ISEARCH-6777: update abovemeta setting  [ https://a.yandex-team.ru/arc/commit/9172260 ]

[uruz](http://staff/uruz) 2022-02-22 15:12:03+03:00

7.8.86
------

* [uruz](http://staff/uruz)

 * ISEARCH-6777: Добавить гибкости в конфиги celery для плавного переключения  [ https://a.yandex-team.ru/arc/commit/9151561 ]

* [vlad-savinov](http://staff/vlad-savinov)

 * Migration fixed in intranet/search/core

migrations fixed  [ https://a.yandex-team.ru/arc/commit/9129752 ]

[uruz](http://staff/uruz) 2022-02-16 15:36:47+03:00

7.8.85
------

* [uruz](http://staff/uruz)

 * ISEARCH-7113: Починить celery после обновления  [ https://a.yandex-team.ru/arc/commit/9125989 ]

* [vlad-savinov](http://staff/vlad-savinov)

 * New layer at added to suggest, abovemeta

suggest, new layer at abovemeta  [ https://a.yandex-team.ru/arc/commit/9125977 ]

[uruz](http://staff/uruz) 2022-02-09 18:01:39+03:00

7.8.84
------
 * ISEARCH-7109: Переключить походы в api на новый домен  [ https://a.yandex-team.ru/arc/commit/9120073 ]

[uruz](http://staff/uruz) 2022-02-08 15:26:07+03:00

7.8.83
------
 * ISEARCH-7104: Поток обращений о проблемах с индексацией Стаффа  [ https://a.yandex-team.ru/arc/commit/9119448 ]

[uruz](http://staff/uruz) 2022-02-08 14:59:52+03:00

7.8.82
------

* [vlad-savinov](http://staff/vlad-savinov)

 * abovemeta wiki_suggest permission migration, production _env removed from reindex-wiki

new permissions for group in migration, wiki.test _env production removed  [ https://a.yandex-team.ru/arc/commit/9114645 ]

[uruz](http://staff/uruz) 2022-02-07 14:10:59+03:00

7.8.81
------

* [vlad-savinov](http://staff/vlad-savinov)

 * abovemeta migration, wiki layer in suggest

new migration  [ https://a.yandex-team.ru/arc/commit/9110022 ]

[uruz](http://staff/uruz) 2022-02-04 19:46:23+03:00

7.8.80
------

* [vlad-savinov](http://staff/vlad-savinov)

 * abovemeta SuggestDeciderStep logs

adding logs to SuggestDecider in abovemeta  [ https://a.yandex-team.ru/arc/commit/9108923 ]

[uruz](http://staff/uruz) 2022-02-04 16:34:23+03:00

7.8.79
------

* [vlad-savinov](http://staff/vlad-savinov)

 * Logging updated in Decider in abovemeta

if state.debug removed from abovemeta logging  [ https://a.yandex-team.ru/arc/commit/9105365 ]

[uruz](http://staff/uruz) 2022-02-03 19:31:50+03:00

7.8.78
------

* [vlad-savinov](http://staff/vlad-savinov)

 * SuggestForm, SuggestState in abovemeta, debug field added

abovemeta suggest debug state added  [ https://a.yandex-team.ru/arc/commit/9104837 ]

[uruz](http://staff/uruz) 2022-02-03 18:43:26+03:00

7.8.77
------

* [vlad-savinov](http://staff/vlad-savinov)

 * Logging in abovemeta decider changed to .info

abovemeta logging in prepare_search changed to .info  [ https://a.yandex-team.ru/arc/commit/9103499 ]

[uruz](http://staff/uruz) 2022-02-03 14:44:09+03:00

7.8.76
------

* [vlad-savinov](http://staff/vlad-savinov)

 * Debug logging added to abovemeta DeciderStep

debug logging added to abovemeta decider  [ https://a.yandex-team.ru/arc/commit/9099457 ]

[uruz](http://staff/uruz) 2022-02-02 17:27:48+03:00

7.8.75
------

* [vlad-savinov](http://staff/vlad-savinov)

 * ISEARCH-7088: Wiki layer added to intrasearch suggest

intrasearch, wiki added to suggest                                                   [ https://a.yandex-team.ru/arc/commit/9095838 ]
 * ISEARCH-7091: new fields 'author', 'created' added to intrasearch tracker suggest 

intrasearch, new fields added into the tracker suggest  [ https://a.yandex-team.ru/arc/commit/9095687 ]

* [shadchin](http://staff/shadchin)

 * CONTRIB-2453 Reimport kombu  [ https://a.yandex-team.ru/arc/commit/9082043 ]

* [uruz](http://staff/uruz)

 * ISEARCH-7074: Писать при выгрузке факторы как YSON  [ https://a.yandex-team.ru/arc/commit/9070824 ]
 * ISEARCH-7056: Поднять лимиты мониторингов базы      [ https://a.yandex-team.ru/arc/commit/9058332 ]

* [danila-eremin](http://staff/danila-eremin)

 * CROWDFUNDING-15 Fix calling fixtures in intranet/search/tests  [ https://a.yandex-team.ru/arc/commit/9029758 ]

[uruz](http://staff/uruz) 2022-02-01 19:38:44+03:00

7.8.74
------
 * ISEARCH-7028: Правка snippet_languages  [ https://a.yandex-team.ru/arc/commit/9024078 ]

[uruz](http://staff/uruz) 2022-01-12 17:03:10+03:00

7.8.73
------
 * ISEARCH-7028: Правки ошибки обработки nopage  [ https://a.yandex-team.ru/arc/commit/9023289 ]

[uruz](http://staff/uruz) 2022-01-12 14:41:22+03:00

7.8.72
------
 * ISEARCH-7048: Досыпать фильтровочных атрибутов в группы  [ https://a.yandex-team.ru/arc/commit/9019528 ]

[uruz](http://staff/uruz) 2022-01-11 15:57:13+03:00

7.8.71
------
 * PR from branch users/uruz/feature/ISEARCH-7028-2

ISEARCH-7028: Проблемы с индексацией Стаффа

ISEARCH-7028: Rename class to better represent its evil nature  [ https://a.yandex-team.ru/arc/commit/9014991 ]

[uruz](http://staff/uruz) 2022-01-10 14:34:28+03:00

7.8.70
------
 * ISEARCH-7015: up deps              [ https://a.yandex-team.ru/arc/commit/8971327 ]
 * ISEARCH-7015: another attempt      [ https://a.yandex-team.ru/arc/commit/8969484 ]
 * ISEARCH-7015: gunicorn -> uwsgi 2  [ https://a.yandex-team.ru/arc/commit/8968386 ]

[uruz](http://staff/uruz) 2021-12-21 14:25:35+03:00

7.8.69
------
 * ISEARCH-7015: gunicorn -> uwsgi  [ https://a.yandex-team.ru/arc/commit/8967749 ]

[uruz](http://staff/uruz) 2021-12-20 15:56:49+03:00

7.8.68
------
 * ISEARCH-6994: Verbose output                                       [ https://a.yandex-team.ru/arc/commit/8955238 ]
 * ISEARCH-6992: CORS, переводы, возможность принимать URL без схемы  [ https://a.yandex-team.ru/arc/commit/8955142 ]

[uruz](http://staff/uruz) 2021-12-16 00:30:17+03:00

7.8.67
------

[uruz](http://staff/uruz) 2021-12-13 18:15:27+03:00

7.8.66
------
 * ISEARCH-6994: fix template error again  [ https://a.yandex-team.ru/arc/commit/8944342 ]

[uruz](http://staff/uruz) 2021-12-13 15:52:03+03:00

7.8.65
------
 * ISEARCH-6994: fix template error  [ https://a.yandex-team.ru/arc/commit/8943869 ]

[uruz](http://staff/uruz) 2021-12-13 14:50:22+03:00

7.8.64
------
 * ISEARCH-6994: fix import path  [ https://a.yandex-team.ru/arc/commit/8926929 ]

[uruz](http://staff/uruz) 2021-12-10 21:54:30+03:00

7.8.63
------
 * ISEARCH-6994: Научиться по паре запрос+url получать значение всех факторов из relev.conf из SAAS  [ https://a.yandex-team.ru/arc/commit/8926661 ]

[uruz](http://staff/uruz) 2021-12-10 20:11:45+03:00

7.8.62
------
 * ISEARCH-6992: Добавляем OPTIONS чтобы использовать на тестинге CORS  [ https://a.yandex-team.ru/arc/commit/8917820 ]
 * ISEARCH-7010: Починить падающий тест                                 [ https://a.yandex-team.ru/arc/commit/8913978 ]

[uruz](http://staff/uruz) 2021-12-08 20:12:07+03:00

7.8.61
------
 * ISEARCH-6992: Возможность предложить свою ссылку в выдаче - back  [ https://a.yandex-team.ru/arc/commit/8913646 ]
 * ISEARCH-6951: Придумать универсальный интерфейс индексации        [ https://a.yandex-team.ru/arc/commit/8889270 ]

[uruz](http://staff/uruz) 2021-12-07 19:53:42+03:00

7.8.60
------
 * ISEARCH-6979: Убрать Обучатор из поиска  [ https://a.yandex-team.ru/arc/commit/8884814 ]

[uruz](http://staff/uruz) 2021-11-29 20:09:25+03:00

7.8.59
------
 * ISEARCH-6913: Правки ошибки отступа  [ https://a.yandex-team.ru/arc/commit/8798873 ]

[uruz](http://staff/uruz) 2021-11-03 15:26:27+03:00

7.8.58
------
 * ISEARCH-6913: More logs  [ https://a.yandex-team.ru/arc/commit/8796564 ]

[uruz](http://staff/uruz) 2021-11-02 21:38:55+03:00

7.8.57
------
 * PR from branch users/uruz/feature/ISEARCH-6859-2

ISEARCH-6859: fix startup

ISEARCH-6859: Правильные ссылки на логи в Y.Deploy  [ https://a.yandex-team.ru/arc/commit/8784603 ]

[uruz](http://staff/uruz) 2021-10-29 18:30:46+03:00

7.8.56
------
 * ISEARCH-6925: Настроить алерты на размер монги и количество коннектов  [ https://a.yandex-team.ru/arc/commit/8781102 ]
 * ISEARCH-6859: Восстановить тестинг поиска                              [ https://a.yandex-team.ru/arc/commit/8781073 ]

[uruz](http://staff/uruz) 2021-10-28 22:05:48+03:00

7.8.55
------
 * ISEARCH-6932: Искать всегда в последней из активных ревизий  [ https://a.yandex-team.ru/arc/commit/8776455 ]

[uruz](http://staff/uruz) 2021-10-27 19:37:50+03:00

7.8.54
------
 * ISEARCH-6913: Задержка индексации b2b Трекера  [ https://a.yandex-team.ru/arc/commit/8760553 ]

[uruz](http://staff/uruz) 2021-10-22 16:17:47+03:00

7.8.53
------
 * ISEARCH-6909: Сделать инструмент проверки жалоб (фиксы-5)  [ https://a.yandex-team.ru/arc/commit/8752522 ]

[uruz](http://staff/uruz) 2021-10-20 16:46:20+03:00

7.8.52
------
 * ISEARCH-6905: Создавать ревизии при пуше, если их ещё не существует (фикс)  [ https://a.yandex-team.ru/arc/commit/8747805 ]

[uruz](http://staff/uruz) 2021-10-19 15:18:01+03:00

7.8.51
------
 * PR from branch users/uruz/feature/ISEARCH-6909-4

ISEARCH-6909: Сделать инструмент проверки жалоб (фиксы-4)

ISEARCH-6909: Сделать инструмент проверки жалоб (фиксы-4)  [ https://a.yandex-team.ru/arc/commit/8745586 ]

[uruz](http://staff/uruz) 2021-10-18 22:40:44+03:00

7.8.50
------
 * ISEARCH-6909: Сделать инструмент проверки жалоб (фиксы-2)  [ https://a.yandex-team.ru/arc/commit/8744634 ]

[uruz](http://staff/uruz) 2021-10-18 18:16:24+03:00

7.8.49
------
 * ISEARCH-6909: Сделать инструмент проверки жалоб (фиксы)  [ https://a.yandex-team.ru/arc/commit/8744221 ]

[uruz](http://staff/uruz) 2021-10-18 16:18:59+03:00

7.8.48
------
 * ISEARCH-6909: Сделать инструмент проверки жалоб  [ https://a.yandex-team.ru/arc/commit/8739299 ]

[uruz](http://staff/uruz) 2021-10-15 18:39:39+03:00

7.8.47
------

* [uruz](http://staff/uruz)

 * ISEARCH-6906: Не создавать объекты пуша при включении неизвестного нам сервиса  [ https://a.yandex-team.ru/arc/commit/8739037 ]
 * ISEARCH-6905: Создавать ревизии при пуше, если их ещё не существует             [ https://a.yandex-team.ru/arc/commit/8739032 ]
 * ISEARCH-6908: Добавить в образ rdb-tools                                        [ https://a.yandex-team.ru/arc/commit/8737864 ]

* [shadchin](http://staff/shadchin)

 * DEVTOOLSSUPPORT-12493 Drop ResourceFinder

Текущая реализация `library.python.django.contrib.staticfiles.finders.ResourceFinder` эквивалентна `django.contrib.staticfiles.finders.FileSystemFinder`  [ https://a.yandex-team.ru/arc/commit/8711107 ]

[uruz](http://staff/uruz) 2021-10-15 18:10:25+03:00

7.8.46
------
 * ISEARCH-6872: Fix log info about headers one more time  [ https://a.yandex-team.ru/arc/commit/8699897 ]

[uruz](http://staff/uruz) 2021-10-04 19:42:18+03:00

7.8.45
------
 * ISEARCH-6872: Fix log info about headers  [ https://a.yandex-team.ru/arc/commit/8698794 ]
 * ISEARCH-6792: JSONP And Reflected XSS     [ https://a.yandex-team.ru/arc/commit/8698741 ]

[uruz](http://staff/uruz) 2021-10-04 16:08:51+03:00

7.8.44
------
 * ISEARCH-6872: Нет данных об аб тестах                      [ https://a.yandex-team.ru/arc/commit/8693398 ]
 * ISEARCH-6885: Поправить работу с ручкой стафа на тестинге  [ https://a.yandex-team.ru/arc/commit/8693396 ]

[uruz](http://staff/uruz) 2021-10-01 19:50:48+03:00

7.8.43
------
 * ISEARCH-6777: tvm for saas and some other services  [ https://a.yandex-team.ru/arc/commit/8688844 ]

[uruz](http://staff/uruz) 2021-09-30 19:19:04+03:00

7.8.42
------

* [kdunaev](http://staff/kdunaev)

 * ISEARCH-6861: Исправляю KeyError, добавляю логов  [ https://a.yandex-team.ru/arc/commit/8686816 ]

[uruz](http://staff/uruz) 2021-09-30 13:24:58+03:00

7.8.41
------
 * ISEARCH-6777: fix index  [ https://a.yandex-team.ru/arc/commit/8678820 ]

[uruz](http://staff/uruz) 2021-09-28 16:38:46+03:00

7.8.40
------
 * ISEARCH-6777: DEPLOY_STAGE_ID keyerror  [ https://a.yandex-team.ru/arc/commit/8677576 ]

[uruz](http://staff/uruz) 2021-09-28 13:38:39+03:00

7.8.39
------

* [kdunaev](http://staff/kdunaev)

 * ISEARCH-6860: Добавить сервисную авторизацию

Оказывается в коде уже есть авторизация с фековыми трекерными юидами, которые начинаются с `9...`. Добавил отдельную проверку, если передан заголовок X-Cloud-UID, берем значение из него, кладем в поле `cloud_uid`, а значение в заголовке `X-UID` не валидируем на пренадлежность фейковому диапазону. Кажется такой минимальный патч должен сработать.

Отдельно исправляю стиль-чеки, чтобы тесты были зелеными.  [ https://a.yandex-team.ru/arc/commit/8673728 ]
 * ISEARCH-6861: Добавить cloud_uid в выдачу по сотрудникам организации в коннекте

Здесь в индексацию данных о сотрудинках организации добавляется поле `cloud_uid`, затем прокидывается в сериализатор для саджеста. Тестов на сниппеты в проекте нет.
Стиль-чеки в этом пр упадут, они иправлены в другом пр.                                                                                                                                                        [ https://a.yandex-team.ru/arc/commit/8673513 ]

[uruz](http://staff/uruz) 2021-09-27 15:51:15+03:00

7.8.38
------
 * ISEARCH-6777: fix tvm config  [ https://a.yandex-team.ru/arc/commit/8667741 ]

[uruz](http://staff/uruz) 2021-09-24 18:33:56+03:00

7.8.37
------
 * ISEARCH-6777: tvm auth token + port for deploy  [ https://a.yandex-team.ru/arc/commit/8615759 ]

[uruz](http://staff/uruz) 2021-09-10 17:09:59+03:00

7.8.36
------

* [uruz](http://staff/uruz)

 * ISEARCH-6777: Edit settings to run in Y.Deploy  [ https://a.yandex-team.ru/arc/commit/8607426 ]

* [smilingleader](http://staff/smilingleader)

 * Change "calc_suggest_metrics.yql"  [ https://a.yandex-team.ru/arc/commit/8599960 ]
 * Change "calc_suggest_metrics.yql"  [ https://a.yandex-team.ru/arc/commit/8599941 ]
 * Change "calc_metrics.yql"          [ https://a.yandex-team.ru/arc/commit/8597026 ]
 * Change "calc_metrics.yql"          [ https://a.yandex-team.ru/arc/commit/8596108 ]
 * Change "calc_metrics.yql"          [ https://a.yandex-team.ru/arc/commit/8595658 ]
 * Change "calc_metrics.yql"          [ https://a.yandex-team.ru/arc/commit/8595587 ]
 * Change "calc_metrics.yql"          [ https://a.yandex-team.ru/arc/commit/8595517 ]
 * Change "calc_metrics.yql"          [ https://a.yandex-team.ru/arc/commit/8595436 ]
 * Change "calc_metrics.yql"          [ https://a.yandex-team.ru/arc/commit/8591053 ]

[uruz](http://staff/uruz) 2021-09-08 19:53:36+03:00

7.8.35
------

* [uruz](http://staff/uruz)

 * ISEARCH-6777: invert the if  [ https://a.yandex-team.ru/arc/commit/8582886 ]

* [smilingleader](http://staff/smilingleader)

 * Create file "blockstat.dict"                      [ https://a.yandex-team.ru/arc/commit/8575889 ]
 * PR from branch users/smilingleader/my-new-branch  [ https://a.yandex-team.ru/arc/commit/8575856 ]

* [zivot](http://staff/zivot)

 * notifications changed  [ https://a.yandex-team.ru/arc/commit/8562482 ]

[uruz](http://staff/uruz) 2021-09-01 21:16:24+03:00

7.8.34
------
 * ISEARCH-6777: Переезд в Y.Deploy: фикс скрипта запуска  [ https://a.yandex-team.ru/arc/commit/8557969 ]

[uruz](http://staff/uruz) 2021-08-25 17:33:10+03:00

7.8.33
------

* [uruz](http://staff/uruz)

 * ISEARCH-6777: Переезд в Y.Deploy  [ https://a.yandex-team.ru/arc/commit/8556931 ]

* [shadchin](http://staff/shadchin)

 * IGNIETFERRO-1870 Drop unnecessary tornado 4 [intranet]                                                                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/8477960 ]
 * IGNIETFERRO-1870 Auto enable pytest-tornado plugin

Раньше автоматическое подключение плагинов pytest не работало, сейчас работает, достаточно плагин добавить в PEERDIR, поэтому удалил ненужное определение `pytest_plugins`, чтобы было попроще  [ https://a.yandex-team.ru/arc/commit/8434386 ]

[uruz](http://staff/uruz) 2021-08-25 15:30:48+03:00

7.8.32
------

* [shadchin](http://staff/shadchin)

 * Move contrib/python/mockredis to contrib/deprecated/python/mockredis

mockredis больше не развивается, автор рекомендует переключиться на fakeredis

<!-- DEVEXP BEGIN -->
\****
![review](https://codereview.in.yandex-team.ru/badges/review-in_progress-yellow.svg) [![anechiporuk](https://codereview.in.yandex-team.ru/badges/anechiporuk-...-yellow.svg)](https://staff.yandex-team.ru/anechiporuk) [![kmpz](https://codereview.in.yandex-team.ru/badges/kmpz-...-yellow.svg)](https://staff.yandex-team.ru/kmpz)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/8330659 ]

* [qazaq](http://staff/qazaq)

 * Устанавливаем supervisor из pypi.y-t.ru  [ https://a.yandex-team.ru/arc/commit/8249593 ]

[zivot](http://staff/zivot) 2021-07-19 11:37:50+03:00

7.8.31
------

* [ktussh](http://staff/ktussh)

 * FEMIDA-6177:Добавить в сниппет профессий имя на английском языке  [ https://a.yandex-team.ru/arc/commit/8247517 ]

* [exprmntr](http://staff/exprmntr)

 * DEVTOOLS-7781 - remove NO_LINT()  [ https://a.yandex-team.ru/arc/commit/8097952 ]

[qazaq](http://staff/qazaq) 2021-06-08 17:47:28+03:00

7.8.30
------
 * ISEARCH-6761: meta убрана из саджеста  [ https://a.yandex-team.ru/arc_vcs/commit/1270cf83dcb77893467b0008ac14939531f56e7c ]

[zivot](http://staff/zivot) 2021-04-13 13:28:50+03:00

7.8.29
------
 * ISEARCH-6761: Язык пользователя из bb, если не передан language  [ https://a.yandex-team.ru/arc/commit/8036760 ]

[zivot](http://staff/zivot) 2021-03-31 14:08:37+03:00

7.8.28
------
 * ISEARCH-6583: add suggest header

ISEARCH-6583: add suggest header  [ https://a.yandex-team.ru/arc/commit/7964533 ]

[shigarus](http://staff/shigarus) 2021-03-19 15:38:24+03:00

7.8.27
------

* [zivot](http://staff/zivot)

 * ISEARCH-6710: monitorado b2b  [ https://a.yandex-team.ru/arc/commit/7955163 ]
 * ISEARCH-6710: monitorado      [ https://a.yandex-team.ru/arc/commit/7955149 ]

* [tavria](http://staff/tavria)

 * ISEARCH-6749: [back] Увеличить таймауты ab_info и прокинуть куку для залипания  [ https://a.yandex-team.ru/arc/commit/7953710 ]

[tavria](http://staff/tavria) 2021-03-17 15:35:56+03:00

7.8.26
------
 * ISEARCH-6728: redis mem unistat signals  [ https://a.yandex-team.ru/arc/commit/7952526 ]

[zivot](http://staff/zivot) 2021-03-16 14:55:08+03:00

7.8.25
------
 * SEARCH-6728: Мониторинг redis  [ https://a.yandex-team.ru/arc/commit/7947636 ]

[zivot](http://staff/zivot) 2021-03-15 12:29:23+03:00

7.8.24
------
 * ISEARCH-6693: Прописать YAUTH_MECHANISMS  [ https://a.yandex-team.ru/arc/commit/7922221 ]

[zivot](http://staff/zivot) 2021-03-05 03:07:08+03:00

7.8.23
------

* [tavria](http://staff/tavria)

 * ISEARCH-6723: [back] Принимать от фронта на беке test-id и передавать в разбивалку AB  [ https://a.yandex-team.ru/arc/commit/7872790 ]

* [zivot](http://staff/zivot)

 * ISEARCH-6722: Выпилить Element.getchildren()  [ https://a.yandex-team.ru/arc/commit/7872404 ]

[tavria](http://staff/tavria) 2021-02-19 17:42:51+03:00

7.8.22
------
 * ISEARCH-6717: Фикс получения страницы на другом языке  [ https://a.yandex-team.ru/arc/commit/7865138 ]

[zivot](http://staff/zivot) 2021-02-17 12:56:55+03:00

7.8.21
------
 * ISEARCH-6716: [back] Прокинуть на фронт данные по ab  [ https://a.yandex-team.ru/arc/commit/7853305 ]

[tavria](http://staff/tavria) 2021-02-15 13:10:05+03:00

7.8.20
------
 * ISEARCH-6475: Revert поддержки нескольких языков  [ https://a.yandex-team.ru/arc/commit/7852736 ]

[zivot](http://staff/zivot) 2021-02-12 13:27:30+03:00

7.8.19
------
 * ISEARCH-6419: Отдаем словоформы в саджесте  [ https://a.yandex-team.ru/arc/commit/7850166 ]

[zivot](http://staff/zivot) 2021-02-11 16:54:38+03:00

7.8.18
------
 * ISEARCH-6475: Находим документы на одном языке  [ https://a.yandex-team.ru/arc/commit/7841725 ]

[zivot](http://staff/zivot) 2021-02-09 12:48:06+03:00

7.8.17
------
 * ISEARCH-6475: Поддержать несколько языков в документации  [ https://a.yandex-team.ru/arc/commit/7840444 ]

[zivot](http://staff/zivot) 2021-02-09 00:41:20+03:00

7.8.16
------
 * ISEARCH-6698: группировка по base_url  [ https://a.yandex-team.ru/arc/commit/7825532 ]

[zivot](http://staff/zivot) 2021-02-03 12:49:53+03:00

7.8.15
------
 * ISEARCH-6676: Разбиение по заголовкам + снятие группировки  [ https://a.yandex-team.ru/arc/commit/7705567 ]

[zivot](http://staff/zivot) 2020-12-21 14:56:24+03:00

7.8.14
------
 * Revert "ISEARCH-6617: Улучшение разбиения по подзаголовкам"

[zivot](http://staff/zivot) 2020-12-18 17:04:38+03:00

7.8.13
------
 * ISEARCH-6675: Сломалась индексация readme  [ https://a.yandex-team.ru/arc/commit/7678202 ]

[zivot](http://staff/zivot) 2020-12-17 04:32:27+03:00

7.8.12
------
 * ISEARCH-6617: Улучшение разбиения по подзаголовкам  [ https://a.yandex-team.ru/arc/commit/7676155 ]
 * Change .devexp.json                                 [ https://a.yandex-team.ru/arc/commit/7645288 ]

[zivot](http://staff/zivot) 2020-12-16 14:06:50+03:00

7.8.11
------

* [shigarus](http://staff/shigarus)

 * ISEARCH-6650: fix st index  [ https://a.yandex-team.ru/arc/commit/7625419 ]

* [shadchin](http://staff/shadchin)

 * Update svn from 0.3.44 to 1.0.1  [ https://a.yandex-team.ru/arc/commit/7540949 ]

[shigarus](http://staff/shigarus) 2020-11-27 13:11:40+03:00

7.8.10
------
 * ISEARCH-6562: fix camelcase split  [ https://a.yandex-team.ru/arc/commit/7533654 ]

[shigarus](http://staff/shigarus) 2020-10-29 23:32:44+03:00

7.8.9
-----
 * ISEARCH-6618 фикс получения аватарок клуба  [ https://a.yandex-team.ru/arc/commit/7469378 ]

[tmalikova](http://staff/tmalikova) 2020-10-15 17:45:39+03:00

7.8.8
-----
 * ISEARCH-6602 фикс attachements id is not int  [ https://a.yandex-team.ru/arc/commit/7467621 ]

[tmalikova](http://staff/tmalikova) 2020-10-15 10:35:45+03:00

7.8.7
-----
 * рассчитываем на необязательность kind  [ https://a.yandex-team.ru/arc/commit/7455207 ]

[tmalikova](http://staff/tmalikova) 2020-10-12 10:59:11+03:00

7.8.6
-----
 * IESARCH-6611: fix main url dupl  [ https://a.yandex-team.ru/arc/commit/7412573 ]

[shigarus](http://staff/shigarus) 2020-09-29 21:07:27+03:00

7.8.5
-----
 * ISEARCH-6561 очередные фиксы  [ https://a.yandex-team.ru/arc/commit/7363994 ]

[tmalikova](http://staff/tmalikova) 2020-09-24 10:51:09+03:00

7.8.4
-----
 * ISEARCH-6599: Переименовать документацию YQL в поисковой выдаче  [ https://a.yandex-team.ru/arc_vcs/commit/4d88962b853c1246f9708f1b754ccdac1aac381c ]

[zivot](http://staff/zivot) 2020-09-23 16:36:50+03:00

7.8.3
-----
 * ISEARCH-6561 фикс ката с подробностями о лицензии  [ https://a.yandex-team.ru/arc/commit/7354457 ]

[tmalikova](http://staff/tmalikova) 2020-09-21 18:48:56+03:00

7.8.2
-----
 * PR from branch users/tmalikova/ISEARCH-6561__fixes

ISEARCH-6561 фикс ошибки индексации сервисов

ISEARCH-6561 фикс ошибки индексации тикетов без компонент  [ https://a.yandex-team.ru/arc/commit/7352812 ]

[tmalikova](http://staff/tmalikova) 2020-09-21 13:25:59+03:00

7.8.1
-----
 * ISEARCH-6561 фикс дефолтного сериалайзера  [ https://a.yandex-team.ru/arc/commit/7340447 ]

[tmalikova](http://staff/tmalikova) 2020-09-17 15:19:30+03:00

7.8.0
-----
 * ISEARCH-6561 поиск по ясеню  [ https://a.yandex-team.ru/arc/commit/7340109 ]

[tmalikova](http://staff/tmalikova) 2020-09-17 14:27:16+03:00

7.7.8
-----
 * ISEARCH-6525 стадия получения аватарок  [ https://a.yandex-team.ru/arc/commit/7323518 ]

[tmalikova](http://staff/tmalikova) 2020-09-11 17:03:51+03:00

7.7.7
-----
 * ISEARCH-6530 abc api v4  [ https://a.yandex-team.ru/arc/commit/7310198 ]

[tmalikova](http://staff/tmalikova) 2020-09-08 12:31:31+03:00

7.7.6
-----

* [uruz](http://staff/uruz)

 * ISEARCH-6566  [ https://a.yandex-team.ru/arc/commit/7231816 ]

[tmalikova](http://staff/tmalikova) 2020-08-18 14:43:30+03:00

7.7.5
-----

* [uruz](http://staff/uruz)

 * ISEARCH-6566: Добавить фильтр по тегу в саджест сервисов  [ https://a.yandex-team.ru/arc/commit/7207347 ]

* [zivot](http://staff/zivot)

 * ISEARCH-6565: Вовзрат на основной тестинг goals  [ https://a.yandex-team.ru/arc/commit/7183743 ]

[tmalikova](http://staff/tmalikova) 2020-08-18 13:08:11+03:00

7.7.4
-----
 * ISEARCH-6565: Проиднексировать тестовый стенд goals  [ https://a.yandex-team.ru/arc/commit/7182802 ]

[zivot](http://staff/zivot) 2020-08-06 17:19:02+03:00

7.7.3
-----
 * ISEARCH-6016 добавляем рассылки в список вертикалей  [ https://a.yandex-team.ru/arc/commit/7121801 ]

[tmalikova](http://staff/tmalikova) 2020-07-17 15:34:44+03:00

7.7.2
-----

* [shigarus](http://staff/shigarus)

 * ISEARCH-6496: api v6 connect  [ https://a.yandex-team.ru/arc/commit/7084014 ]

* [comradeandrew](http://staff/comradeandrew)

 * Contrib: separate tornado from gunicorn GEOINFRA-2117

В gunicorn использование tornado веркера является опциональным. Прямо сейчас по пирдиру на gunicorn всегда приходит tornado, причем версии 4, что делает пирдир на gunicorn не совместимым с contrib/python/motor под PY3, потому что motor пирдирит себе tornado-6.
Так как в gunicorn использовать tornado - опционально, вынес пирдир на tornado всем кто пирдирит gunicorn. Такое изменение никак не меняет поведение и никаких функциональных изменений здесь не ожидается. Все кому нужен tornado вместе с gunicorn могут делать пирдир на него отдельно.

UPD: Вынес пирдир на торнадо явно  [ https://a.yandex-team.ru/arc/commit/7068479 ]

[shigarus](http://staff/shigarus) 2020-07-06 22:22:23+03:00

7.7.1
-----
 * меняем агрегацию сигналов unistat  [ https://a.yandex-team.ru/arc/commit/6988360 ]

[tmalikova](http://staff/tmalikova) 2020-06-19 14:41:44+03:00

7.7.0
------

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6058 каталог переносов страниц  [ https://a.yandex-team.ru/arc/commit/6987267 ]

* [ignat](http://staff/ignat)

 * PR from branch users/ignat/replace_contrib_python_yt_dependency

Fix build dependency

YT-10083: Replace contrib/python/yt with yt/python/client  [ https://a.yandex-team.ru/arc/commit/6969514 ]

[tmalikova](http://staff/tmalikova) 2020-06-19 10:32:18+03:00

7.6.20
------
 * ISEARCH-6483 возврат бывших, подписавших staff_agreement, в поиск  [ https://a.yandex-team.ru/arc/commit/6945972 ]

[tmalikova](http://staff/tmalikova) 2020-06-12 15:18:21+03:00

7.6.19
------
 * ISEARCH-6492: Руководитель сервиса в саджесте  [ https://a.yandex-team.ru/arc/commit/6928407 ]

[qazaq](http://staff/qazaq) 2020-06-11 10:55:22+03:00

7.6.18
------
 * ISEARCH-6457 не индексируем junk вообще  [ https://a.yandex-team.ru/arc/commit/6890488 ]

[tmalikova](http://staff/tmalikova) 2020-06-01 10:33:41+03:00

7.6.17
------
 * ISEARCH-6457 индексируем сервисы раз в 15 минут  [ https://a.yandex-team.ru/arc/commit/6884331 ]
 * ISEARCH-6457 фикс индексации readme              [ https://a.yandex-team.ru/arc/commit/6884180 ]

[tmalikova](http://staff/tmalikova) 2020-05-29 14:27:10+03:00

7.6.16
------
 * ISEARCH-6369 обновление saas_push до последней версии  [ https://a.yandex-team.ru/arc/commit/6873032 ]

[tmalikova](http://staff/tmalikova) 2020-05-26 16:56:45+03:00

7.6.15
------
 * ISEARCH-6369 обновление клиента сааса  [ https://a.yandex-team.ru/arc/commit/6855352 ]

[tmalikova](http://staff/tmalikova) 2020-05-22 14:35:08+03:00

7.6.14
------
 * ISEARCH-6434 фикс подсветки в сниппете клубов  [ https://a.yandex-team.ru/arc/commit/6843653 ]
 * ISEARCH-6320 фикс парсинга кривых заголовков   [ https://a.yandex-team.ru/arc/commit/6843652 ]

[tmalikova](http://staff/tmalikova) 2020-05-19 11:02:02+03:00

7.6.13
------
 * ISEARCH-6421: affiliation_counters как int  [ https://a.yandex-team.ru/arc/commit/6781153 ]

[zivot](http://staff/zivot) 2020-05-13 13:16:42+03:00

7.6.12
------
 * ISEARCH-6312: Переименовал raw_content  [ https://a.yandex-team.ru/arc/commit/6778835 ]

[zivot](http://staff/zivot) 2020-05-12 17:58:06+03:00

7.6.11
------
 * ISEARCH-6421: Добавить поля в саджест по сотрудникам и группам                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           [ https://a.yandex-team.ru/arc/commit/6778087 ]
 * ISEARCH-6312: Сломалась индексация readme.md

[zivot](http://staff/zivot) 2020-05-12 15:11:08+03:00

7.6.10
------
 * ISEARCH-6366 индексируем автоматически всё, что есть на docs.yandex-team.ru
 * Убираем бейджи из описания пул реквеста                                                                                                                                                                                                                                                                                                                                                                                                                                             [ https://a.yandex-team.ru/arc/commit/6766948 ]
[tmalikova](http://staff/tmalikova) 2020-05-07 15:05:19+03:00

7.6.9
-----
 * фикс выхода за пределы int64 у dwell_time  [ https://a.yandex-team.ru/arc/commit/6755510 ]

[tmalikova](http://staff/tmalikova) 2020-04-30 18:34:44+03:00

7.6.8
-----
 * ISEARCH-6397: Обработка фильтра по зоне

[zivot](http://staff/zivot) 2020-04-29 17:40:48+03:00

7.6.7
-----
 * ISEARCH-6397: Частичная подсветка в саджесте

[zivot](http://staff/zivot) 2020-04-28 17:07:36+03:00

7.6.6
-----
 * ISEARCH-6417 проверка суперюзера для доступа в админку  [ https://a.yandex-team.ru/arc/commit/6694962 ]
 * Change .devexp.json  [ https://a.yandex-team.ru/arc/commit/6692602 ]

[tmalikova](http://staff/tmalikova) 2020-04-24 11:40:02+03:00

7.6.5
-----
 * отлавливаем AuthError в пушах этушки  [ https://a.yandex-team.ru/arc/commit/6691421 ]

[tmalikova](http://staff/tmalikova) 2020-04-23 14:19:05+03:00

7.6.4
-----
 * ISEARCH-6063 не сохраняем основной документ, если он весь делится на подразделы  [ https://a.yandex-team.ru/arc/commit/6690697 ]

[tmalikova](http://staff/tmalikova) 2020-04-23 11:28:08+03:00

7.6.3
-----
 * не индексируем весь кликхаус  [ https://a.yandex-team.ru/arc/commit/6686798 ]

[tmalikova](http://staff/tmalikova) 2020-04-22 10:19:42+03:00

7.6.2
-----
 * ISEARCH-6063 стрипаем символы абзацев в документации и правильно фильтруем всё                                                                                                                                                                                                                                                                                                                              [ https://a.yandex-team.ru/arc/commit/6684450 ]
 * настройка релизера  [ https://a.yandex-team.ru/arc/commit/6684244 ]

[tmalikova](http://staff/tmalikova) 2020-04-21 16:56:27+03:00

7.6.1
-----
 * ISEARCH-6063 переход к конкретному месту в документе  [ https://a.yandex-team.ru/arc/commit/6683563 ]
 * ISEARCH-6413 passages в саджесте документации  [ https://a.yandex-team.ru/arc/commit/6683507 ]

[tmalikova](http://staff/tmalikova) 2020-04-21 14:00:27+03:00

7.6.0
-----
 * ISEARCH-5582 отсутствия на вертикали людей и в саджесте  [ https://a.yandex-team.ru/arc/commit/6682993 ]

[tmalikova](http://staff/tmalikova) 2020-04-21 10:48:16+03:00

7.5.4
-----
 * ISEARCH-6377 берём фасет из s_product, а не из component_name  [ https://a.yandex-team.ru/arc/commit/6671209 ]

[tmalikova](http://staff/tmalikova) 2020-04-16 18:11:13+03:00

7.5.3
-----
 * ISEARCH-6399 фикс потерянного слага сервиса в саджесте групп  [ https://a.yandex-team.ru/arc/commit/6662567 ]

[tmalikova](http://staff/tmalikova) 2020-04-14 11:59:34+03:00

7.5.2
-----
 * ISEARCH-6391 одинаковое название статуса в фильтре и сниппете  [ https://a.yandex-team.ru/arc/commit/6604574 ]

[tmalikova](http://staff/tmalikova) 2020-04-10 15:47:04+03:00

7.5.1
-----
 * ISEARCH-6391 саджест по abc сервисам  [ https://a.yandex-team.ru/arc/commit/6601327 ]

[tmalikova](http://staff/tmalikova) 2020-04-09 16:31:05+03:00

7.5.0
-----

* [qazaq](http://staff/qazaq)

 * ISEARCH-6262: Новые факторы по ABC сервисам

Переписал индексатор сервисов. Добавлены новые факторы.
Нужно ещё сделать сам отдельный саджест по сервисам.

Открытые вопросы:
1. Предлагалось считать клики по сервисам. Есть нюанс, что все клики сейчас собираются только для вертикали "всё" и для входящих в неё вертикалей. Вроде добавить туда сервисы не дорого. Но я этого пока не делал.
2. Вопрос по ranking_factors (TODO)
  [ https://a.yandex-team.ru/arc/commit/6596591 ]

[tmalikova](http://staff/tmalikova) 2020-04-08 12:45:09+03:00

7.4.0
-----
 * ISEARCH-6335 поиск для облачных пользователей  [ https://a.yandex-team.ru/arc/commit/6589970 ]
 * Change .devexp.json  [ https://a.yandex-team.ru/arc/commit/6583445 ]

[tmalikova](http://staff/tmalikova) 2020-04-07 14:19:59+03:00

7.3.0
-----
 * ISEARCH-6344: Пользовательский фактор "часто ищу человека"  [ https://a.yandex-team.ru/arc/commit/6557992 ]

[qazaq](http://staff/qazaq) 2020-04-02 12:58:37+03:00

7.2.7
-----
 * AUDTOOL-463 поисковый саджест в аудите  [ https://a.yandex-team.ru/arc/commit/6545537 ]

[tmalikova](http://staff/tmalikova) 2020-03-30 15:22:18+03:00

7.2.6
-----
 * ISEARCH-6263 добавила поле position в саджест по людям  [ https://a.yandex-team.ru/arc/commit/6543545 ]

[tmalikova](http://staff/tmalikova) 2020-03-29 20:32:43+03:00

7.2.5
-----
 * индексации вики на отдельной компоненте  [ https://a.yandex-team.ru/arc/commit/6538721 ]
 * Change .devexp.json  [ https://a.yandex-team.ru/arc/commit/6524135 ]

[tmalikova](http://staff/tmalikova) 2020-03-27 13:35:20+03:00

7.2.4
-----
 * ISEARCH-6351 чиним удаление ревизий в админке  [ https://a.yandex-team.ru/arc/commit/6518845 ]

[tmalikova](http://staff/tmalikova) 2020-03-24 11:27:23+03:00

7.2.3
-----
 * ISEARCH-6295 Перейти на новые параметры ручки поиска тикетов в Трекере  [ https://a.yandex-team.ru/arc/commit/6513159 ]

[aksenovma](http://staff/aksenovma) 2020-03-20 15:24:52+03:00

7.2.2
-----
 * ISEARCH-6347 misspell fix  [ https://a.yandex-team.ru/arc/commit/6512772 ]

[tmalikova](http://staff/tmalikova) 2020-03-20 13:06:00+03:00

7.2.1
-----

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6347 чиним индексацию вики в b2b  [ https://a.yandex-team.ru/arc/commit/6512519 ]

* [qazaq](http://staff/qazaq)

 * ISEARCH-6332: Поправил поиск публичных вики-страниц в b2b  [ https://a.yandex-team.ru/arc/commit/6512491 ]

[qazaq](http://staff/qazaq) 2020-03-20 12:10:38+03:00

7.2.0
------

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6338 группировочные атрибуты и факторы
 * ISEARCH-6347 отправляем в переводчик сразу текстовый контент

* [qazaq](http://staff/qazaq)

 * Линтер

[tmalikova](http://staff/tmalikova) 2020-03-19 15:21:04+03:00

7.1.9
-----
 * ISEARCH-6332: Поправил опечатку в s_type  [ https://a.yandex-team.ru/arc/commit/6497789 ]

[qazaq](http://staff/qazaq) 2020-03-17 17:27:40+03:00

7.1.8
-----
 * ISEARCH-6332: Не показываем публичные страницы вики тем, у кого к ним нет доступа  [ https://a.yandex-team.ru/arc/commit/6496419 ]

[qazaq](http://staff/qazaq) 2020-03-17 12:38:11+03:00

7.1.7
-----
 * swap24 в саджесте  [ https://a.yandex-team.ru/arc/commit/6481682 ]
 * ISEARCH-6316 не падаем при таймауте календаря и не перетираем translated из кеша  [ https://a.yandex-team.ru/arc/commit/6481474 ]

[tmalikova](http://staff/tmalikova) 2020-03-12 17:37:37+03:00

7.1.6
-----
 * ISEARCH-6316 поиск по переведённой вики  [ https://a.yandex-team.ru/arc/commit/6473060 ]

[tmalikova](http://staff/tmalikova) 2020-03-11 13:55:04+03:00

7.1.5
-----

* [monory](http://staff/monory)

 * [CONTRIB-1727] Move Tornado to django-way differentiation of lib versions

[CONTRIB-1727] Add Tornado 6.0.3 for Py3  [ https://a.yandex-team.ru/arc/commit/6455462 ]

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6229 обрезаем поисковый запрос  [ https://a.yandex-team.ru/arc/commit/6471139 ]

[tmalikova](http://staff/tmalikova) 2020-03-10 19:57:11+03:00

7.1.4
-----
 * ретраим отвалившиеся запросы в idm.rolenodes  [ https://a.yandex-team.ru/arc/commit/6453876 ]

[tmalikova](http://staff/tmalikova) 2020-03-04 13:09:27+03:00

7.1.3
-----
 * кешируем поход за acl в фемиду  [ https://a.yandex-team.ru/arc/commit/6451021 ]

[tmalikova](http://staff/tmalikova) 2020-03-03 16:59:53+03:00

7.1.2
-----
 * оптимизация запросов в idm.rolenodes при индексации  [ https://a.yandex-team.ru/arc/commit/6449790 ]

[tmalikova](http://staff/tmalikova) 2020-03-03 13:03:56+03:00

7.1.1
-----
 * ISEARCH-6323 правильная проверка на длину атрибутов  [ https://a.yandex-team.ru/arc/commit/6437587 ]
 * фикс 500 из-за родовой травмы стаффа  [ https://a.yandex-team.ru/arc/commit/6437574 ]

[tmalikova](http://staff/tmalikova) 2020-02-28 15:29:10+03:00

7.1.0
-----

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6315 индексируем переведенную документацию  [ https://a.yandex-team.ru/arc/commit/6433987 ]

* [danielzhe](http://staff/danielzhe)

 * SUBBOTNIK-3370 Move yenv, python-blackboxer to arcadia common library  [ https://a.yandex-team.ru/arc/commit/6394727 ]

[tmalikova](http://staff/tmalikova) 2020-02-27 16:21:54+03:00

7.0.8
-----

* [ndtretyak](http://staff/ndtretyak)

 * IDM-9135: Не забирать total_count при каждом запросе

* [tmalikova](http://staff/tmalikova)

 * Change .devexp.json

[ndtretyak](http://staff/ndtretyak) 2020-02-18 12:06:13+03:00

7.0.7
-----
 * ISEARCH-6081 доработки для качества людей

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-complete-green.svg) ![qazaq](https://codereview.common-int.yandex-team.ru/badges/qazaq-ok-green.svg) ![feakuru](https://codereview.common-int.yandex-team.ru/badges/feakuru-ok-green.svg)
<!-- DEVEXP END -->                                                                                                             [ https://a.yandex-team.ru/arc/commit/6373711 ]
 * ISEARCH-6092 фикс 500 при пустом запросе с пустым query

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-in_progress-yellow.svg) ![stampi](https://codereview.common-int.yandex-team.ru/badges/stampi-ok-green.svg) ![qazaq](https://codereview.common-int.yandex-team.ru/badges/qazaq-...-yellow.svg) ![aksenovma](https://codereview.common-int.yandex-team.ru/badges/aksenovma-ok-green.svg)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6373702 ]

[tmalikova](http://staff/tmalikova) 2020-02-14 16:49:29+03:00

7.0.6
-----
 * ISEARCH-5951: Оптимизация индексатора клубов Этушки  [ https://a.yandex-team.ru/arc/commit/6353623 ]

[qazaq](http://staff/qazaq) 2020-02-11 13:27:50+03:00

7.0.5
-----

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6054 заменяем зонный фильтр на более строгий                                [ https://a.yandex-team.ru/arc/commit/6344778 ]
 * доработки collect_factors_for_poll

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/6335186 ]
 * доработки collect_factors_for_poll

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/6334542 ]

* [qazaq](http://staff/qazaq)

 * Очередной леммер (успешно собирается на маке)  [ https://a.yandex-team.ru/arc/commit/6343474 ]

[tmalikova](http://staff/tmalikova) 2020-02-07 17:05:10+03:00

7.0.4
-----
 * доработка collect_factors_for_pool                               [ https://a.yandex-team.ru/arc/commit/6334485 ]
 * правильно передаём jsonfactors, чтобы они попадали в reqans лог  [ https://a.yandex-team.ru/arc/commit/6334310 ]

[tmalikova](http://staff/tmalikova) 2020-02-06 13:19:45+03:00

7.0.3
-----
 * ISEARCH-6296 пушей директории  [ https://a.yandex-team.ru/arc/commit/6331707 ]

[tmalikova](http://staff/tmalikova) 2020-02-05 14:17:29+03:00

7.0.2
-----
 * ISEARCH-6296 фикс внешней документации  [ https://a.yandex-team.ru/arc/commit/6331318 ]

[tmalikova](http://staff/tmalikova) 2020-02-05 12:50:07+03:00

7.0.1
-----
 * ISEARCH-6296 фикс индексации кондуктора и людей  [ https://a.yandex-team.ru/arc/commit/6329765 ]

[tmalikova](http://staff/tmalikova) 2020-02-04 20:31:05+03:00

7.0.0
------

* [qazaq](http://staff/qazaq)

 * PR from branch users/qazaq/py3

Python 3: Поправили получение лемм + включили catboost

Python 3: dict.keys() -> list(dict) + чиним тесты

Python-3: httplib -> requests, cPickle -> pickle

Python-3: xrange -> range, long -> int, force_unicode -> force_str

Python-3: zip, filter, reduce

Python-3: print, map, exc.message, iter*, unicode -> str

Python-3: urlparse -> urllib.parse + jabber  [ https://a.yandex-team.ru/arc/commit/6328702 ]

[tmalikova](http://staff/tmalikova) 2020-02-04 16:26:43+03:00

6.15.4
------

* [tmalikova](http://staff/tmalikova)

 * фиксы метрик и админки  [ https://a.yandex-team.ru/arc/commit/6307632 ]

* [sidorovaa](http://staff/sidorovaa)

 * Remove duplicate PY_SRCS/TEST_SRCS (DEVTOOLS-5213)  [ https://a.yandex-team.ru/arc/commit/6304974 ]

[tmalikova](http://staff/tmalikova) 2020-01-31 11:29:25+03:00

6.15.3
------
 * фикс 500 в саджесте трекера  [ https://a.yandex-team.ru/arc/commit/6267874 ]

[tmalikova](http://staff/tmalikova) 2020-01-29 18:05:28+03:00

6.15.2
------
 * ISEARCH-6278 костыльный фикс поиска с пустым поисковым запросом  [ https://a.yandex-team.ru/arc/commit/6267011 ]

[tmalikova](http://staff/tmalikova) 2020-01-29 15:11:53+03:00

6.15.1
------
 * ISEARCH-6278 костыльный фикс поиска с пустым поисковым запросом  [ https://a.yandex-team.ru/arc/commit/6266124 ]

[tmalikova](http://staff/tmalikova) 2020-01-29 12:27:02+03:00

6.15.0
------
 * ISEARCH-6016 вертикаль поиска по рассылкам  [ https://a.yandex-team.ru/arc/commit/6263761 ]

[tmalikova](http://staff/tmalikova) 2020-01-29 11:33:35+03:00

6.14.2
------
 * черный список очередей для индексации  [ https://a.yandex-team.ru/arc/commit/6259967 ]

[tmalikova](http://staff/tmalikova) 2020-01-27 17:05:31+03:00

6.14.1
------
 * ISEARCH-6251: Замена s_suggest на поиск по зоне  [ https://a.yandex-team.ru/arc/commit/6250320 ]

[qazaq](http://staff/qazaq) 2020-01-24 15:59:44+03:00

6.14.0
-------
 * ISEARCH-6089 простые метрики саджеста на stat  [ https://a.yandex-team.ru/arc/commit/6236354 ]

[tmalikova](http://staff/tmalikova) 2020-01-21 13:40:09+03:00

6.13.19
-------
 * ISEARCH-6274: Логин и пароль от mongo держим отдельно от строки соединения в celery  [ https://a.yandex-team.ru/arc/commit/6217847 ]

[qazaq](http://staff/qazaq) 2020-01-15 22:08:01+03:00

6.13.18
-------
 * ISEARCH-6274: Логин и пароль от mongo держим отдельно от строки соединения  [ https://a.yandex-team.ru/arc/commit/6216047 ]

[qazaq](http://staff/qazaq) 2020-01-15 20:06:41+03:00

6.13.17
-------
 * временно выключаем индексацию документации каждый час  [ https://a.yandex-team.ru/arc/commit/6209658 ]

[tmalikova](http://staff/tmalikova) 2020-01-14 18:40:26+03:00

6.13.16
-------
 * ISEARCH-5962 разные формулы для разных слоёв саджеста  [ https://a.yandex-team.ru/arc/commit/6209547 ]

[tmalikova](http://staff/tmalikova) 2020-01-14 18:17:42+03:00

6.13.15
-------
 * разумные таймауты в регулярных индексациях    [ https://a.yandex-team.ru/arc/commit/6207821 ]
 * оптимизация расписания регулярных индексаций  [ https://a.yandex-team.ru/arc/commit/6201617 ]

[tmalikova](http://staff/tmalikova) 2020-01-14 11:55:20+03:00

6.13.14
-------
 * оптимизация расписания регулярных индексаций

[tmalikova](http://staff/tmalikova) 2020-01-10 18:02:24+03:00

6.13.13
-------
 * ISEARCH-6279 fields в параметрах abc  [ https://a.yandex-team.ru/arc/commit/6200953 ]

[tmalikova](http://staff/tmalikova) 2020-01-10 15:43:24+03:00

6.13.12
-------
 * ISEARCH-6246 Обрезать длину описания на вертикали трекера  [ https://a.yandex-team.ru/arc/commit/6155695 ]

[aksenovma](http://staff/aksenovma) 2019-12-26 19:14:45+03:00

6.13.11
-------
 * ISEARCH-6252 component_name из разметки и фикс дублирования страниц  [ https://a.yandex-team.ru/arc/commit/6151232 ]

[tmalikova](http://staff/tmalikova) 2019-12-25 14:32:09+03:00

6.13.10
-------
 * перезапуск пушей с дефолтным приоритетом  [ https://a.yandex-team.ru/arc/commit/6130244 ]

[tmalikova](http://staff/tmalikova) 2019-12-18 17:50:05+03:00

6.13.9
------
 * ISEARCH-6245 фикс перевода ts в datetime в вики и подобных местах  [ https://a.yandex-team.ru/arc/commit/6129516 ]

[tmalikova](http://staff/tmalikova) 2019-12-17 17:05:43+03:00

6.13.8
------
 * ISEARCH-6018: Оказывается, по умолчанию запросы запускаются с версией 0

[qazaq](http://staff/qazaq) 2019-12-16 19:39:58+03:00

6.13.7
------
 * ISEARCH-6018: Мои комменты на русском в YQL всё сломали

[qazaq](http://staff/qazaq) 2019-12-16 19:04:47+03:00

6.13.6
------
 * ISEARCH-6018: Дата может быть датой, а может быть строкой

[qazaq](http://staff/qazaq) 2019-12-16 18:11:14+03:00

6.13.5
------
 * Ещё один бесполезный релиз, чтобы проверить make

[qazaq](http://staff/qazaq) 2019-12-16 17:22:38+03:00

6.13.4
------
 * Проверочный релиз через make

[qazaq](http://staff/qazaq) 2019-12-16 16:41:48+03:00

6.13.3
------
 * ISEARCH-6018: Поправил шаблонизацию YQL-запроса  [ https://a.yandex-team.ru/arc/commit/6126526 ]

[qazaq](http://staff/qazaq) 2019-12-16 16:20:41+03:00

6.13.2
------
 * ISEARCH-6018: YQL-запросы в SQLv1  [ https://a.yandex-team.ru/arc/commit/6103496 ]

[qazaq](http://staff/qazaq) 2019-12-16 13:39:02+03:00

6.13.1
------

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6088 слоезависимые фичи  [ https://a.yandex-team.ru/arc/commit/6024060 ]

* [aksenovma](http://staff/aksenovma)

 * ISEARCH-6231 Фикс рекурсивного вызова  [ https://a.yandex-team.ru/arc/commit/6024063 ]

[tmalikova](http://staff/tmalikova) 2019-11-29 19:19:14+03:00

6.13.0
------

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6088 урлы с редиректом в саджестах  [ https://a.yandex-team.ru/arc/commit/6023461 ]

* [aksenovma](http://staff/aksenovma)

 * ISEARCH-6231 Ограничения для роботов в саджесте людей  [ https://a.yandex-team.ru/arc/commit/6022913 ]

[tmalikova](http://staff/tmalikova) 2019-11-29 16:49:03+03:00

6.12.11
-------
 * ISEARCH-6226 улучшаем логирование  [ https://a.yandex-team.ru/arc/commit/6014594 ]

[tmalikova](http://staff/tmalikova) 2019-11-27 15:32:05+03:00

6.12.10
-------
 * ISEARCH-6226 фильтруем на всё в зависимости от permissions  [ https://a.yandex-team.ru/arc/commit/6007917 ]

[tmalikova](http://staff/tmalikova) 2019-11-25 16:29:19+03:00

6.12.9
------
 * yqlv1 в индексации readme

[tmalikova](http://staff/tmalikova) 2019-11-25 10:28:10+03:00

6.12.8
------
 * ISEARCH-6234 чиним индексацию документации  [ https://a.yandex-team.ru/arc/commit/5995598 ]

[tmalikova](http://staff/tmalikova) 2019-11-22 18:21:10+03:00

6.12.7
------
 * ISEARCH-6221 - даём пользователю найти себя  [ https://a.yandex-team.ru/arc/commit/5925042 ]

[tmalikova](http://staff/tmalikova) 2019-11-15 10:31:54+03:00

6.12.6
------
 * ISEARCH-6079 не подсвечиваем click_urls  [ https://a.yandex-team.ru/arc/commit/5924066 ]

[tmalikova](http://staff/tmalikova) 2019-11-14 19:41:50+03:00

6.12.5
------
 * ISEARCH-6070 sitemap url fixes  [ https://a.yandex-team.ru/arc/commit/5923762 ]

[tmalikova](http://staff/tmalikova) 2019-11-14 18:21:32+03:00

6.12.4
------
 * ISEARCH-6070 правильно парсим урлы в sitemap.xml  [ https://a.yandex-team.ru/arc/commit/5923151 ]

[tmalikova](http://staff/tmalikova) 2019-11-14 16:05:00+03:00

6.12.3
------
 * ISEARCH-6066 фикс саджестов в b2b  [ https://a.yandex-team.ru/arc/commit/5919745 ]

[tmalikova](http://staff/tmalikova) 2019-11-13 15:20:32+03:00

6.12.2
------
 * ISEARCH-6070 фикс проверки на наличие url  [ https://a.yandex-team.ru/arc/commit/5918736 ]

[tmalikova](http://staff/tmalikova) 2019-11-13 09:57:00+03:00

6.12.1
-----
 * ISEARCH-6066 опечатка в GroupPermissionStep

[tmalikova](http://staff/tmalikova) 2019-11-12 17:33:17+03:00

6.12.0
------

* [mirabu](http://staff/mirabu)

 * ISEARCH-6070: Использовать sitemap для индексации документации  [ https://a.yandex-team.ru/arc/commit/5908172 ]
 * ISEARCH-6079 Подсветка в саджесте                               [ https://a.yandex-team.ru/arc/commit/5908171 ]

* [tmalikova](http://staff/tmalikova)

 * ISEARCH-6065 не пятисотим из-за кривых данных в стафф  [ https://a.yandex-team.ru/arc/commit/5908401 ]
 * ISEARCH-6066 ручка и step проверки permissions         [ https://a.yandex-team.ru/arc/commit/5908175 ]

[tmalikova](http://staff/tmalikova) 2019-11-12 16:20:17+03:00

6.11.6
------
 * ISEARCH-6065 Перенес ACL по Стафф за фичу  [ https://a.yandex-team.ru/arc/commit/5907764 ]

[aksenovma](http://staff/aksenovma) 2019-11-12 13:50:18+03:00

6.11.5
------
 * ISEARCH-6065 Поправлен suggest по пользователям  [ https://a.yandex-team.ru/arc/commit/5905585 ]

[aksenovma](http://staff/aksenovma) 2019-11-11 17:35:24+03:00

6.11.4
------
 * ISEARCH-6065 фикс error_acl  [ https://a.yandex-team.ru/arc/commit/5904253 ]

[tmalikova](http://staff/tmalikova) 2019-11-11 11:14:25+03:00

6.11.3
------
 * ISEARCH-6065 Доработки после тестирования  [ https://a.yandex-team.ru/arc/commit/5900722 ]

[aksenovma](http://staff/aksenovma) 2019-11-08 18:06:17+03:00

6.11.2
------
 * ISEARCH-6065 фиксы  [ https://a.yandex-team.ru/arc/commit/5883755 ]

[tmalikova](http://staff/tmalikova) 2019-11-01 10:42:05+03:00

6.11.1
------
 * PR from branch users/tmalikova/ISEARCH-6065__staff_access

ISEARCH-6065 фикс тестов + немного косметики

ISEARCH-6065 Поправил фикстуру

ISEARCH-6065 Убрал лишний степ

ISEARCH-6065 Доработки по ревью

ISEARCH-6065 Забыл указать ручку Стаффа

ISEARCH-6065 Разграничение доступа к вертикали Стафф

ISEARCH-6065 Атрибут group_id в индексаторе людей  [ https://a.yandex-team.ru/arc/commit/5882923 ]

[tmalikova](http://staff/tmalikova) 2019-10-31 20:53:45+03:00

6.11.0
------
 * [ISEARCH-6068 Ошибки при индексации st. [ https://a.yandex-team.ru/arc/commit/5881193 ]
 * ISEARCH-6073 подключаем django-idm-api  [ https://a.yandex-team.ru/arc/commit/5881191 ]

[tmalikova](http://staff/tmalikova) 2019-10-31 13:43:42+03:00

6.10.5
------
 * ISEARCH-6017 TVM2 в индексации описаний рассылок  [ https://a.yandex-team.ru/arc/commit/5879083 ]

[mirabu](http://staff/mirabu) 2019-10-30 17:17:44+03:00


6.10.3
------
 * ISEARCH-6057 Саджест по документации.  [ https://a.yandex-team.ru/arc/commit/5874600 ]

[mirabu](http://staff/mirabu) 2019-10-29 12:24:49+03:00

6.10.2
-----
* ISEARCH-6074 не пользуемся больше count в abc [ https://a.yandex-team.ru/arc/commit/5862310 ]

[tmalikova](http://staff/tmalikova) 2019-10-28 17:27:55+03:00

6.10.1
-----
 * ISEARCH-5954 фикс ValueError: Unicode strings with encoding declaration are not supported [ https://a.yandex-team.ru/arc/commit/5861126 ]

[tmalikova](http://staff/tmalikova) 2019-10-28 10:19:55+03:00

6.10.0
-----
 * ISEARCH-6057 Саджест по документации.  [ https://a.yandex-team.ru/arc/commit/5857278 ]

[mirabu](http://staff/mirabu) 2019-10-25 15:21:55+03:00

6.9.1
-----
ISEARCH-6059 Переключил джобу extract_links на кэш таблицы.  [ https://a.yandex-team.ru/arc/commit/5846601 ]

[mirabu](http://staff/mirabu) 2019-10-22 11:54:55+03:00

6.9.0
-----
 * ISEARCH-5979 Не зажигаем мониторинг для пушей удалённых организаций.                [ https://a.yandex-team.ru/arc/commit/5829182 ]

[mirabu](http://staff/mirabu) 2019-10-16 15:00:16+03:00

6.8.1
-----
 * ISEARCH-6039 Добавил стадию кэширования для этушки, трекера, вики, документации.  [ https://a.yandex-team.ru/arc/commit/5803833 ]

[mirabu](http://staff/mirabu@yandex-team.ru) 2019-10-09 18:00:00+03:00

6.8.0
-----
 * ISEARCH-6039 Добавил стадию кэширования для этушки, трекера, вики, документации.  [ https://a.yandex-team.ru/arc/commit/5802932 ]

[mirabu](http://staff/mirabu@yandex-team.ru) 2019-10-09 15:30:00+03:00

6.7.1
-----
 * ISEARCH-6044 Добавлена зона кликабельных запросов для readme  [ https://a.yandex-team.ru/arc/commit/5786410 ]

[mirabu](http://staff/mirabu@yandex-team.ru) 2019-10-03 10:00:00+03:00

6.7.0
-----
 * ISEARCH-6038 ранжирование колдунщиков с помощью cb модели  [ https://a.yandex-team.ru/arc/commit/5757280 ]

[tmalikova](http://staff/tmalikova) 2019-09-27 15:33:36+03:00

6.6.6
-----
 *  ISEARCH-6041 включение регулярной переиндексации документации  [ https://a.yandex-team.ru/arc/commit/5691451 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-20 14:05:00+03:00

6.6.4
-----
 *  ISEARCH-5072 фикс парсинга блоков кода  [ https://a.yandex-team.ru/arc/commit/5690846 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-20 14:05:00+03:00

6.6.2
-----
 *  Убрал параметр external=False при создании таблицы в джобе extract_links [ https://a.yandex-team.ru/arc/commit/5690375 ]
 *  PR from branch users/tmalikova/ISEARCH-5072__fixes [ https://a.yandex-team.ru/arc/commit/5690194 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-19 11:04:00+03:00

6.6.1
-----
 *  ISEARCH-5072 фикс startup.sh [ https://a.yandex-team.ru/arc/commit/5690088 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-20 10:04:00+03:00

6.6.0
-----
 *  ISEARCH-5072 Добавлен индексатор Readme [ https://a.yandex-team.ru/arc/commit/5684410 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-19 11:04:00+03:00


6.5.9
-----
 *  ISEARCH-5991 индексация вики, трекера и этушки через logbroker [ https://a.yandex-team.ru/arc/commit/5663641 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-16 11:03:00+03:00

6.5.8
-----
 *  ISEARCH-5991 обновление бинаря сааса

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-11 17:54:00+03:00

6.5.7
-----
 *  ISEARCH-6035 дополнительные фильтры в саджесте idm [ https://a.yandex-team.ru/arc/commit/5644968 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-11 11:25:00+03:00

6.5.6
-----
 *  ISEARCH-6030 увеличиваем таймауты в этушку [ https://a.yandex-team.ru/arc/commit/5639210 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-09-10 10:09:00+03:00

6.5.5
-----
 *  ISEARCH-5810: Добавил локальный хост вики [ https://a.yandex-team.ru/arc/commit/5625779 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-09-05 14:10:00+03:00

6.5.4
-----
 *  ISEARCH-5810: Отдаём meta в саджесте, только если запрос пришёл с wiki [ https://a.yandex-team.ru/arc/commit/5605131 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-09-04 02:00:00+03:00

6.5.3
-----
 *  ISEARCH-6026: Используем новый путь до файла blockstat в YQL [ https://a.yandex-team.ru/arc/commit/5604886 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-09-03 23:00:00+03:00

6.5.2
-----
 *  ISEARCH-5810 Отдаём фичи uaas в саджесте для wiki [ https://a.yandex-team.ru/arc/commit/5604546 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-09-03 20:30:00+03:00

6.5.1
-------
 *  ISEARCH-6015 Уволенные в поиске vol.2 [ https://a.yandex-team.ru/arc/commit/5528573 ]

[Shoshin Boris](http://staff/mirabu@yandex-team.ru) 2019-08-23 14:10:00+03:00

6.5.0
-------
 *  ISEARCH-5967 настройки prestable инстанса

[Malikova Taisiya](http://staff/tmalikova@yandex-team.ru) 2019-08-23 13:14:00+03:00

6.4.1
-------
 *  ISEARCH-5466 tvm2 в индексации трекера [ https://a.yandex-team.ru/arc/commit/5518263 ]

[Shoshin Boris](http://staff/mirabu@yandex-team.ru) 2019-08-22 13:20:00+03:00

6.4.0
-------
 *  ISEARCH-6009 Управление направлением сортировки [ https://a.yandex-team.ru/arc/commit/5514978 ]

[Shoshin Boris](http://staff/mirabu@yandex-team.ru) 2019-08-21 15:40:00+03:00

6.3.4
-------
 *  ISEARCH-5914 Добавлена выдача колдунщика оборудования по запросам printer, scanner, fax и регулярке prn-* [ https://a.yandex-team.ru/arc/commit/5461913 ]

[Shoshin Boris](http://staff/mirabu@yandex-team.ru) 2019-08-15 12:51:00+03:00

6.3.3
-------
 * ISEARCH-5974 В индексатор plan services добавленно ID в поиск. [ https://a.yandex-team.ru/arc/commit/5458279 ]

[Shoshin Boris](http://staff/mirabu@yandex-team.ru) 2019-08-15 12:51:00+03:00

6.3.2
-------
 * ISEARCH-5974 В индексатор plan services добавленно ID в поиск. [ https://a.yandex-team.ru/arc/commit/5451274 ]

[Shoshin Boris](http://staff/mirabu@yandex-team.ru) 2019-08-14 12:20:00+03:00

6.3.1
-------
 * ISEARCH-5779 чиним срабатывание колдунщиков [ https://a.yandex-team.ru/arc/commit/5449836 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-13 18:05:00+03:00

6.3.0
-------
 * ISEARCH-5955 Сделано удаление переговорок с флагом is_deleted=True и с office.is_deleted=True. Убран фильтр по is_bookable=true. Добавлен mock тест [ https://a.yandex-team.ru/arc/commit/5448848 ]

[Shoshin Boris](http://staff/mirabu@yandex-team.ru) 2019-08-13 14:18:00+03:00

6.2.7
-------
 * ISEARCH-5779 не фейлим пуши для удалённых постов [ https://a.yandex-team.ru/arc/commit/5448546 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-13 12:27:00+03:00

6.2.6
-------
 * ISEARCH-5779 фикс пушей at.posts [ https://a.yandex-team.ru/arc/commit/5448400 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-13 12:27:00+03:00

6.2.5
-------
 * ISEARCH-5779 fix replace_yauser [ https://a.yandex-team.ru/arc/commit/5448262 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-13 11:57:00+03:00

6.2.4
-------
 * ISEARCH-5779 доработки по индексации из кеша [ https://a.yandex-team.ru/arc/commit/5448157 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-13 11:26:00+03:00

6.2.3
-------
 * ISEARCH-5779 доработки для load в индексаторе этушки [ https://a.yandex-team.ru/arc/commit/5446362 ]
 * ISEARCH-5779 доработки для load в индексаторе этушки [ https://a.yandex-team.ru/arc/commit/5446174 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-12 17:33:00+03:00

6.2.2
-------
 * ISEARCH-5779 подмешиваем за фичей этушку во всё [ https://a.yandex-team.ru/arc/commit/5445762 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-12 15:16:00+03:00

6.2.1
-------
 * ISEARCH-5779 скрытая вертикаль новой этушки [ https://a.yandex-team.ru/arc/commit/5441641 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-09 19:00:00+03:00

6.2.0
-------
 * ISEARCH-5779 новый индексатор этушки [ https://a.yandex-team.ru/arc/commit/5441264 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-09 18:14:00+03:00

6.1.3
-------
 * ISEARCH-5995 фикс fielddate в отчётах [ https://a.yandex-team.ru/arc/commit/5421713 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-02 14:32:00+03:00

6.1.2
-------
 * ISEARCH-5995 yql команды по аркадийному [ https://a.yandex-team.ru/arc/commit/5420990 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-08-02 10:54:00+03:00

6.1.1
-------
 * экспорт yt команд из правильного места [ https://a.yandex-team.ru/arc/commit/5379573 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-30 10:45:00+03:00

6.1.0
-------
 * ISEARCH-5987 разделяем фичи для фильтрации и скрытия инфы с карточки уволенных [ https://a.yandex-team.ru/arc/commit/5371778 ]
 * переиндексируем весь стафф раз в час [ https://a.yandex-team.ru/arc/commit/5371946 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-29 16:50:00+03:00

6.0.1
-------
 * ISEARCH-5960 фикс проблемы с индексацией трекера [ https://a.yandex-team.ru/arc/commit/5371279 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-29 13:07:00+03:00

6.0.0
-------
 * ISEARCH-5960 переезд в Аркадию  [ https://a.yandex-team.ru/arc/commit/5370454 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-29 10:41:00+03:00

5.35.16
-------
 * ISEARCH-5925 убираем хак удаления нод по старому урлу  [ https://github.yandex-team.ru/tools/intrasearch/commit/7d6a3c6a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-24 17:55:06+03:00

5.35.15
-------
 * новые пользователи админки            [ https://github.yandex-team.ru/tools/intrasearch/commit/30a1a951 ]
 * ISEARCH-5925 фильтры по датам в keys  [ https://github.yandex-team.ru/tools/intrasearch/commit/f872a540 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-23 14:36:05+03:00

5.35.14
-------
 * ISEARCH-5973 ограничиваем максимальное кол-во групп  [ https://github.yandex-team.ru/tools/intrasearch/commit/438226bd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-17 17:18:46+03:00

5.35.13
-------
 * ISEARCH-5972 фильтрация по is_memorial (#681)  [ https://github.yandex-team.ru/tools/intrasearch/commit/e6ef4e4f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-16 17:45:31+03:00

5.35.12
-------
 * ISEARCH-5969 фикс ошибок в cachedhttpstep (#680)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0d7a1cb2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-15 14:58:00+03:00

5.35.11
-------
 * ISEARCH-5969 чиним фичи в саджесте + небольшая уборка (#679)  [ https://github.yandex-team.ru/tools/intrasearch/commit/99ed2451 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-13 12:15:51+03:00

5.35.10
-------
 * ISEARCH-5969: Добавил FeaturesStep в саджест в isearch  [ https://github.yandex-team.ru/tools/intrasearch/commit/17fa5935 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-07-12 20:09:38+03:00

5.35.9
------
 * ISEARCH-5969: РКН - попытка №3  [ https://github.yandex-team.ru/tools/intrasearch/commit/94686403 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-07-12 19:33:14+03:00

5.35.8
------
 * ISEARCH-5969: Забыл вызвать apply_acl  [ https://github.yandex-team.ru/tools/intrasearch/commit/710e6fd8 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-07-12 19:23:00+03:00

5.35.7
------
 * ISEARCH-5969: РКН  [ https://github.yandex-team.ru/tools/intrasearch/commit/c80cdf1b ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-07-12 18:49:52+03:00

5.35.6
------
 * ISEARCH-5950 расширяем cors для b2b (#677)  [ https://github.yandex-team.ru/tools/intrasearch/commit/a793595c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-11 15:42:42+03:00

5.35.5
------
 * ISEARCH-5925 добавляем произвольные фильтры в idm rolenodes  [ https://github.yandex-team.ru/tools/intrasearch/commit/81729a04 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-11 14:28:49+03:00

5.35.4
------
 * ISEARCH-5929 переходим на настоящий id в idm_rolenodes (#676)  [ https://github.yandex-team.ru/tools/intrasearch/commit/41970ab1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-10 13:35:59+03:00

5.35.3
------
 * ISEARCH-5929 аккуратнее удаляем узлы с дублирующимися slug_path  [ https://github.yandex-team.ru/tools/intrasearch/commit/11383ea6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-01 17:03:18+03:00

5.35.2
------
 * ISEARCH-5929 не удаляем детей в случае удаления узла во время переиндексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/05e950a9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-01 15:50:44+03:00

5.35.1
------
 * ISEARCH-5929 удаление удаленных узлов из индекса в idm.rolenodes (#675)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9fd0f32f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-07-01 11:01:05+03:00

5.35.0
------
 * ISEARCH-5931 английская версия департамента в саджесте idm_users (#674)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7048bf5d ]
 * ISEARCH-5876 отдаём click_urls в саджесте (#673)                         [ https://github.yandex-team.ru/tools/intrasearch/commit/8ca83993 ]
 * ISEARCH-5956 переход на factory_boy (#671)                               [ https://github.yandex-team.ru/tools/intrasearch/commit/5ab4fc87 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-28 12:38:09+03:00

5.34.0
------
 * ISEARCH-5937 ходим напрямую в хосты pgaas (#670)  [ https://github.yandex-team.ru/tools/intrasearch/commit/e0954344 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-20 10:39:17+03:00

5.33.16
-------
 * ISEARCH-5857 фикс авторизации по tvm2 в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/b5b28340 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-06 12:42:51+03:00

5.33.15
-------
 * ISEARCH-5940 убираем cache в DirectoryStep  [ https://github.yandex-team.ru/tools/intrasearch/commit/70da066c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-05 23:11:52+03:00

5.33.14
-------
 * ISEARCH-5940 фикс неправильного кеша в DirectoryStep  [ https://github.yandex-team.ru/tools/intrasearch/commit/9fcacf2a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-05 21:57:19+03:00

5.33.13
-------
 * ISEARCH-5926 увеличиваем flush_limit  [ https://github.yandex-team.ru/tools/intrasearch/commit/9e55581a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-04 10:59:56+03:00

5.33.12
-------
 * ISEARCH-5926 упрощаем обработку пушей - меньше записей в базу  [ https://github.yandex-team.ru/tools/intrasearch/commit/c4984050 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-04 10:31:29+03:00

5.33.11
-------
 * ISEARCH-5926 упрощаем обработку пушей - меньше записей в базу  [ https://github.yandex-team.ru/tools/intrasearch/commit/095d7a3f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-03 18:41:09+03:00

5.33.10
-------
 * ISEARCH-5926 упрощаем обработку пушей - меньше записей в базу  [ https://github.yandex-team.ru/tools/intrasearch/commit/837bfec5 ]
 * ISEARCH-5926 упрощаем обработку пушей - меньше записей в базу  [ https://github.yandex-team.ru/tools/intrasearch/commit/027b915a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-03 18:14:42+03:00

5.33.9
------
 * ISEARCH-5926 переходим на схему с локами  [ https://github.yandex-team.ru/tools/intrasearch/commit/70988118 ]
 * возвращаю кеши в индексацию документации  [ https://github.yandex-team.ru/tools/intrasearch/commit/5f98b3c9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-06-03 16:44:29+03:00

5.33.8
------
 * ISEARCH-5926 поднимаем таймаут логброкеру  [ https://github.yandex-team.ru/tools/intrasearch/commit/5e6f0e96 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-30 19:39:37+03:00

5.33.7
------
 * ISEARCH-5926 флашим чаще, чем коммитим  [ https://github.yandex-team.ru/tools/intrasearch/commit/be9ab2c8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-29 17:50:39+03:00

5.33.6
------
 * ISEARCH-5926 коммитим отдельно каждый батч  [ https://github.yandex-team.ru/tools/intrasearch/commit/16932bd7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-29 17:10:46+03:00

5.33.5
------
 * ISEARCH-5926 уменьшаем timeout  [ https://github.yandex-team.ru/tools/intrasearch/commit/f946f4d5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-29 16:05:43+03:00

5.33.4
------
 * ISEARCH-5926 блокировка на listen_tracker  [ https://github.yandex-team.ru/tools/intrasearch/commit/4b350940 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-29 12:55:07+03:00

5.33.3
------
 * ISEARCH-5926 блокировка на listen_tracker  [ https://github.yandex-team.ru/tools/intrasearch/commit/fe354bc0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-29 12:33:30+03:00

5.33.2
------
 * ISEARCH-5926 уменьшаем messages_limit  [ https://github.yandex-team.ru/tools/intrasearch/commit/239fbc44 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-29 12:24:59+03:00

5.33.1
------
 * фикс ferryman_merge_doc_table  [ https://github.yandex-team.ru/tools/intrasearch/commit/476362ba ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-28 19:02:36+03:00

5.33.0
------
 * ISEARCH-5926 переходим на официальный клиент LB (#668)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0e56c80f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-28 18:49:10+03:00

5.32.3
------
 * ISEARCH-5926 фиксы кеширования  [ https://github.yandex-team.ru/tools/intrasearch/commit/0fa76350 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-28 17:19:20+03:00

5.32.2
------
 * ISEARCH-5926 фиксы передачи x-org-id  [ https://github.yandex-team.ru/tools/intrasearch/commit/45084b79 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-28 16:58:41+03:00

5.32.1
------
 * ISEARCH-5926 фиксы передачи x-org-id  [ https://github.yandex-team.ru/tools/intrasearch/commit/66a2c686 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-28 15:05:22+03:00

5.32.0
------
 * ISEARCH-5927 меняем логику получения org_id директории (#669)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9c67e31a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-28 13:40:32+03:00

5.31.1
------
 * улучшаем логирование проблем с tvm  [ https://github.yandex-team.ru/tools/intrasearch/commit/2f08b459 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-24 09:56:49+03:00

5.31.0
------
 * ISEARCH-5922 меняем атрибут паспорта 1011 на 1017 в b2b (#667)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c6ddaf6f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-05-17 13:59:19+03:00

5.30.4
------
 * ISEARCH-5862 loglevel info для saas_push  [ https://github.yandex-team.ru/tools/intrasearch/commit/9396a9ab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-29 18:35:14+03:00

5.30.3
------
 * ISEARCH-5862  мониторинг демона saas (#666)  [ https://github.yandex-team.ru/tools/intrasearch/commit/907c9b72 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-29 18:12:23+03:00

5.30.2
------
 * ISEARCH-5885 фикс кеша в doc  [ https://github.yandex-team.ru/tools/intrasearch/commit/8f7e0e23 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-25 17:40:22+03:00

5.30.1
------
 * ISEARCH-5909 отключаем индексацию через логброкер для goals  [ https://github.yandex-team.ru/tools/intrasearch/commit/3af81454 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-23 14:26:54+03:00

5.30.0
------
 * ISEARCH-5901 переделка ContentTrigger (#663)  [ https://github.yandex-team.ru/tools/intrasearch/commit/74e6b200 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-22 15:34:25+03:00

5.29.8
------
 * ISEARCH-5903 чистка админки (#665)                  [ https://github.yandex-team.ru/tools/intrasearch/commit/7835efc0 ]
 * ISEARCH-5878 убираем ненужный парсинг xml response  [ https://github.yandex-team.ru/tools/intrasearch/commit/c9f9a5de ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-19 10:58:34+03:00

5.29.7
------
 * ISEARCH-5900 обновляем saas_push и конфиги  [ https://github.yandex-team.ru/tools/intrasearch/commit/58c78b4a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-18 17:51:51+03:00

5.29.6
------
 * ISEARCH-5900 обновляем saas_push и конфиги (#664)  [ https://github.yandex-team.ru/tools/intrasearch/commit/fd488fde ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-18 17:07:26+03:00

5.29.5
------
 * ISEARCH-5900 временно отключаем индексацию через логброкер  [ https://github.yandex-team.ru/tools/intrasearch/commit/8053a0e4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-17 17:46:57+03:00

5.29.4
------
 * ISEARCH-5888 ходим с tvm2 и из decider  [ https://github.yandex-team.ru/tools/intrasearch/commit/473b1ea1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-12 14:03:25+03:00

5.29.3
------
 * ISEARCH-5893 фикс ура в doc_count  [ https://github.yandex-team.ru/tools/intrasearch/commit/8a1cca31 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-12 13:23:55+03:00

5.29.2
------
 * ISEARCH-5893 фикс вызова get_doc_count                         [ https://github.yandex-team.ru/tools/intrasearch/commit/65d2b2d7 ]
 * ISEARCH-5888 ходим в saas с сервисным tvm2 тикетом из админки  [ https://github.yandex-team.ru/tools/intrasearch/commit/a31fe7c4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-11 19:59:18+03:00

5.29.1
------
 * ISEARCH-5888 ходим в saas с сервисным tvm2 тикетом из админки  [ https://github.yandex-team.ru/tools/intrasearch/commit/65587dde ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-11 19:31:34+03:00

5.29.0
------
 * ISEARCH-5893 переносим get_docs_count в isearch (#661)     [ https://github.yandex-team.ru/tools/intrasearch/commit/5ed18880 ]
 * ISEARCH-5888 ходим в saas с сервисным tvm2 тикетом (#662)  [ https://github.yandex-team.ru/tools/intrasearch/commit/700b7817 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-11 19:03:18+03:00

5.28.3
------
 * ISEARCH-5890 убираем logstash хэндлер и упрощаем настройки логирования (#660)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7aa0ed18 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-09 16:56:55+03:00

5.28.2
------
 * ISEARCH-5886 cors для конструктора форм в b2b (#659)  [ https://github.yandex-team.ru/tools/intrasearch/commit/98bca1c4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-04 13:42:18+03:00

5.28.1
------
 * ISEARCH-5869 потерянный импорт  [ https://github.yandex-team.ru/tools/intrasearch/commit/3ae8e12a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-02 17:12:37+03:00

5.28.0
------
 * ISEARCH-5869 названия в сажестах idm по частям (#658)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7a134f4b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-02 12:22:12+03:00

5.27.16
-------
 * ISEARCH-5882 доработки по внешней документации  [ https://github.yandex-team.ru/tools/intrasearch/commit/1b178896 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-04-01 15:09:28+03:00

5.27.15
-------
 * SAAS-5008 регулярки goals, invite, equipment через lb  [ https://github.yandex-team.ru/tools/intrasearch/commit/653e014a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-29 16:51:20+03:00

5.27.14
-------
 * SAAS-5008 регулярные переиндексации целей, оборудования и переговорок через логброкер  [ https://github.yandex-team.ru/tools/intrasearch/commit/c79b45c6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-29 14:22:31+03:00

5.27.13
-------
 * SAAS-5008 цели через логброкер  [ https://github.yandex-team.ru/tools/intrasearch/commit/a9a0b7d4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-29 14:00:07+03:00

5.27.12
-------
 * SAAS-5008 переговорки и оборудование через логброкер  [ https://github.yandex-team.ru/tools/intrasearch/commit/a54a644d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-29 13:51:36+03:00

5.27.11
-------
 * ISEARCH-5866 update saas_push (#657)  [ https://github.yandex-team.ru/tools/intrasearch/commit/26b041e5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-29 12:35:15+03:00

5.27.10
-------
 * ISEARCH-5874 настраиваем мониторинг acl  [ https://github.yandex-team.ru/tools/intrasearch/commit/ff936ff2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-26 18:38:12+03:00

5.27.9
------
 * ISEARCH-5874 настраиваем мониторинг acl  [ https://github.yandex-team.ru/tools/intrasearch/commit/f5ea721c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-26 18:17:34+03:00

5.27.8
------
 * ISEARCH-5874 настраиваем мониторинг acl (#656)  [ https://github.yandex-team.ru/tools/intrasearch/commit/cb2ec8d3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-26 17:31:31+03:00

5.27.7
------
 * ISEARCH-5873 откат временного фикса  [ https://github.yandex-team.ru/tools/intrasearch/commit/773cefcd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-26 16:07:42+03:00

5.27.6
------
 * ISEARCH-5873 фикс, чтобы прикрыть дырку  [ https://github.yandex-team.ru/tools/intrasearch/commit/f006efd7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-26 15:56:55+03:00

5.27.5
------
 * фикс индексации clicked marked urls  [ https://github.yandex-team.ru/tools/intrasearch/commit/e579eb0c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-25 18:26:12+03:00

5.27.4
------
 * ISEARCH-5861 фикс сниппета директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/27126331 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-19 17:47:17+03:00

5.27.3
------
 * ISEARCH-5861 улучшение логирования стадий индексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/1efd6e68 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-19 16:53:25+03:00

5.27.2
------
 * ISEARCH-5861 фикс парсинга сниппетов  [ https://github.yandex-team.ru/tools/intrasearch/commit/314e2530 ]
 * ISEARCH-5861 фикс парсинга сниппетов  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e997750 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-19 16:21:04+03:00

5.27.1
------
 * ISEARCH-5861 фикс контекста  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e4516f4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-19 15:53:45+03:00

5.27.0
------
 * ISEARCH-5861 schematics 1.0.4 -> 2.1.0 (#655)  [ https://github.yandex-team.ru/tools/intrasearch/commit/78f2c478 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-19 14:20:02+03:00

5.26.9
------
 * ISEARCH-5848 сортировка фасетов вики в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/76a6302f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-19 13:11:09+03:00

5.26.8
------
 * ISEARCH-5848 "упрощаем" поиск по фасетам (#654)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3753213b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-19 12:45:03+03:00

5.26.7
------
 * ISEARCH-5858 фикс 500 при невозможности распарсить запрос для подсветки (#653)  [ https://github.yandex-team.ru/tools/intrasearch/commit/aba966c3 ]
 * фикс фильтра в idm                                                              [ https://github.yandex-team.ru/tools/intrasearch/commit/64573f2a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-03-14 11:24:51+03:00

5.26.5
------
 * фикс ошибок из-за дат в doc  [ https://github.yandex-team.ru/tools/intrasearch/commit/08abdf04 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-27 18:59:52+03:00

5.26.4
------
 * ISEARCH-5839 фикс рестартов  [ https://github.yandex-team.ru/tools/intrasearch/commit/6c41657f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-27 16:45:47+03:00

5.26.3
------
 * ISEARCH-5839 убираем intrasearch-wiki2  [ https://github.yandex-team.ru/tools/intrasearch/commit/1703254c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-27 16:42:47+03:00

5.26.2
------
 * ISEARCH-5839 фикс конфига для прода  [ https://github.yandex-team.ru/tools/intrasearch/commit/bdd3ae70 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-27 16:26:15+03:00

5.26.1
------
 * ISEARCH-5839 явно создаём etc/saas  [ https://github.yandex-team.ru/tools/intrasearch/commit/1ba4c953 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-27 11:03:58+03:00

5.26.0
------
 * ISEARCH-5839 заливка в саас через логброкер (#652)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8f6a7f92 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-27 10:47:54+03:00

5.25.6
------
 * ISEARCH-5843 фикс подсчета метрик  [ https://github.yandex-team.ru/tools/intrasearch/commit/e0f53d88 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-22 12:45:20+03:00

5.25.5
------
 * ISEARCH-5843 используем только x-request-id  [ https://github.yandex-team.ru/tools/intrasearch/commit/8c807da9 ]
 * ISEARCH-5843 тесты на request_id             [ https://github.yandex-team.ru/tools/intrasearch/commit/e3e048f2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-21 11:36:56+03:00

5.25.4
------
 * ISEARCH-5843 проставляем везде X-Request-Id и берем его из заголовков  [ https://github.yandex-team.ru/tools/intrasearch/commit/06fbcad0 ]
 * ISEARCH-5843 фикс разных мелочей                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/3980f93a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-21 11:22:56+03:00

5.25.3
------
 * ISEARCH-5843 lower логина при запросе стафф групп  [ https://github.yandex-team.ru/tools/intrasearch/commit/be7ed32c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-19 18:07:32+03:00

5.25.2
------
 * ISEARCH-5843 lower логина при запросе стафф групп  [ https://github.yandex-team.ru/tools/intrasearch/commit/dc965726 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-19 18:00:42+03:00

5.25.1
------
 * ISEARCH-5680 фикс дублирования языка  [ https://github.yandex-team.ru/tools/intrasearch/commit/9f986f5f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-19 15:40:15+03:00

5.25.0
------
 * ISEARCH-5680 ходим в вики с tvm2 (#651)  [ https://github.yandex-team.ru/tools/intrasearch/commit/d7ac7ecf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-19 13:46:16+03:00

5.24.3
------
 * небольшие фиксы для стабильности  [ https://github.yandex-team.ru/tools/intrasearch/commit/e99b5f94 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-18 12:53:16+03:00

5.24.2
------
 * фикс kill_duplicate_pushes  [ https://github.yandex-team.ru/tools/intrasearch/commit/11194a79 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-15 14:43:55+03:00

5.24.1
------
 * ISEARCH-5817 фикс приоритетов  [ https://github.yandex-team.ru/tools/intrasearch/commit/ecd545b4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-14 11:34:56+03:00

5.24.0
------
 * ISEARCH-5817 обновляем celery (#650)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0a9d5eb1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-13 12:17:15+03:00

5.23.8
------
 * фикс индексации вики в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/0a295880 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-12 18:56:45+03:00

5.23.7
------
 * фикс индексации вики в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/814e2afb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-12 18:41:05+03:00

5.23.6
------
 * фикс индексации вики в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/0d092c18 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-12 17:35:35+03:00

5.23.5
------
 * ISEARCH-5829 фикс 500 в апи пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/413b8bd8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-11 15:43:25+03:00

5.23.4
------
 * ISEARCH-5829 убиваем одинаковые пуши и пробуем всё индексировать глобавльно у директории (#649)  [ https://github.yandex-team.ru/tools/intrasearch/commit/741066a0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-11 12:46:07+03:00

5.23.3
------
 * ISEARCH-5834 фикс индексации документации                          [ https://github.yandex-team.ru/tools/intrasearch/commit/d9ddd3ef ]
 * ISEARCH-5829 пишем время чека при постановке задачи на индексацию  [ https://github.yandex-team.ru/tools/intrasearch/commit/0b588dc9 ]
 * ISEARCH-5829 фикс ошибок бд                                        [ https://github.yandex-team.ru/tools/intrasearch/commit/ab35ac11 ]
 * ISEARCH-5829 параллельные чеки и фикс чистки статусов              [ https://github.yandex-team.ru/tools/intrasearch/commit/70eeb80f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-08 15:16:26+03:00

5.23.2
------
 * ISEARCH-5816 убираем yauth из апи  [ https://github.yandex-team.ru/tools/intrasearch/commit/e35f92d9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-05 17:19:42+03:00

5.23.1
------
 * ISEARCH-5816 фиксы по само тестированию  [ https://github.yandex-team.ru/tools/intrasearch/commit/7b33de21 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-05 17:01:46+03:00

5.23.0
------
 * ISEARCH-5816  django 1.11 (#648)  [ https://github.yandex-team.ru/tools/intrasearch/commit/fabb4a69 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-02-05 16:09:16+03:00

5.22.1
------
 * ISEARCH-5780 load в глобальную очередь  [ https://github.yandex-team.ru/tools/intrasearch/commit/cfad2015 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-25 12:25:09+03:00

5.22.0
------
 * ISEARCH-5780 учимся индексировать из кеша вики, трекер и этушку (#645)  [ https://github.yandex-team.ru/tools/intrasearch/commit/5ac37d87 ]
 * ISEARCH-5736 удаляем собственную обвзяку для логов и метрик (#647)      [ https://github.yandex-team.ru/tools/intrasearch/commit/85359c60 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-25 11:22:27+03:00

5.21.6
------
 * ISEARCH-5749: Десериализуем контекст лока  [ https://github.yandex-team.ru/tools/intrasearch/commit/ec500552 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-01-23 15:57:34+03:00

5.21.5
------
 * Поправил конфиг ylock             [ https://github.yandex-team.ru/tools/intrasearch/commit/25e89f2f ]
 * Разные команды для релиза в прод  [ https://github.yandex-team.ru/tools/intrasearch/commit/513c15ca ]
 * Команды для релиза                [ https://github.yandex-team.ru/tools/intrasearch/commit/0673613a ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-01-23 14:56:37+03:00

5.21.4
------
 * Попытка выкатки №2

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-01-22 19:04:50+03:00

5.21.3
------
 * ISEARCH-5749: Локи через mongodb  [ https://github.yandex-team.ru/tools/intrasearch/commit/f9a74406 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2019-01-22 18:53:04+03:00

5.21.2
------
 * ISEARCH-5602 настройка softness через фичи (#643)  [ https://github.yandex-team.ru/tools/intrasearch/commit/957152c3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-21 19:28:23+03:00

5.20.2
------
 * ISEARCH-5807 фикс хедера x-org-id  [ https://github.yandex-team.ru/tools/intrasearch/commit/5d418ea1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-21 16:10:19+03:00

5.20.1
------
 * фикс удаления вики документов в YT  [ https://github.yandex-team.ru/tools/intrasearch/commit/9496bc88 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-21 14:33:19+03:00

5.20.0
------
 * ISEARCH-5807 чистка от вьюх и явно ненужных зависимостей (#642)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c076ec0a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-17 17:20:32+03:00

5.19.12
-------
 * ISEARCH-5811 удаляем страницы вики правильно (#641)  [ https://github.yandex-team.ru/tools/intrasearch/commit/941226c1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-16 14:48:10+03:00

5.19.11
-------
 * ISEARCH-5786 вариант с не считать клики под катами в колдунщиках (#640)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2e232e0e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-15 11:19:04+03:00

5.19.10
-------
 * ISEARCH-5808 фикс проверки длины максимального поискового атрибута  [ https://github.yandex-team.ru/tools/intrasearch/commit/f91d990b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-15 10:32:10+03:00

5.19.9
------
 * ISEARCH-5747 фикс подчеркивания в подсветке (#639)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2cb41e58 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2019-01-11 12:26:59+03:00

5.19.8
------
 * ISEARCH-5793 фикс 500 из-за отстуствия полей в апи стаффа (#638)  [ https://github.yandex-team.ru/tools/intrasearch/commit/fe799d97 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-12-26 16:01:45+03:00

5.19.7
------
 * ISEARCH-5783 уменьшаем вес колдунщику людей при совпадении не по фио/логину  [ https://github.yandex-team.ru/tools/intrasearch/commit/53220035 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-12-18 14:50:09+03:00

5.19.6
------
 * ISEARCH-5715 команда сборки факторов для пула (#637)  [ https://github.yandex-team.ru/tools/intrasearch/commit/81e2a3c5 ]
 * Update .devexp.json                                   [ https://github.yandex-team.ru/tools/intrasearch/commit/d72a266f ]
 * Update .devexp.json                                   [ https://github.yandex-team.ru/tools/intrasearch/commit/e0d2ad1d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-12-13 13:06:48+03:00

5.19.5
------
 * ISEARCH-5443 фикс урлов для логов селери  [ https://github.yandex-team.ru/tools/intrasearch/commit/46cd3c66 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-12-05 12:53:02+03:00

5.19.4
------
 * ISEARCH-5260 увеличиваем количество дней до 60  [ https://github.yandex-team.ru/tools/intrasearch/commit/0adbbab8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-12-04 20:09:44+03:00

5.19.3
------
 * ISEARCH-5260 зоны с кликабельными и оцененными поисковыми запросами (#636)  [ https://github.yandex-team.ru/tools/intrasearch/commit/1b1c47e5 ]
 * Update .devexp.json                                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/558a2f3a ]
 * Update .devexp.json                                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/9c3616ab ]
 * Update .devexp.json                                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/db55b39c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-12-04 19:51:57+03:00

5.19.2
------
 * ISEARCH-5755 выводим сервисы в людях (#635)  [ https://github.yandex-team.ru/tools/intrasearch/commit/dd9f42ec ]
 * обновила конфиг ревьюшницы                   [ https://github.yandex-team.ru/tools/intrasearch/commit/3d2aa650 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-29 12:38:33+03:00

5.19.1
------
 * ISEARCH-5742 берем название из title страницы для внутренней документации (#634)  [ https://github.yandex-team.ru/tools/intrasearch/commit/44a941ec ]
 * ISEARCH-5752 экспорт оценок в YT (#633)                                           [ https://github.yandex-team.ru/tools/intrasearch/commit/1d5f58f7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-28 16:39:51+03:00

5.19.0
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5682: Новый хост директории b2b в тестинге (#632)  [ https://github.yandex-team.ru/tools/intrasearch/commit/cc54b4b0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-26 18:46:36+03:00

5.18.14
-------
 * не переиндексируем всё подряд в yt  [ https://github.yandex-team.ru/tools/intrasearch/commit/7ed306ba ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-22 14:58:42+03:00

5.18.13
-------
 * ISEARCH-5697 фикс фейла при урлах с кириллицей  [ https://github.yandex-team.ru/tools/intrasearch/commit/e3999721 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-21 14:34:27+03:00

5.18.12
-------
 * фикс завершения индексации с excpected_docs  [ https://github.yandex-team.ru/tools/intrasearch/commit/fd00edde ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-21 11:49:37+03:00

5.18.11
-------
 * ISEARCH-5705 учимся индексировать дельту людей директории (#631)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6678b5ea ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-21 11:37:44+03:00

5.18.10
-------
 * ISEARCH-5720 передаем зону в template при запросе в saas в candidatesearch (#629)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7465f0b1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-21 11:08:43+03:00

5.18.9
------
 * ISEARCH-5697 фикс удаления  [ https://github.yandex-team.ru/tools/intrasearch/commit/3dd1a55a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-20 15:43:38+03:00

5.18.8
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5697: Удаляем удаленные группы из индекса (#630)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3ab04c92 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * фикс падающего теста  [ https://github.yandex-team.ru/tools/intrasearch/commit/7953f1e6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-20 15:15:07+03:00

5.18.7
------
 * ISEARCH-5706 добавляем регулярные переиндексации всех пользователей и групп idm  [ https://github.yandex-team.ru/tools/intrasearch/commit/d698f688 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-19 11:37:43+03:00

5.18.6
------
 * ISEARCH-5007 фикс yql  [ https://github.yandex-team.ru/tools/intrasearch/commit/743508d4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-16 15:50:55+03:00

5.18.5
------
 * ISEARCH-5007 запрещаем адресацию на внутреннюю вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/06337852 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-16 15:41:32+03:00

5.18.4
------
 * ISEARCH-5007 запрещаем адресацию на внутреннюю вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/574afcec ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-16 15:38:29+03:00

5.18.3
------
 * ISEARCH-5646: В индексациях апи сравнивать количество проиндексированного с count в апи (#627)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3d6b6056 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-16 14:41:06+03:00

5.18.2
------
 * ISEARCH-5007 пустых фикс заголовков  [ https://github.yandex-team.ru/tools/intrasearch/commit/4a768db5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-16 13:41:30+03:00

5.18.1
------
 * ISEARCH-5725 убираем startrek из настроек  [ https://github.yandex-team.ru/tools/intrasearch/commit/7eb06277 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-16 10:36:43+03:00

5.18.0
------
 * ISEARCH-5007 удаляем старую локацию из индекса при получении 301/302 (#625)                      [ https://github.yandex-team.ru/tools/intrasearch/commit/cecaf542 ]
 * выключаем tail_searchlog и export_searchlog - кибана не работает, данные берем из другого места  [ https://github.yandex-team.ru/tools/intrasearch/commit/cf6c6e0b ]
 * ISEARCH-5725 убираем подпорки под несколько сервисов трекера (#626)                              [ https://github.yandex-team.ru/tools/intrasearch/commit/5edf033b ]
 * ISEARCH-5734 подключаем ревьюшницу (#628)                                                        [ https://github.yandex-team.ru/tools/intrasearch/commit/7591f7e2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-15 17:35:44+03:00

5.17.10
-------
 * ISEARCH-5681 не запрашиваем все сервисы в индексации дельт  [ https://github.yandex-team.ru/tools/intrasearch/commit/f08ac38a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-13 17:01:35+03:00

5.17.9
------
 * ISEARCH-5681 не запрашиваем все сервисы в индексации дельт  [ https://github.yandex-team.ru/tools/intrasearch/commit/4f1acc44 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-09 14:47:13+03:00

5.17.8
------
 * ISEARCH-5681 не запрашиваем все сервисы в индексации дельт  [ https://github.yandex-team.ru/tools/intrasearch/commit/17990aad ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-09 14:14:28+03:00

5.17.7
------
 * ISEARCH-5681 лок таймаут ещё меньше  [ https://github.yandex-team.ru/tools/intrasearch/commit/d63eb330 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-09 12:47:52+03:00

5.17.6
------
 * ISEARCH-5681 дельты в людях и логи (#624)  [ https://github.yandex-team.ru/tools/intrasearch/commit/741a50bb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-08 16:05:23+03:00

5.17.5
------
 * ISEARCH-5739 подпорка под отсутствие части имени в директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/7da6f467 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-08 15:04:53+03:00

5.17.4
------
 * ISEARCH-5716 заменяем z_base на z_femida_name при поиске по ФИО в кан… (#623)  [ https://github.yandex-team.ru/tools/intrasearch/commit/5931a32e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-08 11:44:47+03:00

5.17.3
------
 * ISEARCH-5703 удаляем пуши по частям (#622)  [ https://github.yandex-team.ru/tools/intrasearch/commit/68864967 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-07 15:58:25+03:00

5.17.2
------
 * ISEARCH-5626 фикс каунтера в саджесте (#621)  [ https://github.yandex-team.ru/tools/intrasearch/commit/a6fef6da ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-11-06 12:22:05+03:00

5.17.1
------
 * ISEARCH-5728 меняем поход в uaas (#620)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9123b1c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-10-31 16:45:04+03:00

5.17.0
------
 * ISEARCH-5640 оптимизируем место в базе (#619)               [ https://github.yandex-team.ru/tools/intrasearch/commit/8adf234 ]
 * удаляю trendbox.yml из мастера до нормальной его настройки  [ https://github.yandex-team.ru/tools/intrasearch/commit/cff6229 ]
 * тесты на trendbox                                           [ https://github.yandex-team.ru/tools/intrasearch/commit/d88f98e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-10-26 13:40:14+03:00

5.16
----

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5677: Поддерживаем в Вики "несколько авторов страницы" (#617)  [ https://github.yandex-team.ru/tools/intrasearch/commit/5bf3076 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5624 временный фикс слишком длинных значений  [ https://github.yandex-team.ru/tools/intrasearch/commit/7330423 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-10-19 18:26:45+03:00

5.15.7
------
 * ISEARCH-5624 доработки для нового сервиса стартрека (#616)  [ https://github.yandex-team.ru/tools/intrasearch/commit/fdb40e3 ]
 * тесты на trendbox                                           [ https://github.yandex-team.ru/tools/intrasearch/commit/631dfbe ]
 * тесты на trendbox                                           [ https://github.yandex-team.ru/tools/intrasearch/commit/084fb34 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-10-18 16:06:22+03:00

5.15.6
------
 * ISEARCH-5686 используем констрейнты для поиска по именам в кандидатах (#615)  [ https://github.yandex-team.ru/tools/intrasearch/commit/94fa574 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-10-10 16:20:28+03:00

5.15.5
------
 * изменения в ferryman_merge_doc_tables  [ https://github.yandex-team.ru/tools/intrasearch/commit/c79b6fa ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-10-09 11:09:32+00:00

5.15.4
------
 * ISEARCH-5686: Новый поисковый запрос для поиска по ФИО  [ https://github.yandex-team.ru/tools/intrasearch/commit/8fff1856 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-10-05 12:26:50+03:00

5.15.3
------
 * ISEARCH-5686: Вернул старую структуру документа candidatesearch  [ https://github.yandex-team.ru/tools/intrasearch/commit/5b8453f2 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-10-04 14:05:45+03:00

5.15.2
------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5651 оптимизация получения ссылок во время индексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/2f94bead ]
 * ISEARCH-5577 храним пуши в b2b дольше                          [ https://github.yandex-team.ru/tools/intrasearch/commit/5c1294d0 ]

[Kirill Kartashov](http://staff/qazaq@yandex-team.ru) 2018-09-26 16:52:11+03:00

5.15.1
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * FEMIDA-5621: При поиске кандидатов Фемиды распознаем ФИО и ищем явно по ним (#613)  [ https://github.yandex-team.ru/tools/intrasearch/commit/381b0bc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-19 12:58:15+03:00

5.15.0
------
 * ISEARCH-5627 автоподсчет метрик на yql и загрузка их в статистику (#612)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8e15bc7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-19 12:55:26+03:00

5.14.4
------
 * ISEARCH-5577 ещё логов  [ https://github.yandex-team.ru/tools/intrasearch/commit/9e10eda ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-18 20:18:59+03:00

5.14.3
------
 * ISEARCH-5577 добавляем логирования изменения статуса пушей с рестарами  [ https://github.yandex-team.ru/tools/intrasearch/commit/38fe25a ]
 * не удаляем ревизии из saasdocumentstorage                               [ https://github.yandex-team.ru/tools/intrasearch/commit/d3807da ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-18 19:37:40+03:00

5.14.2
------
 * ISEARCH-5668 не флашим таблицы в ferryman если индексация сфейлилась  [ https://github.yandex-team.ru/tools/intrasearch/commit/d8e5e66 ]
 * ISEARCH-5668 глобальная настрока skip_revision_check                  [ https://github.yandex-team.ru/tools/intrasearch/commit/d7ec195 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-18 12:18:39+03:00

5.14.1
------
 * чистим временные таблицы в merge_doc_tables при ошибке  [ https://github.yandex-team.ru/tools/intrasearch/commit/9f85e09 ]
 * WIKI-11337 включаем переиндексацию вики                 [ https://github.yandex-team.ru/tools/intrasearch/commit/75f46b5 ]
 * WIKI-11337 отключаем переиндексацию вики                [ https://github.yandex-team.ru/tools/intrasearch/commit/18d22c8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-16 15:39:28+03:00

5.14.0
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5532: Саджест по очередям трекера в b2b (#610)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2eccc9c ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5533 - доработка апи пушей + апи синхронизации директории (#609)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7f71dc3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-13 15:33:44+03:00

5.13.9
------
 * cors для dev вики в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/6017e23 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-12 19:52:40+03:00

5.13.8
------
 * учимся исключать пользователей из эксперимента  [ https://github.yandex-team.ru/tools/intrasearch/commit/9c47756 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-07 17:49:58+03:00

5.13.7
------
 * выключаем пуши фемиды в yt  [ https://github.yandex-team.ru/tools/intrasearch/commit/cd2e8f7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-07 12:03:04+03:00

5.13.6
------
 * ISEARCH-5624 отказоустойчивость в массовой переиндексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/11e1c6c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-06 16:47:50+03:00

5.13.5
------
 * ISEARCH-5259 фикс получения пути таблицы  [ https://github.yandex-team.ru/tools/intrasearch/commit/c946f8c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-06 15:53:16+03:00

5.13.4
------
 * ISEARCH-5259 прячем ссылочные факторы за флаг  [ https://github.yandex-team.ru/tools/intrasearch/commit/2dbd513 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-06 14:13:49+03:00

5.13.3
------
 * ISEARCH-5259 восстанавливаем кросссылочные факторы (#608)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3da5fe7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-05 15:38:36+03:00

5.13.2
------
 * ISEARCH-5617 shadow_revision в массовой переиндексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/4276b9b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-05 14:52:22+03:00

5.13.1
------
 * ISEARCH-5617 рефакторинг send_push_table (#607)  [ https://github.yandex-team.ru/tools/intrasearch/commit/582857d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-09-05 11:32:01+00:00

5.13.0
------
 * ISEARCH-5590 меняем местами оценки в выдаче  [ https://github.yandex-team.ru/tools/intrasearch/commit/3a4c234 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-30 15:26:00+03:00

5.12.7
------
 * уменьшаем время хранения пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/8d4c894 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-27 13:00:11+03:00

5.12.6
------
 * ISEARCH-5633 фикс неизвестного языка  [ https://github.yandex-team.ru/tools/intrasearch/commit/dde1e96 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-27 11:08:34+03:00

5.12.5
------
 * ISEARCH-5633 фикс неизвестного языка  [ https://github.yandex-team.ru/tools/intrasearch/commit/66ceeff ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-24 17:09:54+03:00

5.12.4
------
 * ISEARCH-5595 фикс пушей без ревизий  [ https://github.yandex-team.ru/tools/intrasearch/commit/a01c62f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-24 14:23:11+03:00

5.12.3
------
 * ISEARCH-5595 фиксы пушей директории (#606)                           [ https://github.yandex-team.ru/tools/intrasearch/commit/29f3da0 ]
 * ISEARCH-5563 варнинги при устаревших документах в индексации (#605)  [ https://github.yandex-team.ru/tools/intrasearch/commit/1e37a43 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-24 10:44:15+03:00

5.12.2
------
 * ISEARCH-5628 добавляем video_conferencing в саджест переговорок  [ https://github.yandex-team.ru/tools/intrasearch/commit/a533f35 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-21 18:52:13+03:00

5.12.1
------
 * ISEARCH-5545 учимся скипать проверку ревизий в поиске  [ https://github.yandex-team.ru/tools/intrasearch/commit/a6ac34e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-21 14:21:00+03:00

5.12.0
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5613: Переписал тесты api на pytest (#604)  [ https://github.yandex-team.ru/tools/intrasearch/commit/d0e250e ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5545 новый сервис для тестирования дефолтной формулы саас  [ https://github.yandex-team.ru/tools/intrasearch/commit/c4802c0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-21 12:31:18+03:00

5.11.0
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5591: Оценка документов на поисковой выдаче (#603)  [ https://github.yandex-team.ru/tools/intrasearch/commit/f326036 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5486 отключаем индексацию стартрека через yt  [ https://github.yandex-team.ru/tools/intrasearch/commit/597b23d ]
 * ISEARCH-5580 обновляем версию yt.wrapper (#602)       [ https://github.yandex-team.ru/tools/intrasearch/commit/43eed87 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-16 12:39:58+03:00

5.10.5
------
 * ISEARCH-5597 фикс индексации с алиасами  [ https://github.yandex-team.ru/tools/intrasearch/commit/f869cf6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-13 20:15:40+03:00

5.10.4
------
 * ISEARCH-5596 убираем двоеточие из саджестовых атрибутов  [ https://github.yandex-team.ru/tools/intrasearch/commit/0657842 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-13 19:43:58+03:00

5.10.3
------
 * ISEARCH-5546 включаем ферримен для этушки и стартрека  [ https://github.yandex-team.ru/tools/intrasearch/commit/6dcb0d5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-10 18:07:15+03:00

5.10.2
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5578: Обработка пушей об изменении алиасов в директории (#601)  [ https://github.yandex-team.ru/tools/intrasearch/commit/aa947e7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-10 16:24:40+03:00

5.10.1
------

* [Kirill Kartashov](http://staff/qazaq@yandex-team.ru)

 * ISEARCH-5578: Индексация алиасов польз-й, отделов и групп директории (#600)  [ https://github.yandex-team.ru/tools/intrasearch/commit/791314e ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * доступ Кириллу в админку  [ https://github.yandex-team.ru/tools/intrasearch/commit/40754e1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-10 11:56:22+03:00

5.10.0
------
 * ISEARCH-5530 базовый саджест по тикетам трекера (#597)           [ https://github.yandex-team.ru/tools/intrasearch/commit/8205e1d ]
 * улучшение логирования в yt тасках                                [ https://github.yandex-team.ru/tools/intrasearch/commit/4609b5f ]
 * ISEARCH-5486 команда для массовой переиндексации трекера (#599)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2a24590 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-09 12:26:40+03:00

5.9.2
-----
 * Увеличиваем таймауты к abc                        [ https://github.yandex-team.ru/tools/intrasearch/commit/ab45f84 ]
 * доработки для разработки на виртуалке + локально  [ https://github.yandex-team.ru/tools/intrasearch/commit/3c84985 ]
 * доработки для разработки на виртуалке + локально  [ https://github.yandex-team.ru/tools/intrasearch/commit/800fe01 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-06 17:58:54+03:00

5.9.1
-----
 * ISEARCH-5571 фикс индексации тикетов в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/fc65f9f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-03 12:42:58+03:00

5.9.0
-----
 * ISEARCH-5571 фикс индексации тикетов в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/30864ac ]
 * ISEARCH-5523 тесты на перезапуск пушей      [ https://github.yandex-team.ru/tools/intrasearch/commit/7436fd7 ]
 * ISEARCH-5558 новые динамические факторы     [ https://github.yandex-team.ru/tools/intrasearch/commit/f9a0d94 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-03 12:07:30+03:00

5.8.7
-----
 * ISEARCH-5568 фикс неправльного рестарта тикетов директории и трекере  [ https://github.yandex-team.ru/tools/intrasearch/commit/0d8e6a0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-08-01 12:49:53+03:00

5.8.6
-----
 * ISEARCH-5523 дизейблим рестарт пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/fd11a93 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-31 19:40:46+03:00

5.8.5
-----
 * ISEARCH-5523 прекращаем рестартить пуши этушки  [ https://github.yandex-team.ru/tools/intrasearch/commit/d4dd4fa ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-31 19:38:10+03:00

5.8.4
-----
 * ISEARCH-5523 возвращаем рестарт пушей, ограничиваем кол-во комментариев в трекере 200  [ https://github.yandex-team.ru/tools/intrasearch/commit/775367f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-31 19:21:24+03:00

5.8.3
-----
 * ISEARCH-5523 дизейблим рестарт пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/6b47571 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-31 18:52:08+03:00

5.8.2
-----
 * ISEARCH-5523 стейлим пуши уже через час  [ https://github.yandex-team.ru/tools/intrasearch/commit/be63fad ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-31 13:33:44+03:00

5.8.1
-----
 * ISEARCH-5523 фикс ретрая пушей без организации в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/6499f39 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-31 12:12:14+03:00

5.8.0
-----
 * ISEARCH-5549 найстройка окружений для локальной разработки (#595)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3f02f0d ]
 * ISEARCH-5523 мониторинг и автоперезапуск упавших пушей (#595)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3f02f0d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-30 15:36:36+03:00

5.7.19
------
 * ISEARCH-5550 убираем костыли и вытаскиваем только первую сотню значений фасетов  [ https://github.yandex-team.ru/tools/intrasearch/commit/40cd5e2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-25 13:21:39+03:00

5.7.18
------
 * убираем ретраи фасетов  [ https://github.yandex-team.ru/tools/intrasearch/commit/ac3be5e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-25 11:25:07+03:00

5.7.17
------
 * попытка убрать хак с фасетами  [ https://github.yandex-team.ru/tools/intrasearch/commit/703b507 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-25 11:14:39+03:00

5.7.16
------
 * ISEARCH-5543 завершаем пуш после любой финальной успешной стадии, а не только после успешного store  [ https://github.yandex-team.ru/tools/intrasearch/commit/f4427bb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-24 16:55:54+03:00

5.7.15
------
 * ISEARCH-5543 убираем лишние пуши  [ https://github.yandex-team.ru/tools/intrasearch/commit/21ddb57 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-24 14:25:05+03:00

5.7.14
------
 * ISEARCH-5543 дополнительный лог апдейтов  [ https://github.yandex-team.ru/tools/intrasearch/commit/df8c514 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-24 13:51:26+03:00

5.7.13
------
 * ISEARCH-5543 связываем пуш с первой индексацией  [ https://github.yandex-team.ru/tools/intrasearch/commit/18e7c45 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 19:22:21+03:00

5.7.12
------
 * ISEARCH-5543 связываем пуш с первой индексацией  [ https://github.yandex-team.ru/tools/intrasearch/commit/cf53be2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 19:18:55+03:00

5.7.11
------
 * ISEARCH-5543 ещё одно логирование пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/66e4dbb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 19:09:53+03:00

5.7.10
------
 * ISEARCH-5543 в реалтайм запускаем индексации из пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/20a3dc1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 18:44:29+03:00

5.7.9
-----
 * ISEARCH-5543 добавляем логи  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e20578 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 18:38:45+03:00

5.7.8
-----
 * ISEARCH-5543 отменяем лишние пуши директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/fdbfb4c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 18:20:23+03:00

5.7.7
-----
 * ISEARCH-5543 убираем лишнее из админки  [ https://github.yandex-team.ru/tools/intrasearch/commit/01c93f2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 18:07:09+03:00

5.7.6
-----
 * ISEARCH-5543 упрощаем статусы пушей (#593)                                   [ https://github.yandex-team.ru/tools/intrasearch/commit/908d670 ]
 * ISEARCH-5503 фикс удаления старых-старых индексаций, у которых нет end_time  [ https://github.yandex-team.ru/tools/intrasearch/commit/b3e99db ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-20 17:59:55+03:00

5.7.5
-----
 * ISEARCH-5540 фикс тестов и приема пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/f51a2a5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-18 14:18:29+03:00

5.7.4
-----

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-5540 Несколько финальных исправлений в обработке пушей (#590)  [ https://github.yandex-team.ru/tools/intrasearch/commit/f962f96 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5503 команда удаления старых индексаций (#589)  [ https://github.yandex-team.ru/tools/intrasearch/commit/becf4ed ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-18 13:44:57+03:00

5.7.3
-----
 * ISEARCH-5537 доработки статистики и команды переиндексации всей директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/15164b5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-17 18:59:37+03:00

5.7.2
-----
 * ISEARCH-5537 фикс определения with_global  [ https://github.yandex-team.ru/tools/intrasearch/commit/db90d51 ]
 * ISEARCH-5537 логи про статистику           [ https://github.yandex-team.ru/tools/intrasearch/commit/0019839 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-17 15:53:47+03:00

5.7.1
-----
 * ISEARCH-5537 фикс лишнего удаления статусов (#592)  [ https://github.yandex-team.ru/tools/intrasearch/commit/a133cd0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-17 15:39:30+03:00

5.7.0
-----
 * ISEARCH-5537 оптимизация сбора статистики индексации (#591)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ead2243 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-17 15:10:32+03:00

5.6.12
------
 * ISEARCH-5495 хотфикс в sync_directory_organization  [ https://github.yandex-team.ru/tools/intrasearch/commit/95e2563 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-15 11:59:50+03:00

5.6.11
------
 * пересмотр admin_users  [ https://github.yandex-team.ru/tools/intrasearch/commit/afc316c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-11 13:51:08+03:00

5.6.10
------

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-5365 Фиксы: логи, трекер, xss (#587)  [ https://github.yandex-team.ru/tools/intrasearch/commit/752a8f5 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5528 убираем сервисы из основной выдачи метавертикали (#588)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7b58765 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-11 13:27:13+03:00

5.6.9
-----

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-5365 Фиксы пушей от директории + привязка пушей к организациям (#586)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c1ef6a0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-10 16:55:58+03:00

5.6.8
-----

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-5365 фикс ссылки на логи и перевода пушей трекера в cancel  [ https://github.yandex-team.ru/tools/intrasearch/commit/e026fbb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-10 11:50:58+03:00

5.6.7
-----

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * фиксы фиксов                              [ https://github.yandex-team.ru/tools/intrasearch/commit/21f5ece ]
 * ISEARCH-5365 Надежность индексации пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/9d23812 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-09 19:04:08+03:00

5.6.6
-----
 * ISEARCH-5520 учитываем, что из ab могут приходить списки  [ https://github.yandex-team.ru/tools/intrasearch/commit/102ac96 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-06 15:06:30+03:00

5.6.5
-----
 * ISEARCH-5520 берем фичи из конфига эксперимента + фича swap24 (#582)  [ https://github.yandex-team.ru/tools/intrasearch/commit/f6267cd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-06 14:47:23+03:00

5.6.4
-----

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-5365 Надежность индексации пушей (#576)  [ https://github.yandex-team.ru/tools/intrasearch/commit/e43c231 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-04 14:22:53+03:00

5.6.3
-----
 * ISEARCH-5515 отказоустойчивость при неработающем yt (#581)  [ https://github.yandex-team.ru/tools/intrasearch/commit/a749b2d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-04 11:27:50+03:00

5.6.2
-----
 * ISEARCH-5510 регулярная переиндексация wiki и doc в saas и yt  [ https://github.yandex-team.ru/tools/intrasearch/commit/39d86bd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-03 17:51:10+03:00

5.6.1
-----

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-5514 Не выводится количество документов в ревизии в админке bisearch (#580)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c265062 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * фикс TypeError: not enough arguments for format string  [ https://github.yandex-team.ru/tools/intrasearch/commit/c10bab3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-03 17:09:25+03:00

5.6.0
-----
 * ISEARCH-5510 настройка инстансов ферримена в зависимости от сервиса и раздельная настройка дефолтных сервисов для разных источников (#579)  [ https://github.yandex-team.ru/tools/intrasearch/commit/95e4078 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-07-03 11:39:36+03:00

5.5.9
-----
 * SAASSUP-220 не переоткрываем индекс в saas при realtime индексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/803e7c9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-21 18:56:55+03:00

5.5.8
-----
 * SAASSUP-220 не переоткрываем индекс в saas при realtime индексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/a97f23d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-21 18:47:22+03:00

5.5.7
-----
 * SAASSUP-220 индексируем людей и ко в b2b realtime по умолчанию  [ https://github.yandex-team.ru/tools/intrasearch/commit/32daa29 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-21 18:38:31+03:00

5.5.6
-----
 * ISEARCH-5472 таймаут для каталога страниц вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/4776996 ]
 * ISEARCH-5392 убираю ненужный лог                [ https://github.yandex-team.ru/tools/intrasearch/commit/7a7bf0c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-20 17:36:28+03:00

5.5.5
-----
 * ISEARCH-5392 ещё немного логов  [ https://github.yandex-team.ru/tools/intrasearch/commit/17c958e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-20 15:23:43+03:00

5.5.4
-----
 * ISEARCH-5438 добавляем в запрос информацию о нашем request_id, чтобы уметь объединять несколько запросов в саас на одной вертикали  [ https://github.yandex-team.ru/tools/intrasearch/commit/6a02a9a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-14 18:26:48+03:00

5.5.3
-----
 * ISEARCH-5438 маркируем роботные запросы и добавляем информацию для деления зон и скоупов (#578)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c5c8958 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-08 18:46:26+03:00

5.5.2
-----
 * ISEARCH-5438 интеграция с abt (#577)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0759f45 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-08 15:12:56+03:00

5.5.1
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5377 не выводим сортировку на пустой выдаче (#575)                            [ https://github.yandex-team.ru/tools/intrasearch/commit/2c94d50 ]
 * ISEARCH-5481 убираем автоисправление если ничего не нашлось по исправленному запросу  [ https://github.yandex-team.ru/tools/intrasearch/commit/cba0a7a ]
 * ISEARCH-5456 исправление лишнего экранирования в errata (#574)                        [ https://github.yandex-team.ru/tools/intrasearch/commit/ca5b326 ]

* [Alexander Koshelev](http://staff/alexkoshelev@yandex-team.ru)

 * Фикс ParallelStep,,чтобы он был действительно параллельным (#461)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6da090d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-06 16:34:32+03:00

5.4.4
-----
 * ISEARCH-5473 удаление детей при удалении узла в idm.rolenodes (#573)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ee177ac ]
 * фикс flush_buffered_attribute                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/6b50f82 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-04 16:40:53+03:00

5.4.3
-----
 * ISEARCH-5392 добавляем логов в статистику индексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/0d6a4ef ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-01 14:16:46+03:00

5.4.2
-----
 * ISEARCH-5392 добавляем логов в статистику индексации (#572)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2c4e8dc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-06-01 13:19:49+03:00

5.4.1
-----
 * чиним export_searchlogs                                          [ https://github.yandex-team.ru/tools/intrasearch/commit/9459c88 ]
 * ISEARCH-5475 убираем yt_send_push_tables из регулярного запуска  [ https://github.yandex-team.ru/tools/intrasearch/commit/3e0de75 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-31 17:27:36+03:00

5.4.0
-----
 * ISEARCH-4978 тесты на авторизацию в abovemeta (#566)                                   [ https://github.yandex-team.ru/tools/intrasearch/commit/a33854c ]
 * ISEARCH-5366 добавляем количество пушей в логе в мониторинг полноты индексации (#571)  [ https://github.yandex-team.ru/tools/intrasearch/commit/07b63bc ]
 * ISEARCH-5475 включаем регулярную индексацию через yt (#570)                            [ https://github.yandex-team.ru/tools/intrasearch/commit/d910c24 ]
 * ISEARCH-5452 фикс построения хлебных крошек в документации (#569)                      [ https://github.yandex-team.ru/tools/intrasearch/commit/27b4dc5 ]
 * ISEARCH-5472 - увеличиваем таймаут ожидания от вики до 20сек (#568)                    [ https://github.yandex-team.ru/tools/intrasearch/commit/354cbee ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-31 15:12:01+03:00

5.3.4
-----
 * ISEARCH-5468 фикс получения заголовков у внешней документации (#567)  [ https://github.yandex-team.ru/tools/intrasearch/commit/79d889a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-29 13:46:36+03:00

5.3.3
-----
 * ISEARCH-5469 возвращаем получение пушей о создании очереди     [ https://github.yandex-team.ru/tools/intrasearch/commit/fdb19fb ]
 * ISEARCH-5455 вернула обратно sanitize=True в get_text_content  [ https://github.yandex-team.ru/tools/intrasearch/commit/2da3963 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-28 18:47:55+03:00

5.3.2
-----
 * ISEARCH-4978 tvm2 в abovemeta (#565)  [ https://github.yandex-team.ru/tools/intrasearch/commit/e55c305 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-25 12:53:07+03:00

5.3.1
-----
 * ISEARCH-5460 уменьшаем таймауты в saas  [ https://github.yandex-team.ru/tools/intrasearch/commit/b6df9e2 ]
 * приводим вики урл к нижнему регистру    [ https://github.yandex-team.ru/tools/intrasearch/commit/b9abf6d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-24 17:29:43+03:00

5.3.0
-----
 * ISEARCH-5256 Факторы по офисам в оборудовании (#564)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6135d736 ]

[Gleb Nikolaev](http://staff/larousse@yandex-team.ru) 2018-05-24 13:04:44+03:00

5.2.3
-----
 * ISEARCH-5005 [Фемида] настройка ранжирования (#563)  [ https://github.yandex-team.ru/tools/intrasearch/commit/5f40d32e ]

[Gleb Nikolaev](http://staff/larousse@yandex-team.ru) 2018-05-22 14:51:40+03:00

5.2.2
-----
 * ISEARCH 5005 [Фемида] настройка ранжирования (#562)  [ https://github.yandex-team.ru/tools/intrasearch/commit/59a7dab2 ]

[Gleb Nikolaev](http://staff/larousse@yandex-team.ru) 2018-05-21 20:57:49+03:00

5.2.1
-----
 * ISEARCH-5457 порядок в команде создания relev.conf для saas (#561)  [ https://github.yandex-team.ru/tools/intrasearch/commit/92f42bf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-18 15:32:46+03:00

5.2.0
-----

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-5367 Принимать пуши об изменении системы от idm.rolenodes (#559)  [ https://github.yandex-team.ru/tools/intrasearch/commit/edc1266 ]
 * Фиксы ISEARCH-5367                                                        [ https://github.yandex-team.ru/tools/intrasearch/commit/b4c2ecb ]
 * ISEARCH-5367 Принимать пуши об изменении системы от idm.rolenodes         [ https://github.yandex-team.ru/tools/intrasearch/commit/c9ff692 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-5453 cpu-friendly get_text_content                                     [ https://github.yandex-team.ru/tools/intrasearch/commit/680b3f2 ]
 * ISEARCH-5449 команда для полной переиндексации этушки и других больши… (#560)  [ https://github.yandex-team.ru/tools/intrasearch/commit/84f2fa8 ]
 * ISEARCH-5287 отдельный ferryman для престейбла и прода                         [ https://github.yandex-team.ru/tools/intrasearch/commit/490fbbb ]
 * ISEARCH-5287 отдельный ferryman для престейбла и прода                         [ https://github.yandex-team.ru/tools/intrasearch/commit/e9ef99b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-16 14:08:11+03:00

5.1.8
-----
 * ISEARCH-5446 меняем токены для апи метрики  [ https://github.yandex-team.ru/tools/intrasearch/commit/d04dbd0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-10 18:56:30+03:00

5.1.7
-----
 * ISEARCH-5422 выставляем max_row_weight для mr операций  [ https://github.yandex-team.ru/tools/intrasearch/commit/5a94dbc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-10 14:37:22+03:00

5.1.6
-----
 * ISEARCH-5422 выставляем max_row_weight для mr операций  [ https://github.yandex-team.ru/tools/intrasearch/commit/bfd9f20 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-10 14:16:46+03:00

5.1.5
-----
 * ISEARCH-5422 выставляем max_row_weight для mr операций  [ https://github.yandex-team.ru/tools/intrasearch/commit/7e46bfb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-10 13:53:21+03:00

5.1.4
-----
 * не падаем при неправильном ответе метрики в индексации вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/6e370a0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-08 18:49:48+03:00

5.1.3
-----
 * ISEARCH-5422 фикс индексации st через celery+yt  [ https://github.yandex-team.ru/tools/intrasearch/commit/7379add ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-08 17:00:14+03:00

5.1.2
-----
 * чиним индексацию стартрека из-за добавления next link в апи  [ https://github.yandex-team.ru/tools/intrasearch/commit/f025f28 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-08 15:25:46+03:00

5.1.1
-----
 * ISEARCH-5422 фикс кириллицы  [ https://github.yandex-team.ru/tools/intrasearch/commit/16dc9d2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-08 12:07:54+03:00

5.1
---
 * ISEARCH-5425 Пуши через ferrymen (#558)           [ https://github.yandex-team.ru/tools/intrasearch/commit/d172ef7 ]
 * ISEARCH-5422 индексация json_ref через yt (#554)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ae43c8e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-05-07 18:55:22+03:00

5.0.12
------
 * ISEARCH-5414 В выдаче офис, которого уже нет на стаффе (#557)  [ https://github.yandex-team.ru/tools/intrasearch/commit/78f11e92 ]
 * Isearch 4745 (#556)                                            [ https://github.yandex-team.ru/tools/intrasearch/commit/41b3d58f ]

[Gleb Nikolaev](http://staff/larousse@yandex-team.ru) 2018-04-26 16:45:29+03:00

5.0.11
------

* [Gleb Nikolaev](http://staff/larousse@yandex-team.ru)

 * ISEARCH-4745 Перезапуск индексации в админке (#555)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8e815be5 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * фиксы тестов                     [ https://github.yandex-team.ru/tools/intrasearch/commit/8ab97de2 ]
 * фиксы для совместной разработки  [ https://github.yandex-team.ru/tools/intrasearch/commit/7d0f4527 ]
 * фиксы для совместной разработки  [ https://github.yandex-team.ru/tools/intrasearch/commit/6991f7c4 ]

[Gleb Nikolaev](http://staff/larousse@yandex-team.ru) 2018-04-25 19:05:59+03:00

5.0.10
------
 * Убираем таймаут в запросах к idm rolenodes (==ждем вечно)  [ https://github.yandex-team.ru/tools/intrasearch/commit/baa6b3b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-20 14:19:08+03:00

5.0.9
-----
 * ISEARCH-5435 service_id в саджесте групп (#553)  [ https://github.yandex-team.ru/tools/intrasearch/commit/51a5f41 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-20 12:06:39+03:00

5.0.8
-----
 * ISEARCH-5424 доработка команды мержа таблиц  [ https://github.yandex-team.ru/tools/intrasearch/commit/8943532 ]
 * логи в вики                                  [ https://github.yandex-team.ru/tools/intrasearch/commit/c4c9b6f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-19 10:30:37+03:00

5.0.6
-----
 * ISEARCH-5427 указываем tablet_cell_bundles  [ https://github.yandex-team.ru/tools/intrasearch/commit/b441b56 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-17 19:06:56+03:00

5.0.5
-----
 * ISEARCH-5427 указываем tablet_cell_bundles  [ https://github.yandex-team.ru/tools/intrasearch/commit/662c9ac ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-17 18:30:52+03:00

5.0.4
-----
 * ISEARCH-5330 нормализация урлов вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/c236909 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-17 17:19:24+03:00

5.0.3
-----
 * ISEARCH-5426 фикс пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/35a35aa ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-17 16:32:18+03:00

5.0.2
-----
 * доступ в админку для kiparis и larousse    [ https://github.yandex-team.ru/tools/intrasearch/commit/4680f20 ]
 * ISEARCH-5287 фикс индексации doc.external  [ https://github.yandex-team.ru/tools/intrasearch/commit/2eafb60 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-17 15:58:48+03:00

5.0.1
-----
 * ISEARCH-5287 фикс индексации idm.rolenodes  [ https://github.yandex-team.ru/tools/intrasearch/commit/0f9ea64 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-17 15:35:03+03:00

5.0.0
-----
 * ISEARCH-5426 фикс зависания тестов       [ https://github.yandex-team.ru/tools/intrasearch/commit/270e6c1 ]
 * ISEARCH-5426 индексация через YT (#550)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2e11ef0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-17 14:57:24+03:00

4.10.2
------
 * ISEARCH-5418 фикс 'NoneType' object has no attribute 'replace' в errata  [ https://github.yandex-team.ru/tools/intrasearch/commit/6eb2ad5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-04 17:58:37+03:00

4.10.1
------
 * ISEARCH-5417 используем пагинацию в комментариях к тикетам стартрека  [ https://github.yandex-team.ru/tools/intrasearch/commit/5e6a435 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-04 15:08:29+03:00

4.10.0
------
 * ISEARCH-5378 оптимизируем пуши от стартрека (#549)  [ https://github.yandex-team.ru/tools/intrasearch/commit/4edc600 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-03 16:17:25+03:00

4.9.7
-----
 * ISEARCH-5416 фикс исправления при None  [ https://github.yandex-team.ru/tools/intrasearch/commit/3f918a8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-02 15:06:40+03:00

4.9.6
-----
 * ISEARCH-5416 фикс исправления при None                                 [ https://github.yandex-team.ru/tools/intrasearch/commit/83cb7af ]
 * ISEARCH-5416 на метавертикали в первую очередь смотрим на сервис вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/35d9c23 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-02 14:56:27+03:00

4.9.5
-----
 * ISEARCH-5403 запрет переиндексировать все организации из админки b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/3507020 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-04-02 13:07:18+03:00

4.9.4
-----
 * ISEARCH-4185 не используем template в саджесте  [ https://github.yandex-team.ru/tools/intrasearch/commit/59d8d53 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-23 14:50:07+03:00

4.9.3
-----
 * ISEARCH-4185 добавляем подсветку в errata  [ https://github.yandex-team.ru/tools/intrasearch/commit/ad79036 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-23 11:50:28+03:00

4.9.2
-----
 * ISEARCH-4185 фикс саджеста по людям  [ https://github.yandex-team.ru/tools/intrasearch/commit/8d7bc92 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-22 19:19:09+03:00

4.9.1
-----
 * ISEARCH-4185 фикс отсутствия errata  [ https://github.yandex-team.ru/tools/intrasearch/commit/3b6cdf2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-22 18:00:01+03:00

4.9.0
-----
 * ISEARCH-4185 редирект на исправленный запрос (#544)  [ https://github.yandex-team.ru/tools/intrasearch/commit/840b265 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-22 17:37:26+03:00

4.8.5
-----
 * ISEARCH-5163 добавляем велосипеды в вывод саджеста  [ https://github.yandex-team.ru/tools/intrasearch/commit/76dc440 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-21 21:32:19+03:00

4.8.4
-----
 * ISEARCH-5163 добавляем велосипеды в индекс людей (#548)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6487b77 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-21 21:01:16+03:00

4.8.3
-----
 * ISEARCH-5127 правильная версия startrek-client  [ https://github.yandex-team.ru/tools/intrasearch/commit/42630fd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-21 18:15:55+03:00

4.8.2
-----
 * ISEARCH-5127 в индексации трекера заменяем issues/_search на issues/_RelativeScroll (#547)  [ https://github.yandex-team.ru/tools/intrasearch/commit/e84b9db ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-20 18:56:39+03:00

4.8.1
-----
 * ISEARCH-5078 убираем ids.exceptions из индексатора стартрека  [ https://github.yandex-team.ru/tools/intrasearch/commit/c04c233 ]
 * ISEARCH-5078 фикс ошибки из-за обновления ids                 [ https://github.yandex-team.ru/tools/intrasearch/commit/4374ef0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-20 14:26:27+03:00

4.8.0
-----
 * ISEARCH-5078 переход на новое апи abc (#546)        [ https://github.yandex-team.ru/tools/intrasearch/commit/3f21b5b ]
 * ISEARCH-5359 не принимаем пуши от не generic групп  [ https://github.yandex-team.ru/tools/intrasearch/commit/f8ed38b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-20 12:53:03+03:00

4.7.6
-----
 * ISEARCH-5363 стенд для асессоров (prestable) (#545)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c1a3c86 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-15 13:00:55+03:00

4.7.5
-----
 * ISEARCH-5359 убираем из directory.people не generic группы  [ https://github.yandex-team.ru/tools/intrasearch/commit/10c90ab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-13 14:14:22+03:00

4.7.4
-----
 * ISEARCH-4185 обратная совместимость для новой работы с опечатками  [ https://github.yandex-team.ru/tools/intrasearch/commit/019192d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-12 20:25:52+03:00

4.7.3
-----
 * ISEARCH-5374 получаем ip из x-forwarded-for  [ https://github.yandex-team.ru/tools/intrasearch/commit/4da2803 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-07 13:26:54+03:00

4.7.2
-----
 * ISEARCH-5374 логирование пришедших ip  [ https://github.yandex-team.ru/tools/intrasearch/commit/c4e1bf3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-07 13:10:58+03:00

4.7.1
-----
 * ISEARCH-5374 получаем ip из x-forwarded-for (#543)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2f1abf3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-06 19:44:16+03:00

4.7
---
 * ISEARCH-5359 индексируем только generic группы в directory.groups (#542)  [ https://github.yandex-team.ru/tools/intrasearch/commit/56a99c5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-06 17:04:22+03:00

4.6.16
------
 * ISEARCH-5391 фикс индексации внешней документации  [ https://github.yandex-team.ru/tools/intrasearch/commit/7c252d9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-03-05 17:58:14+03:00

4.6.15
------
 * ISEARCH-5384 выключаем индексацию jhist  [ https://github.yandex-team.ru/tools/intrasearch/commit/79a3705 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-20 17:27:57+03:00

4.6.14
------
 * ISEARCH-5382 ретраим стафф апи только один раз  [ https://github.yandex-team.ru/tools/intrasearch/commit/bce3a1f ]
 * ISEARCH-5382 ретраим стафф апи только один раз  [ https://github.yandex-team.ru/tools/intrasearch/commit/b5808e1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-19 20:52:50+03:00

4.6.13
------
 * ISEARCH-5362 добавляем staff_id и uid в сериалайзер (#541)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7467ece ]
 * фиксы скорости админки                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/259e2f6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-14 20:18:00+03:00

4.6.12
------
 * более быстрая сортировка в админке индексаций  [ https://github.yandex-team.ru/tools/intrasearch/commit/702ac8c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-13 16:09:04+03:00

4.6.11
------
 * ISEARCH-5369 фикс удаления документов из saas (#540)  [ https://github.yandex-team.ru/tools/intrasearch/commit/734a13c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-13 13:54:15+03:00

4.6.10
------
 * conn_max_age настраиваемый параметр  [ https://github.yandex-team.ru/tools/intrasearch/commit/0b04d61 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-13 10:51:25+03:00

4.6.9
-----
 * ISEARCH-5368 не деляем ревизию обязательным атрибутом  [ https://github.yandex-team.ru/tools/intrasearch/commit/4460366 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-12 16:11:21+03:00

4.6.8
-----
 * ISEARCH-5368 больше логирования  [ https://github.yandex-team.ru/tools/intrasearch/commit/51a66b0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-12 16:01:06+03:00

4.6.7
-----
 * ISEARCH-5368 больше логирования  [ https://github.yandex-team.ru/tools/intrasearch/commit/7397738 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-12 15:29:28+03:00

4.6.6
-----
 * ISEARCH-5291 пользовательские факторы по департаментам и сервисам в саджесте idm (#539)  [ https://github.yandex-team.ru/tools/intrasearch/commit/62df5ab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-12 14:28:44+03:00

4.6.5
-----
 * ISEARCH-5223 закрываем jsonp в b2b поиске  [ https://github.yandex-team.ru/tools/intrasearch/commit/eacdeae ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-08 16:21:38+03:00

4.6.4
-----
 * ISEARCH-5207 фикс 500 при пустом parsed  [ https://github.yandex-team.ru/tools/intrasearch/commit/62aa42e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-08 15:32:47+03:00

4.6.3
-----
 * ISEARCH-5207 фикс получение роботных пользователей в api/v7  [ https://github.yandex-team.ru/tools/intrasearch/commit/23838ee ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-08 13:38:55+03:00

4.6.2
-----
 * ISEARCH-5207 api v7 директории (#538)                   [ https://github.yandex-team.ru/tools/intrasearch/commit/2e6df90 ]
 * ISEARCH-5328 (revert) убираем лишние пробелы в машинах  [ https://github.yandex-team.ru/tools/intrasearch/commit/c73110e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-08 12:44:33+03:00

4.6.1
-----
 * ISEARCH-5328 убираем лишние пробелы в машинах  [ https://github.yandex-team.ru/tools/intrasearch/commit/dc6a2a0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-07 14:42:06+03:00

4.6.0
-----
 * ISEARCH-5328 вывод номера машины в people при совпадении  [ https://github.yandex-team.ru/tools/intrasearch/commit/364592d ]
 * ISEARCH-5158 тесты в тимсити (#537)                       [ https://github.yandex-team.ru/tools/intrasearch/commit/2cb1b96 ]
 * Update README.md                                          [ https://github.yandex-team.ru/tools/intrasearch/commit/c479a39 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-07 14:29:40+03:00

4.5.10
------
 * ISEARCH-5314 keys в индексации people.groups  [ https://github.yandex-team.ru/tools/intrasearch/commit/feccf63 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-01 14:54:05+03:00

4.5.9
-----
 * ISEARCH-5314 имена департаментов и сервисов в body в people.groups  [ https://github.yandex-team.ru/tools/intrasearch/commit/e4bcd30 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-01 14:06:40+03:00

4.5.8
-----
 * Isearch 5314 (#535)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9c5489c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-01 13:54:24+03:00

4.5.7
-----
 * ISEARCH-5314 локализация в саджесте people.groups (#534)  [ https://github.yandex-team.ru/tools/intrasearch/commit/4a8b96a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-02-01 12:28:52+03:00

4.5.6
-----
 * ISEARCH-4372 прокидываем дополнительные поля колдунщика из админки       [ https://github.yandex-team.ru/tools/intrasearch/commit/20f22fb ]
 * ISEARCH-5349 приводим к нижнему регистру idm.rolenodes.slug_path (#533)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2de5ded ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-31 19:22:26+03:00

4.5.5
-----
 * ISEARCH-5356 добавляем login_pure в сниппеты людей директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/84687a5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-31 14:26:26+03:00

4.5.4
-----
 * ISEARCH-5353 дополнительное логирование  [ https://github.yandex-team.ru/tools/intrasearch/commit/83ffd9b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-30 14:45:04+03:00

4.5.3
-----
 * ISEARCH-5353 увеличиваем таймаут на запрос директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/af580ab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-30 14:03:16+03:00

4.5.2
-----
 * ISEARCH-5353 увеличиваем таймаут на запрос директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/e8242b1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-30 13:37:03+03:00

4.5.1
-----
 * ISEARCH-5353 доступ внешних админов к саджесту (#532)  [ https://github.yandex-team.ru/tools/intrasearch/commit/788e490 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-29 20:09:27+03:00

4.5.0
-----
 * ISEARCH-5318 сохраняем форму без диактрики в саджесте (#531)     [ https://github.yandex-team.ru/tools/intrasearch/commit/6985af2 ]
 * ISEARCH-5344 ссылки на админку пользователя в директории (#530)  [ https://github.yandex-team.ru/tools/intrasearch/commit/1089432 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-29 15:26:47+03:00

4.4.13
------
 * ISEARCH-5329 фикс мониторинга acl и b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/6b2a0f0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-26 14:53:01+03:00

4.4.12
------
 * ISEARCH-5329 фикс мониторинга acl и b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/4d4d2b8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-26 14:46:05+03:00

4.4.11
------
 * ISEARCH-5329 фикс мониторинга acl  [ https://github.yandex-team.ru/tools/intrasearch/commit/b631408 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-26 12:13:56+03:00

4.4.10
------
 * ISEARCH-5323 не индексируем английский кликхаус  [ https://github.yandex-team.ru/tools/intrasearch/commit/06844bf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-25 18:34:01+03:00

4.4.9
-----
 * ISEARCH-5323 не индексируем английский кликхаус  [ https://github.yandex-team.ru/tools/intrasearch/commit/c497c81 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-25 18:25:29+03:00

4.4.8
-----
 * ISEARCH-5346 отключаем индексацию лего   [ https://github.yandex-team.ru/tools/intrasearch/commit/f0030e5 ]
 * ISEARCH-5343 фиксируем версию pyOpenSSL  [ https://github.yandex-team.ru/tools/intrasearch/commit/694248b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-25 17:13:21+03:00

4.4.7
-----
 * ISEARCH-5326 добаляем лог о полученных данных директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/e08dc88 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-25 15:34:59+03:00

4.4.6
-----
 * ISEARCH-5323 добавляем description и индексируем div[role=main] для doc.external  [ https://github.yandex-team.ru/tools/intrasearch/commit/00454b5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-25 14:54:35+03:00

4.4.5
-----
 * ISEARCH-5323 добавляем description и индексируем div[role=main] для doc.external  [ https://github.yandex-team.ru/tools/intrasearch/commit/a7d563f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-25 14:10:09+03:00

4.4.4
-----
 * ISEARCH-5323 добавляем больше зон во внешнюю документацию (#529)  [ https://github.yandex-team.ru/tools/intrasearch/commit/22408cf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-24 21:03:05+03:00

4.4.3
-----
 * не ретраим запросы десайдера  [ https://github.yandex-team.ru/tools/intrasearch/commit/98a5732 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-24 18:45:08+03:00

4.4.2
-----
 * не ретраим запросы десайдера  [ https://github.yandex-team.ru/tools/intrasearch/commit/816d3a6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-24 18:36:25+03:00

4.4.1
-----
 * таймауты для search.decider  [ https://github.yandex-team.ru/tools/intrasearch/commit/6809e1c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-24 18:19:39+03:00

4.4.0
-----
 * ISEARCH-5306 зона с названием abc сервиса для документации (#528)                                            [ https://github.yandex-team.ru/tools/intrasearch/commit/d552efd ]
 * Isearch 5307 (#527)                                                                                          [ https://github.yandex-team.ru/tools/intrasearch/commit/55bfaf8 ]
 * ISEARCH-5304 убираем лишние сигналы из unistat и распределяем регулярные индексации более равномерно (#526)  [ https://github.yandex-team.ru/tools/intrasearch/commit/e630734 ]
 * ISEARCH-5329 мониторинг acl в b2b (#525)                                                                     [ https://github.yandex-team.ru/tools/intrasearch/commit/7d815b2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-24 17:00:02+03:00

4.3.6
-----
 * ISEARCH-5324 индексации по пушам с nort=False  [ https://github.yandex-team.ru/tools/intrasearch/commit/bd86977 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-18 15:29:48+03:00

4.3.5
-----
 * ISEARCH-5324 фикс acl в поиске b2b.tracker  [ https://github.yandex-team.ru/tools/intrasearch/commit/134fc76 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-17 19:51:31+03:00

4.3.4
-----
 * ISEARCH-5089 саджестим по словам из названия департаментов (#524)  [ https://github.yandex-team.ru/tools/intrasearch/commit/33e2376 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-17 15:00:41+03:00

4.3.3
-----
 * ISEARCH-5321 фактор departmentIsYandex  [ https://github.yandex-team.ru/tools/intrasearch/commit/e97de7e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-16 15:34:09+03:00

4.3.2
-----
 * ISEARCH-5248 добавление фактора objectCreated в кондуктор  [ https://github.yandex-team.ru/tools/intrasearch/commit/5ee6c09 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-15 19:14:33+03:00

4.3.1
-----
 * ISEARCH-5057 фикс поиска по пробелам  [ https://github.yandex-team.ru/tools/intrasearch/commit/70516e6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-15 15:24:25+03:00

4.3.0
-----
 * ISEARCH-5246 убираем null из сниппетов кондкутора, добавляем новые зоны в тикеты и группы (#522)  [ https://github.yandex-team.ru/tools/intrasearch/commit/649c7b3 ]
 * ISEARCH-5057 фикс падения при парсинге запроса (#523)                                             [ https://github.yandex-team.ru/tools/intrasearch/commit/e59504d ]
 * ISEARCH-5222 фикс ссылок на цели в тестинге                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/479e76b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-15 14:29:22+03:00

4.2.3
-----
 * фикс мониторинга acl трекера  [ https://github.yandex-team.ru/tools/intrasearch/commit/2fa8c87 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-15 14:02:39+03:00

4.2.2
-----
 * добавляем *.yandex-team.ru в cors на тесте b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/f0c65b1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-12 18:30:10+03:00

4.2.1
-----
 * ISEARCH-5313 добавляем префикс b2b слоям в бизнес-саджесте  [ https://github.yandex-team.ru/tools/intrasearch/commit/7430a27 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-10 16:54:10+03:00

4.2.0
-----
 * ISEARCH-5303 поиск по attachments для femida.candidates (#521)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0595fa6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2018-01-09 14:51:16+03:00

4.1.5
-----
 * ISEARCH-5309 оптимизация flush_buffered_attributes (#520)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c706c0c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-26 16:01:17+03:00

4.1.4
-----
 * фикс мониторинга acl трекера  [ https://github.yandex-team.ru/tools/intrasearch/commit/0c9893a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-25 15:30:09+03:00

4.1.3
-----
 * ISEARCH-5300 регулярная переиндексация people.groups раз в два часа  [ https://github.yandex-team.ru/tools/intrasearch/commit/2ace67e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-20 19:54:23+03:00

4.1.2
-----
 * фикс мониторинга упавших индексаций  [ https://github.yandex-team.ru/tools/intrasearch/commit/5b94818 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-20 16:42:23+03:00

4.1.1
-----
 * ISEARCH-5300 регулярные переиндексации people.group  [ https://github.yandex-team.ru/tools/intrasearch/commit/c9c0cac ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-20 13:23:10+03:00

4.1.0
-----
 * ISEARCH-5299 колдуншики при неполнм ответе от сааса  [ https://github.yandex-team.ru/tools/intrasearch/commit/f913ab6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-18 13:43:25+03:00

4.0.11
------
 * ISEARCH-5268 фикс саджеста клиник с кавычками  [ https://github.yandex-team.ru/tools/intrasearch/commit/573a57f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-13 16:13:19+03:00

4.0.10
------
 * ISEARCH-5268 используем геокодер, а не геопоиск  [ https://github.yandex-team.ru/tools/intrasearch/commit/d10baed ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-13 15:22:32+03:00

4.0.9
-----
 * ISEARCH-5268 нормализация адресов hr.clinics (#518)  [ https://github.yandex-team.ru/tools/intrasearch/commit/07a0dd9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-12 19:07:24+03:00

4.0.8
-----
 * ISEARCH-5033 фикс старого саджеста  [ https://github.yandex-team.ru/tools/intrasearch/commit/db44bc8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-12 10:20:39+03:00

4.0.7
-----
 * ISEARCH-5033 фикс сниппета массива  [ https://github.yandex-team.ru/tools/intrasearch/commit/28d5007 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-11 15:25:06+03:00

4.0.6
-----
 * ISEARCH-5035 переходим на idm-api.* вместо idm.*  [ https://github.yandex-team.ru/tools/intrasearch/commit/55bc33e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-08 17:17:33+03:00

4.0.5
-----
 * ISEARCH-5035 не добавляем алиасы в поисковые атрибуты, если их много  [ https://github.yandex-team.ru/tools/intrasearch/commit/718ca47 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-07 19:11:27+03:00

4.0.4
-----
 * ISEARCH-5280 чиним tail_searchlog  [ https://github.yandex-team.ru/tools/intrasearch/commit/163ee8b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-07 17:46:03+03:00

4.0.3
-----
 * ISEARCH-5033 incomplete варнинги от сааса  [ https://github.yandex-team.ru/tools/intrasearch/commit/e9f699b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-07 17:25:26+03:00

4.0.2
-----
 * ISEARCH-5033 json в запросе к саасу (#517)                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/a456990 ]
 * ISEARCH-5273 шаблон дашборда в yasm на jinje + разбиваем сигнал пушей по типам  [ https://github.yandex-team.ru/tools/intrasearch/commit/00a394f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-07 15:49:49+03:00

4.0.1
-----
 * ISEARCH-5271 DatabaseError -> db.Error  [ https://github.yandex-team.ru/tools/intrasearch/commit/95ddf4d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-07 12:15:02+03:00

4.0
---
 * ISEARCH-5271 ретраи при простановке статуса в базу  [ https://github.yandex-team.ru/tools/intrasearch/commit/904184d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-06 18:06:08+03:00

3.19.14
-------
 * ISEARCH-5279 быстрый фикс is_public        [ https://github.yandex-team.ru/tools/intrasearch/commit/787f295 ]
 * ISEARCH-5261 ещё немного улучшаем клиники  [ https://github.yandex-team.ru/tools/intrasearch/commit/334ce55 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-12-05 15:23:17+03:00

3.19.13
-------
 * индексируем лего в отдельном компоненте  [ https://github.yandex-team.ru/tools/intrasearch/commit/aa436f1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-30 11:54:30+03:00

3.19.12
-------
 * фикс мониторинга acl_testing  [ https://github.yandex-team.ru/tools/intrasearch/commit/ba6f7d0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-30 11:19:15+03:00

3.19.11
-------
 * ISEARCH-5261 ходим зомбом за клиниками  [ https://github.yandex-team.ru/tools/intrasearch/commit/0ce6f5c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-30 11:13:34+03:00

3.19.10
-------
 * фикс вывода id клубов в at.clubs  [ https://github.yandex-team.ru/tools/intrasearch/commit/54f21de ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-29 15:36:02+03:00

3.19.9
------
 * ISEARCH-3990 фикс аватарок клубов без хэшей  [ https://github.yandex-team.ru/tools/intrasearch/commit/b482d3c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-29 14:17:51+03:00

3.19.8
------
 * ISEARCH-5261 фикс токена  [ https://github.yandex-team.ru/tools/intrasearch/commit/c3b0495 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-29 13:39:27+03:00

3.19.7
------
 * ISEARCH-5261 обрабатываем пустые строки в xlsx  [ https://github.yandex-team.ru/tools/intrasearch/commit/687c6a0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-29 11:43:23+03:00

3.19.6
------
 * ISEARCH-5261 фикс админки просмотра пушей  [ https://github.yandex-team.ru/tools/intrasearch/commit/f75427c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-28 16:40:41+03:00

3.19.5
------
 * ISEARCH-5082 - at.clubs в отдельном компоненте  [ https://github.yandex-team.ru/tools/intrasearch/commit/c1b5c9e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-28 16:39:05+03:00

3.19.4
------
 * ISEARCH-5264 фикс валидации коллбэка в jsonp для конструктора форм  [ https://github.yandex-team.ru/tools/intrasearch/commit/7351f5e ]
 * ISEARCH-5261 нормализуем телефонные номера                          [ https://github.yandex-team.ru/tools/intrasearch/commit/91b5e83 ]
 * ISEARCH-5261 фикс пушей из логброкера                               [ https://github.yandex-team.ru/tools/intrasearch/commit/fe21708 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-28 16:11:02+03:00

3.19.3
------
 * ISEARCH-5261 openpyxl==2.4.9 в зависимости  [ https://github.yandex-team.ru/tools/intrasearch/commit/fa975c3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-28 13:15:28+03:00

3.19.2
------
 * ISEARCH-5261 индексация и саджест по клиникам в ДМС (#516)  [ https://github.yandex-team.ru/tools/intrasearch/commit/f8bb9a9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-28 12:53:17+03:00

3.19.1
------
 * ISEARCH-5245 убираем схему их урла-заголовка в at  [ https://github.yandex-team.ru/tools/intrasearch/commit/109450b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-24 14:18:52+03:00

3.19.0
------
 * ISEARCH-3990 фикс урла на аватарки клубов в at.clubs  [ https://github.yandex-team.ru/tools/intrasearch/commit/8617c67 ]
 * ISEARCH-5245 выводим урл, если нет названия в этушке  [ https://github.yandex-team.ru/tools/intrasearch/commit/77203ab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-24 13:50:23+03:00

3.18.7
------
 * выключаем регулярные переиндексации фемиды  [ https://github.yandex-team.ru/tools/intrasearch/commit/c9963b2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-24 11:30:03+03:00

3.18.6
------
 * ISEARCH-5082 добавила ещё логов  [ https://github.yandex-team.ru/tools/intrasearch/commit/c5e67a8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-24 11:03:21+03:00

3.18.5
------
 * ISEARCH-5234 улучшаем саджест переговорок  [ https://github.yandex-team.ru/tools/intrasearch/commit/922025d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-22 15:08:46+03:00

3.18.4
------
 * ISEARCH-5083 правильно склеиваем урлы в робот индексере  [ https://github.yandex-team.ru/tools/intrasearch/commit/552975e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-21 19:35:52+03:00

3.18.3
------
 * ISEARCH-5217 убираем кеширование tvm тикетов в tracker.bisearch совсем  [ https://github.yandex-team.ru/tools/intrasearch/commit/ce6f04e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-21 17:04:25+03:00

3.18.2
------
 * ISEARCH-5217 возвращаем кеширование tvm тикета в индексации трекера     [ https://github.yandex-team.ru/tools/intrasearch/commit/ead0b30 ]
 * ISEARCH-5241 ретраи при получении данных директории в tracker.bisearch  [ https://github.yandex-team.ru/tools/intrasearch/commit/055bc13 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-21 16:14:44+03:00

3.18.1
------
 * ISEARCH-5251 доступ для kiparis к админке в тестинге  [ https://github.yandex-team.ru/tools/intrasearch/commit/7ca6f3b ]
 * ISEARCH-5231 возвращаем utc в фильтр в idm.rolenodes  [ https://github.yandex-team.ru/tools/intrasearch/commit/06e5abb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-21 12:46:50+03:00

3.18.0
------
 * ISEARCH-5233 Версия саджеста со словарем в сниппетах (#515)  [ https://github.yandex-team.ru/tools/intrasearch/commit/4b7f50f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-20 13:36:50+03:00

3.17.7
------
 * ISEARCH-5231 фикс фильтра по ts в idm.rolenodes  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e77764 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-17 15:52:37+03:00

3.17.6
------
 * ISEARCH-5231 фикс фильтра по ts в idm.rolenodes  [ https://github.yandex-team.ru/tools/intrasearch/commit/f76c49e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-17 15:34:57+03:00

3.17.5
------
 * ISEARCH-5215 убираем регулярные переиндексации догмы  [ https://github.yandex-team.ru/tools/intrasearch/commit/c0e6751 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-17 15:08:58+03:00

3.17.4
------
 * ISEARCH-5229 фикс хлебных крошек в doc.external  [ https://github.yandex-team.ru/tools/intrasearch/commit/723fbac ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-14 19:45:36+03:00

3.17.3
------
 * ISEARCH-5231 доработки мониторинга полноты (#513)  [ https://github.yandex-team.ru/tools/intrasearch/commit/d7c3f8e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-14 19:18:38+03:00

3.17.2
------
 * ISEARCH-5234 саджест по переговоркам для ухуры (#514)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8a4e684 ]
 * ISEARCH-5224 ancestors в idm_groups (#512)             [ https://github.yandex-team.ru/tools/intrasearch/commit/460d43b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-14 17:32:28+03:00

3.17.1
------
 * ISEARCH-5232 закрываем выдачу xml в abovemeta  [ https://github.yandex-team.ru/tools/intrasearch/commit/9bd3a7f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-11 15:58:14+03:00

3.17.0
------
 * ISEARCH-5215 выключаем индексацию кода (#510)                               [ https://github.yandex-team.ru/tools/intrasearch/commit/d311865 ]
 * ISEARCH-5053 индексация и прием пушей фемиды с фильтром по вакансии (#511)  [ https://github.yandex-team.ru/tools/intrasearch/commit/215724f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-11 15:22:59+03:00

3.16.14
-------
 * фикс поиска по acl в b2b вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/bb2e536 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-09 18:06:04+03:00

3.16.13
-------
 * ISEARCH-5227 фикс modtime в вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/27a57a7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-09 17:02:39+03:00

3.16.12
-------
 * ISEARCH-5134 убираем группировку по сервисам и департаментам  [ https://github.yandex-team.ru/tools/intrasearch/commit/3ca2dec ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-09 16:31:23+03:00

3.16.11
-------
 * ISEARCH-5134 фикс перезапросов несуществующих департаментов  [ https://github.yandex-team.ru/tools/intrasearch/commit/80b16aa ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-09 16:15:39+03:00

3.16.10
-------
 * ISEARCH-5134 фикс перезапросов несуществующих департаментов  [ https://github.yandex-team.ru/tools/intrasearch/commit/439658b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-09 12:14:40+03:00

3.16.9
------
 * ISEARCH-5192 добавляем фактор urlhash в людей со стаффа и b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/390eba1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-08 19:26:18+03:00

3.16.8
------
 * ISEARCH-5219 добаляем dev в корс на тестинге b2b                    [ https://github.yandex-team.ru/tools/intrasearch/commit/59380f0 ]
 * ISEARCH-5134 убираем сервисы и департаменты из индекса организаций  [ https://github.yandex-team.ru/tools/intrasearch/commit/dce1578 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-08 18:31:04+03:00

3.16.7
------
 * ISEARCH-5175 максимальная длина поисковых атрибутов в str  [ https://github.yandex-team.ru/tools/intrasearch/commit/ffcd547 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-08 15:40:48+03:00

3.16.6
------
 * ISEARCH-5077 апишка мониторинга упавших индексаций  [ https://github.yandex-team.ru/tools/intrasearch/commit/d388050 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-08 14:23:17+03:00

3.16.5
------
 * ISEARCH-5175 не отправляем в саас слишком длинные атрибуты  [ https://github.yandex-team.ru/tools/intrasearch/commit/86d49e3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-08 12:16:31+03:00

3.16.4
------
 * ISEARCH-5203 recoverable DatabaseError  [ https://github.yandex-team.ru/tools/intrasearch/commit/2d30128 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-08 10:31:44+03:00

3.16.3
------
 * ISEARCH-5203 фикс пагинации в индексе  [ https://github.yandex-team.ru/tools/intrasearch/commit/0ce35d1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-07 19:46:19+03:00

3.16.2
------
 * ISEARCH-5203 фикс timestamp в индексациях  [ https://github.yandex-team.ru/tools/intrasearch/commit/fd3b44f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-07 19:08:33+03:00

3.16.1
------
 * ISEARCH-5203 апишка для мониторинга полноты данных в индексе (#509)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7c7ae58 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-07 17:00:54+03:00

3.16.0
------
 * ISEARCH-5219 проверка referer и валидация коллбэков в jsonp (#508)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7bf96f9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-07 12:07:26+03:00

3.15.17
-------
 * ISEARCH-5217 временно убираем кеширование tvm тикетов  [ https://github.yandex-team.ru/tools/intrasearch/commit/c318452 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-03 12:05:10+03:00

3.15.16
-------
 * ISEARCH-5214 абсолютные урлы в списке людей  [ https://github.yandex-team.ru/tools/intrasearch/commit/795b6b1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-02 15:50:16+03:00

3.15.15
-------
 * ISEARCH-5214 вызываем колдунщики только для первой страницы  [ https://github.yandex-team.ru/tools/intrasearch/commit/8620fdc ]
 * ISEARCH-5168 возвращаем replace_br                           [ https://github.yandex-team.ru/tools/intrasearch/commit/4fcfa8d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-02 13:04:26+03:00

3.15.14
-------
 * ISEARCH-5214 урлы на рассылки сервисов  [ https://github.yandex-team.ru/tools/intrasearch/commit/e1712c9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-01 17:12:54+03:00

3.15.13
-------
 * ISEARCH-5214 дефолтные названия ссылок  [ https://github.yandex-team.ru/tools/intrasearch/commit/c35077f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-01 17:01:12+03:00

3.15.12
-------
 * ISEARCH-5214 дефолтные названия ссылок  [ https://github.yandex-team.ru/tools/intrasearch/commit/8e7908e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-01 16:40:11+03:00

3.15.11
-------
 * ISEARCH-5214 обратная совместимость с xml  [ https://github.yandex-team.ru/tools/intrasearch/commit/3880855 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-01 15:36:02+03:00

3.15.10
-------
 * ISEARCH-5214 обратная совместимость с xml  [ https://github.yandex-team.ru/tools/intrasearch/commit/aaa1d8a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-01 15:24:17+03:00

3.15.9
------
 * ISEARCH-5214 очередь трекера в upper  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e94b50 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-01 15:03:39+03:00

3.15.8
------
 * ISEARCH-5214 сортировка контактов сервиса  [ https://github.yandex-team.ru/tools/intrasearch/commit/7890caf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-11-01 14:53:06+03:00

3.15.7
------
 * ISEARCH-5209 убираем текст из контекста  [ https://github.yandex-team.ru/tools/intrasearch/commit/9528294 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-31 16:30:43+03:00

3.15.6
------
 * ISEARCH-5196 сниппет вики public -> is_public  [ https://github.yandex-team.ru/tools/intrasearch/commit/c94af57 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-31 16:07:07+03:00

3.15.5
------
 * ISEARCH-5209 логирование с request_id в abovemeta (#507)  [ https://github.yandex-team.ru/tools/intrasearch/commit/b71bb92 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-31 15:49:00+03:00

3.15.4
------
 * ISEARCH-5196 абсолютные урлы в хлебных крошках на вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/65276db ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-31 13:31:45+03:00

3.15.3
------
 * ISEARCH-5032 (#506)  [ https://github.yandex-team.ru/tools/intrasearch/commit/5357fcc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-30 14:41:28+03:00

3.15.2
------
 * ISEARCH-5206 замена <b> на hlword в json  [ https://github.yandex-team.ru/tools/intrasearch/commit/20d8e9f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-30 12:17:17+03:00

3.15.1
------
 * ISEARCH-5121 фильтр по me() и вывод текущего пользователя первым в фасетах по author и assignee (#501)  [ https://github.yandex-team.ru/tools/intrasearch/commit/d89bc1e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-26 19:08:00+03:00

3.15.0
------
 * ISEARCH-5135 удаляем ненужные индексаторы (#502)                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/d787a0c ]
 * ISEARCH-5168 убираем склеивание нескольких тегов вместе в индексаторе трекера (#503)  [ https://github.yandex-team.ru/tools/intrasearch/commit/38b9c76 ]
 * ISEARCH-4882 не используем timeout при локах в run_check (#504)                       [ https://github.yandex-team.ru/tools/intrasearch/commit/067bc65 ]
 * ISEARCH-5196 доработки по вики json (#505)                                            [ https://github.yandex-team.ru/tools/intrasearch/commit/2b215f7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-26 18:36:02+03:00

3.14.16
-------
 * ISEARCH-5183 car.number пустая строка вместо null  [ https://github.yandex-team.ru/tools/intrasearch/commit/23b77af ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-26 15:05:17+03:00

3.14.15
-------
 * ISEARCH-5191 выводим work_phone вначале  [ https://github.yandex-team.ru/tools/intrasearch/commit/6dcf12e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 18:35:20+03:00

3.14.14
-------
 * ISEARCH-5191 подсветка в work_phone  [ https://github.yandex-team.ru/tools/intrasearch/commit/9d3ab0e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 18:11:21+03:00

3.14.13
-------
 * ISEARCH-5191 обратная совместимость с xml  [ https://github.yandex-team.ru/tools/intrasearch/commit/44a4368 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 17:43:30+03:00

3.14.12
-------
 * ISEARCH-5191 обратная совместимость с xml  [ https://github.yandex-team.ru/tools/intrasearch/commit/c667d0a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 17:38:31+03:00

3.14.11
-------
 * ISEARCH-5191 обратная совместимость с xml  [ https://github.yandex-team.ru/tools/intrasearch/commit/bc347cc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 17:32:15+03:00

3.14.10
-------
 * ISEARCH-5191 храним только upper версию номера  [ https://github.yandex-team.ru/tools/intrasearch/commit/e0f06a3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 16:55:43+03:00

3.14.9
------
 * ISEARCH-5191 фикс 500 при пустом car._forms  [ https://github.yandex-team.ru/tools/intrasearch/commit/4863b0a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 15:31:39+03:00

3.14.8
------
 * ISEARCH-5191 убираем лишние поля в сниппете людей (#500)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0cda2fb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-24 15:09:09+03:00

3.14.7
------
 * ISEARCH-5186 локальный кэш ревизий при обработке пушей стартрека (#499)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ea44071 ]
 * ISEARCH-5187 чиним просмотр поиска в b2b админке                         [ https://github.yandex-team.ru/tools/intrasearch/commit/b26881d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-23 19:09:44+03:00

3.14.6
------
 * ISEARCH-5065 обработка domain_master_changed в b2b (#498)  [ https://github.yandex-team.ru/tools/intrasearch/commit/4c4c9c6 ]
 * ISEARCH-5161 чистим обработку пушей в трекере              [ https://github.yandex-team.ru/tools/intrasearch/commit/94212e7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-23 18:00:25+03:00

3.14.5
------
 * ISEARCH-5174 убираем description=None из описания пустых тикетов (#497)  [ https://github.yandex-team.ru/tools/intrasearch/commit/cda03d5 ]
 * ISEARCH-5050 открываем вертикаль трекера                                 [ https://github.yandex-team.ru/tools/intrasearch/commit/f6f411f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-23 16:03:11+03:00

3.14.4
------
 * версия logbroker-client  [ https://github.yandex-team.ru/tools/intrasearch/commit/862fc39 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-23 14:34:25+03:00

3.14.3
------
 * ISEARCH-5117 ссылка на кулауд логи в админке  [ https://github.yandex-team.ru/tools/intrasearch/commit/eba748b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-23 14:30:54+03:00

3.14.2
------
 * ISEARCH-5117 логи celery в кулауде (#496)  [ https://github.yandex-team.ru/tools/intrasearch/commit/d1b2a42 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-23 13:51:08+03:00

3.14.1
------
 * фикс индексации людей  [ https://github.yandex-team.ru/tools/intrasearch/commit/ae96d8f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-23 13:30:01+03:00

3.14.0
------
 * ISEARCH-5183 доработки по json (#495)                  [ https://github.yandex-team.ru/tools/intrasearch/commit/df7b647 ]
 * ISEARCH-5044 мониторинг acl на вики и стартрек (#494)  [ https://github.yandex-team.ru/tools/intrasearch/commit/29be522 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-19 19:45:06+03:00

3.13.10
-------
 * ISEARCH-5120 фикс верстки в админке  [ https://github.yandex-team.ru/tools/intrasearch/commit/76cec79 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 17:23:40+03:00

3.13.9
------
 * ISEARCH-5120 доработки по пушам в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/bd94b36 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 16:54:11+03:00

3.13.8
------
 * ISEARCH-5120 включаем listen_startrek и в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/25b0a22 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 15:46:01+03:00

3.13.7
------
 * ISEARCH-5120 фикс переиндексации очередей при пушах  [ https://github.yandex-team.ru/tools/intrasearch/commit/92896de ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 15:24:09+03:00

3.13.6
------
 * ISEARCH-5120 фикс лога пушей + accept_pushed=true у трекера  [ https://github.yandex-team.ru/tools/intrasearch/commit/31a4c11 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 15:15:00+03:00

3.13.5
------
 * ISEARCH-5120 фикс переиндексации очередей  [ https://github.yandex-team.ru/tools/intrasearch/commit/e16cb1d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 14:36:27+03:00

3.13.4
------
 * ISEARCH-5120 переиндексируем таски только при изменении названий и пермишшено очередей и компонент  [ https://github.yandex-team.ru/tools/intrasearch/commit/0a595d8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 14:05:10+03:00

3.13.3
------
 * ISEARCH-5120 запускаем индексации пушей без локов  [ https://github.yandex-team.ru/tools/intrasearch/commit/1b58e7c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 12:42:41+03:00

3.13.2
------
 * ISEARCH-5120 запускаем индексации пушей без локов  [ https://github.yandex-team.ru/tools/intrasearch/commit/a3f1b72 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 12:24:26+03:00

3.13.1
------
 * ISEARCH-5120 фикс импортов  [ https://github.yandex-team.ru/tools/intrasearch/commit/6c99f68 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 11:45:49+03:00

3.13.0
------
 * ISEARCH-5120 фикс зависимостей                   [ https://github.yandex-team.ru/tools/intrasearch/commit/3333442 ]
 * ISEARCH-5020 заменяем кафку на логброкер (#491)  [ https://github.yandex-team.ru/tools/intrasearch/commit/dfa83a7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-18 11:24:37+03:00

3.12.19
-------
 * ISEARCH-5173 передаем acl ограничения в саас отдельным параметром (#493)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6340a86 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-17 17:04:55+03:00

3.12.18
-------
 * ISEARCH-5172 не выбираем все ревизии, если не считаем статистику по пушам  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e4f613 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-17 12:35:42+03:00

3.12.17
-------
 * ISEARCH-5136 фикс индексатора фемиды  [ https://github.yandex-team.ru/tools/intrasearch/commit/920ea17 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 17:05:55+03:00

3.12.16
-------
 * ISEARCH-5165 фикс форматирования номеров  [ https://github.yandex-team.ru/tools/intrasearch/commit/7cb37c2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 16:05:31+03:00

3.12.15
-------
 * отдельный oauth токен для кондуктора  [ https://github.yandex-team.ru/tools/intrasearch/commit/ec785a9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 15:33:02+03:00

3.12.14
-------
 * ISEARCH-5165 совсем устойчивы к отказу план апи  [ https://github.yandex-team.ru/tools/intrasearch/commit/cc0ef80 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 15:05:40+03:00

3.12.13
-------
 * ISEARCH-5165 фикс форматирования мотономера  [ https://github.yandex-team.ru/tools/intrasearch/commit/c5fd0c7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 14:55:41+03:00

3.12.12
-------
 * фикс вертикали стартрека  [ https://github.yandex-team.ru/tools/intrasearch/commit/e0a31a6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 14:15:44+03:00

3.12.11
-------
 * ISEARCH-5136 не падаем, если апи фемиды не отдает какие-то поля  [ https://github.yandex-team.ru/tools/intrasearch/commit/20172e5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 14:09:40+03:00

3.12.10
-------
 * ISEARCH-5160 настраиваем вывод дат в at.clubs  [ https://github.yandex-team.ru/tools/intrasearch/commit/9e3b940 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 12:08:16+03:00

3.12.9
------
 * ISEARCH-5160 настраиваем вывод дат в at.clubs  [ https://github.yandex-team.ru/tools/intrasearch/commit/a691ebc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-16 12:02:32+03:00

3.12.8
------
 * ISEARCH-5160 исправляем сниппеты этушки в json (#492)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ff724a4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-13 16:11:42+03:00

3.12.7
------
 * ISEARCH-5159 доработки по визардам в json  [ https://github.yandex-team.ru/tools/intrasearch/commit/0231d36 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-11 23:22:14+03:00

3.12.6
------
 * ISEARCH-5157 правильно выводим Access-Control-Allow-Credentials  [ https://github.yandex-team.ru/tools/intrasearch/commit/c72b449 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-10 16:13:22+03:00

3.12.5
------
 * ISEARCH-5157 правильно выводим Access-Control-Allow-Credentials  [ https://github.yandex-team.ru/tools/intrasearch/commit/9c0b7b6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-10 16:05:23+03:00

3.12.4
------
 * ISEARCH-5156 фиксы сниппетов стартрека  [ https://github.yandex-team.ru/tools/intrasearch/commit/78cb4cf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-10 15:45:55+03:00

3.12.3
------
 * ISEARCH-5156 фиксы сниппетов стартрека        [ https://github.yandex-team.ru/tools/intrasearch/commit/8a3be0f ]
 * ISEARCH-5136 добавление новых полей в фемиду  [ https://github.yandex-team.ru/tools/intrasearch/commit/051434d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-10 15:28:22+03:00

3.12.2
------
 * убираем django_pgaas  [ https://github.yandex-team.ru/tools/intrasearch/commit/eddcef3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-09 17:13:15+03:00

3.12.1
------
 * django_pgaas==0.1.0  [ https://github.yandex-team.ru/tools/intrasearch/commit/c3e4312 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-09 16:03:38+03:00

3.12.0
------
 * ISEARCH-5136 новые атрибуты в поиске по кандидатам (#490)  [ https://github.yandex-team.ru/tools/intrasearch/commit/49c98ce ]
 * убираем запуск никому не нужных расчетов                   [ https://github.yandex-team.ru/tools/intrasearch/commit/1cd038b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-09 13:39:07+03:00

3.11.20
-------
 * ISEARCH-5154 уникальные факторы по урлу в поиске по кандидатам  [ https://github.yandex-team.ru/tools/intrasearch/commit/0b01ef0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-06 12:42:12+03:00

3.11.19
-------
 * ISEARCH-5154 стат фактор по дате обновления  [ https://github.yandex-team.ru/tools/intrasearch/commit/cade90f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-06 11:36:32+03:00

3.11.18
-------
 * ISEARCH-5153 не выводим ошибку о пустом запросе, если одна ошибка уже есть  [ https://github.yandex-team.ru/tools/intrasearch/commit/f99256f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-05 16:07:32+03:00

3.11.17
-------
 * ISEARCH-5153 не выводим ошибку о пустом запросе, если одна ошибка уже есть  [ https://github.yandex-team.ru/tools/intrasearch/commit/050d397 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-05 15:58:37+03:00

3.11.16
-------
 * ISEARCH-5153 делаем явную проверку пришедших ревизий  [ https://github.yandex-team.ru/tools/intrasearch/commit/9912e0e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-05 15:54:39+03:00

3.11.15
-------
 * ISEARCH-5152 быстрый фикс для передачи kps  [ https://github.yandex-team.ru/tools/intrasearch/commit/fa14302 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-05 14:52:59+03:00

3.11.14
-------
 * ISEARCH-4947 убираем лишнюю точку при отсутствии component_name  [ https://github.yandex-team.ru/tools/intrasearch/commit/a93a859 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-04 17:56:26+03:00

3.11.13
-------
 * ISEARCH-4947 убираем лишнюю точку при отсутствии component_name  [ https://github.yandex-team.ru/tools/intrasearch/commit/b8ffc6a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-04 17:19:45+03:00

3.11.12
-------
 * ISEARCH-4947 индексируем в документации только main + причесываем сниппет (#489)  [ https://github.yandex-team.ru/tools/intrasearch/commit/a8e9233 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-04 16:52:58+03:00

3.11.11
-------
 * ISEARCH-5146 ошибки "ничего не найдено" и в xml (#488)  [ https://github.yandex-team.ru/tools/intrasearch/commit/22badba ]
 * ISEARCH-5082 возвращаем старые названия воркерам        [ https://github.yandex-team.ru/tools/intrasearch/commit/a72eaf6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-04 13:35:45+03:00

3.11.10
-------
 * ISEARCH-5082 рестартим локальные воркеры раз в 4 часа  [ https://github.yandex-team.ru/tools/intrasearch/commit/718d946 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-04 12:41:08+03:00

3.11.9
------
 * ISEARCH-5082 рестартим локальные воркеры раз в 4 часа  [ https://github.yandex-team.ru/tools/intrasearch/commit/718a3d6 ]
 * ISEARCH-5082 по крону рестартим локальные celery       [ https://github.yandex-team.ru/tools/intrasearch/commit/c2354de ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-03 19:08:32+03:00

3.11.8
------
 * ISEARCH-5082 по крону рестартим локальные celery (#487)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2097e4b ]
 * фикс обработки ошибок от jhist                           [ https://github.yandex-team.ru/tools/intrasearch/commit/a117517 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-03 19:01:07+03:00

3.11.7
------
 * ISEARCH-5129 дополняем meta                             [ https://github.yandex-team.ru/tools/intrasearch/commit/5ac4d1c ]
 * ISEARCH-5129 убираем фичу show_empty_response_warnings  [ https://github.yandex-team.ru/tools/intrasearch/commit/0fc754b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-03 16:08:19+03:00

3.11.6
------
 * ISEARCH-5129 фикс вывода ошибок в abovemeta  [ https://github.yandex-team.ru/tools/intrasearch/commit/44bf0ff ]
 * ISEARCH-4966 пробуем django_pgaas (#486)     [ https://github.yandex-team.ru/tools/intrasearch/commit/9eaeb32 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-03 15:07:07+03:00

3.11.5
------
 * ISEARCH-5114 обновление весов колдунщиков на метапоиске  [ https://github.yandex-team.ru/tools/intrasearch/commit/04cba0c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-02 15:04:53+03:00

3.11.4
------
 * ISEARCH-5114 обновление весов колдунщиков на метапоиске                    [ https://github.yandex-team.ru/tools/intrasearch/commit/af7f7fc ]
 * ISEARCH-5128 больше не падает индексация людей при косяках в апи планнера  [ https://github.yandex-team.ru/tools/intrasearch/commit/cf18688 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-10-02 14:58:25+03:00

3.11.3
------
 * ISEARCH-5086 логи ретраев  [ https://github.yandex-team.ru/tools/intrasearch/commit/b4ec597 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-28 16:29:10+03:00

3.11.2
------
 * ISEARCH-5086 raise revocerable errors  [ https://github.yandex-team.ru/tools/intrasearch/commit/d98bec8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-28 16:21:39+03:00

3.11.1
------
 * ISEARCH-5086 глобавльный кеш tvm-тикетов на все индексации  [ https://github.yandex-team.ru/tools/intrasearch/commit/5e01961 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-28 16:06:10+03:00

3.11.0
------
 * ISEARCH-5086 tvm при запросах в стартрек + переходим на /issues/_search (#484)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3ff9962 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-28 13:00:09+03:00

3.10.16
-------
 * ISEARCH-5124 выбираем для with_global только живые хосты  [ https://github.yandex-team.ru/tools/intrasearch/commit/aa519d5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-27 18:36:55+03:00

3.10.15
-------
 * ISEARCH-4518 возвращаем сбор глобальной статистики только с одного хоста  [ https://github.yandex-team.ru/tools/intrasearch/commit/533f374 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-27 16:34:32+03:00

3.10.14
-------
 * ISEARCH-4518 фикс сбора глобальной статистики  [ https://github.yandex-team.ru/tools/intrasearch/commit/faa8c9b ]
 * ISEARCH-4518 фикс сбора глобальной статистики  [ https://github.yandex-team.ru/tools/intrasearch/commit/dbcf463 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-27 16:26:57+03:00

3.10.13
-------
 * ISEARCH-4518 меняем базу в редисе + не пишем старые статусы в базу  [ https://github.yandex-team.ru/tools/intrasearch/commit/69fa06a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-27 16:10:48+03:00

3.10.12
-------
 * чиним миграцию  [ https://github.yandex-team.ru/tools/intrasearch/commit/8d5c2d7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-27 13:59:35+03:00

3.10.11
-------
 * ISEARCH-4518 собираем глобальную статистику по локу  [ https://github.yandex-team.ru/tools/intrasearch/commit/3e072be ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-26 18:59:01+03:00

3.10.10
-------
 * убираем ENABLE_NEW_WIKI_REINDEX  [ https://github.yandex-team.ru/tools/intrasearch/commit/7e7ed43 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-26 17:14:00+03:00

3.10.9
------
 * ISEARCH-4518 откатываем постоянный ретрай databaseerror  [ https://github.yandex-team.ru/tools/intrasearch/commit/9734b77 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-26 17:04:07+03:00

3.10.8
------
 * ISEARCH-4974 обновляем переводы  [ https://github.yandex-team.ru/tools/intrasearch/commit/1c807c3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-26 16:23:37+03:00

3.10.7
------
 * ISEARCH-4518 доработки статистики  [ https://github.yandex-team.ru/tools/intrasearch/commit/dd8be38 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-26 14:51:56+03:00

3.10.6
------
 * ISEARCH-4518 доработки переделки статистики (#485)     [ https://github.yandex-team.ru/tools/intrasearch/commit/3f17253 ]
 * ISEARCH-5119 фикс индексации людей без роли в сервисе  [ https://github.yandex-team.ru/tools/intrasearch/commit/ed1cc38 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-26 13:29:53+03:00

3.10.5
------

* [Alexander Koshelev](http://staff/alexkoshelev@yandex-team.ru)

 * ISEARCH-4518: Переписать подсчет статистики индексации (#254)  [ https://github.yandex-team.ru/tools/intrasearch/commit/949825f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-20 19:28:11+03:00

3.10.4
------
 * ISEARCH-5108 фикс KeyError  [ https://github.yandex-team.ru/tools/intrasearch/commit/de04c9c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-18 13:43:47+03:00

3.10.3
------
 * ISEARCH-5108 скрываем варнинги за фичу  [ https://github.yandex-team.ru/tools/intrasearch/commit/294669f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-18 13:24:03+03:00

3.10.2
------
 * ISEARCH-5108 добавляем варнинги в случае пустого ответа (#483)                              [ https://github.yandex-team.ru/tools/intrasearch/commit/39ab3ad ]
 * ISEARCH-4971 убираем "попробуйте позже" из  error_auth                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/b9deef3 ]
 * ISEARCH-5106 убираем фичу abovemeta_new_error_format. теперь ошибки всегда в новом формате  [ https://github.yandex-team.ru/tools/intrasearch/commit/98aece7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-18 12:42:36+03:00

3.10.1
------
 * ISEARCH-4974 потерянный translations  [ https://github.yandex-team.ru/tools/intrasearch/commit/8762787 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-15 11:13:18+03:00

3.10.0
------
 * ISEARCH-4974 перевод ошибок через gettext (#482)  [ https://github.yandex-team.ru/tools/intrasearch/commit/dc8050a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-15 10:47:43+03:00

3.9.7
-----
 * ISEARCH-5110 абсолютные урлы в хлебных крошках  [ https://github.yandex-team.ru/tools/intrasearch/commit/9073132 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-14 15:51:07+03:00

3.9.6
-----
 * ISEARCH-5031 всем сниппетам проставляем url  [ https://github.yandex-team.ru/tools/intrasearch/commit/fb1b715 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-14 15:06:16+03:00

3.9.5
-----
 * ISEARCH-5104 чиним индексацию st.queues (#481)                  [ https://github.yandex-team.ru/tools/intrasearch/commit/31e0808 ]
 * ISEARCH-5103 вынимаем из-за фичи колдунщик людей на вики в b2b  [ https://github.yandex-team.ru/tools/intrasearch/commit/5b9abdc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-14 12:03:03+03:00

3.9.4
-----
 * ISEARCH-5102 не ходим в базу в _fill_factors_info  [ https://github.yandex-team.ru/tools/intrasearch/commit/84190f2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-13 16:39:55+03:00

3.9.3
-----
 * ISEARCH-5102 quick fix - ходим в salve в _fill_factors_info  [ https://github.yandex-team.ru/tools/intrasearch/commit/c3ae401 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-13 12:16:59+03:00

3.9.2
-----
 * ISEARCH-5100 возвращаем nav саджест в version=0  [ https://github.yandex-team.ru/tools/intrasearch/commit/3f0a588 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-12 14:43:22+03:00

3.9.1
-----
 * ISEARCH-5098 индексируем пуши стартрека в real time  [ https://github.yandex-team.ru/tools/intrasearch/commit/1184df5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-12 13:07:22+03:00

3.9.0
-----
 * ISEARCH-5031 сортировка в вики фасетах (#480)                                                                                 [ https://github.yandex-team.ru/tools/intrasearch/commit/488d9ee ]
 * ISEARCH-5098 индексатор стартрека в keys теперь принимает и номера тикетов + умеет переиндексировать удаленные тикеты (#479)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6bf97ab ]
 * ISEARCH-5095 убираем автоматическую группировку по людям (#478)                                                               [ https://github.yandex-team.ru/tools/intrasearch/commit/28266fc ]
 * ISEARCH-5029 настраиваем хождение по ipv6 из докера на isearch.dev (#477)                                                     [ https://github.yandex-team.ru/tools/intrasearch/commit/9ae7876 ]
 * ISEARCH-5081 выключаем стадию контент вообще у всех                                                                           [ https://github.yandex-team.ru/tools/intrasearch/commit/16ffbab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-11 16:51:40+03:00

3.8.14
------
 * ISEARCH-5096 удаляем удаленные документы из индекса в doc  [ https://github.yandex-team.ru/tools/intrasearch/commit/6d4cddd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-07 14:48:29+03:00

3.8.13
------
 * ISEARCH-5096 фикс индексации документации  [ https://github.yandex-team.ru/tools/intrasearch/commit/fac1fc7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-07 13:34:00+03:00

3.8.12
------
 * ISEARCH-5096 фикс индексации документации  [ https://github.yandex-team.ru/tools/intrasearch/commit/59d8b93 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-07 13:04:24+03:00

3.8.11
------
 * ISEARCH-5031 фикс версии саджеста  [ https://github.yandex-team.ru/tools/intrasearch/commit/692e84e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-06 20:32:17+03:00

3.8.10
------
 * ISEARCH-5095 меняем ссылку на команду сервиса  [ https://github.yandex-team.ru/tools/intrasearch/commit/ed584c2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-06 16:00:44+03:00

3.8.9
-----
 * ISEARCH-5004 факторы по количеству просмотров в документации (#474)  [ https://github.yandex-team.ru/tools/intrasearch/commit/125a9e2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-06 12:47:22+03:00

3.8.8
-----
 * ISEARCH-5031 doc_index в json выдаче          [ https://github.yandex-team.ru/tools/intrasearch/commit/8673cfc ]
 * ISEARCH-5081 выключаем стадию content у вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/bcf122f ]
 * ISEARCH-5081 выключаем стадию content у вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/66b6922 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-09-05 13:11:28+03:00

3.8.7
-----
 * ISEARCH-5071 фикс пагинатора в админке (#476)  [ https://github.yandex-team.ru/tools/intrasearch/commit/cbcec61 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-31 18:44:05+03:00

3.8.6
-----
 * ISEARCH-5048 - фикс индексации навигационного саджеста  [ https://github.yandex-team.ru/tools/intrasearch/commit/5c6a622 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-31 16:58:36+03:00

3.8.5
-----
 * ISEARCH-5048 - убираем state=frozen из индексаторов сервисов  [ https://github.yandex-team.ru/tools/intrasearch/commit/1184f65 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-31 16:28:06+03:00

3.8.4
-----
 * ISEARCH-5070 убираем вертикаль и колдунщик по проектам (#475)  [ https://github.yandex-team.ru/tools/intrasearch/commit/a0fc030 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-31 15:58:37+03:00

3.8.3
-----
 * Isearch 5004 (#473)  [ https://github.yandex-team.ru/tools/intrasearch/commit/89a2a93 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-30 17:25:31+03:00

3.8.2
-----
 * ISEARCH-5004 добавляем факторы по дате изменения, создания и зону с ключевыми словами в документацию (#472)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6fce256 ]
 * ISEARCH-5031 команда для генерации схемы сниппетов                                                           [ https://github.yandex-team.ru/tools/intrasearch/commit/0567cee ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-30 15:57:40+03:00

3.8.1
-----
 * ISEARCH-5056 фикс индексации стартрека  [ https://github.yandex-team.ru/tools/intrasearch/commit/48d9a9b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-29 17:29:53+03:00

3.8.0
-----
 * ISEARCH-5031 json в выдаче поиска (#467)  [ https://github.yandex-team.ru/tools/intrasearch/commit/05f62fd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-29 12:25:04+03:00

3.7.13
------
 * ISEARCH-4556 perPage=100 в запросах к стартреку  [ https://github.yandex-team.ru/tools/intrasearch/commit/5f84f58 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-28 16:31:41+03:00

3.7.12
------
 * ISEARCH-4556 добавляем возможность индексировать дельту стартрека (#471)  [ https://github.yandex-team.ru/tools/intrasearch/commit/db2c1a7 ]
 * добавляем в голован трекер                                                [ https://github.yandex-team.ru/tools/intrasearch/commit/6c95b1c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-28 15:52:13+03:00

3.7.11
------
 * ISEARCH-5048: Убрал получение сервисов для стейта frozen (#470)  [ https://github.yandex-team.ru/tools/intrasearch/commit/56bacd60 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-08-07 19:40:26+03:00

3.7.10
------
 * ISEARCH-5028 фикс индексации внутреннего поиска  [ https://github.yandex-team.ru/tools/intrasearch/commit/5457c95 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-03 18:41:24+03:00

3.7.9
-----
 * ISEARCH-5028 убираем None из описания  [ https://github.yandex-team.ru/tools/intrasearch/commit/e0104a5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-03 16:04:43+03:00

3.7.8
-----
 * ISEARCH-5028 скрываем вертикаль поиска по трекеру                    [ https://github.yandex-team.ru/tools/intrasearch/commit/4d60b11 ]
 * ISEARCH-5037 учимся перенастраивать хосты визарда через фичу (#469)  [ https://github.yandex-team.ru/tools/intrasearch/commit/a2f95d0 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-03 15:10:50+03:00

3.7.7
-----
 * ISEARCH-5028 открываем вертикаль b2b трекера  [ https://github.yandex-team.ru/tools/intrasearch/commit/6b5a9c8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-01 19:15:52+03:00

3.7.6
-----
 * ISEARCH-5028 фикс индексации внутреннего трекера  [ https://github.yandex-team.ru/tools/intrasearch/commit/bc50780 ]
 * ISEARCH-5028 фикс индексации внутреннего трекера  [ https://github.yandex-team.ru/tools/intrasearch/commit/23a1ec5 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-08-01 18:34:40+03:00

3.7.5
-----
 * ISEARCH-5028 acl tracker b2b (#468)  [ https://github.yandex-team.ru/tools/intrasearch/commit/b53e56a ]
 * ISEARCH-5040 чиним саджест в b2b     [ https://github.yandex-team.ru/tools/intrasearch/commit/dd06229 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-31 18:58:38+03:00

3.7.4
-----
 * ISEARCH-5015 Фикс мониторинга активных ревизий  [ https://github.yandex-team.ru/tools/intrasearch/commit/8be610f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-24 14:25:50+03:00

3.7.3
-----
 * ISEARCH-5015 поиск по b2b стартреку (#463)  [ https://github.yandex-team.ru/tools/intrasearch/commit/10583bf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-24 12:02:07+03:00

3.7.2
-----
 * ISEARCH-4616 фикс передачи хедеров в ml  [ https://github.yandex-team.ru/tools/intrasearch/commit/3d3b08d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-20 14:54:18+03:00

3.7.1
-----
 * ISEARCH-4893: Не ходить в ручку департаментов (#466)  [ https://github.yandex-team.ru/tools/intrasearch/commit/57bd4bc1 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-07-20 13:54:43+03:00

3.7
---
 * ISEARCH-4616 tvm в подписках (#447)               [ https://github.yandex-team.ru/tools/intrasearch/commit/3ed2dd4 ]
 * [откат] переиндексации idm в отдельный компонент  [ https://github.yandex-team.ru/tools/intrasearch/commit/7a06930 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-20 11:54:05+03:00

3.6.9
-----
 * переиндексации idm в отдельный компонент  [ https://github.yandex-team.ru/tools/intrasearch/commit/d079ef7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-19 11:59:22+03:00

3.6.8
-----
 * ISEARCH-5025 дополнительные атрибуты для femida.candidates (#465)  [ https://github.yandex-team.ru/tools/intrasearch/commit/806a5d3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-18 13:32:56+03:00

3.6.7
-----
 * ISEARCH-4725 фикс фильтров по фасетам в вики  [ https://github.yandex-team.ru/tools/intrasearch/commit/cbd9687 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-17 15:46:50+03:00

3.6.6
-----
 * ISEARCH-4725 соединяем несколько значений одного фасета через И  [ https://github.yandex-team.ru/tools/intrasearch/commit/7589b64 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-14 15:32:40+03:00

3.6.5
-----
 * ISEARCH-4892 multy errors bugfix (#462)  [ https://github.yandex-team.ru/tools/intrasearch/commit/de06cedd ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-07-13 16:30:50+03:00

3.6.4
-----
 * ISEARCH-4725 возвращаем старый вид ошибок об отстуствии текста запроса (#460)  [ https://github.yandex-team.ru/tools/intrasearch/commit/4dfd2fc ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-12 16:22:15+03:00

3.6.3
-----
 * ISEARCH-4892 Разделил AuthStep на isearch и bisearch (#459)  [ https://github.yandex-team.ru/tools/intrasearch/commit/1d35c6f1 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-07-12 15:01:13+03:00

3.6.2
-----
 * ISEARCH-4892 Не ходим в ручку организаций (#458)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9f0876b6 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-07-12 13:52:24+03:00

3.6.1
-----
 * ISEARCH-4725 - фикс поиска по avg grade в фемиде  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e5ff33 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-12 12:35:56+03:00

3.6.0
-----
 * ISEARCH-4725 дополнительные фильтры в метапоиске (#457)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7b9360d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-11 17:46:25+03:00

3.5.4
-----
 * ISEARCH-4851 упрощаем запись в searchlog  [ https://github.yandex-team.ru/tools/intrasearch/commit/d086935 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-06 14:41:51+03:00

3.5.3
-----
 * ISEARCH-5009 [b2b] фикс синхронизации сервисов  [ https://github.yandex-team.ru/tools/intrasearch/commit/eead498 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-04 12:03:37+03:00

3.5.2
-----
 * ISEARCH-5009 [b2b] в department url на самом деле label => убираем валидацию  [ https://github.yandex-team.ru/tools/intrasearch/commit/0962214 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-04 11:45:28+03:00

3.5.1
-----
 * ISEARCH-5008 [b2b] переименовываем визард людей  [ https://github.yandex-team.ru/tools/intrasearch/commit/9d5989c ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-03 14:27:17+03:00

3.5.0
-----
 * ISEARCH-5008 переименовываем визард людей в b2b                                 [ https://github.yandex-team.ru/tools/intrasearch/commit/a3490f6 ]
 * ISEARCH-4982 [b2b] обрабытваем только пуши об интересующих нас сервисах (#456)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c753074 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-07-03 14:13:34+03:00

3.4.2
-----
 * ISEARCH-4994 - cors headers в abovemeta (#455)  [ https://github.yandex-team.ru/tools/intrasearch/commit/5d46258 ]
 * убираем лишние логи                             [ https://github.yandex-team.ru/tools/intrasearch/commit/6aa4902 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-27 16:27:03+03:00

3.4.1
-----
 * индексируем jhist из кулауда  [ https://github.yandex-team.ru/tools/intrasearch/commit/bd5cf1d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-26 14:23:31+03:00

3.4.0
-----
 * индексируем jhist из кулауда  [ https://github.yandex-team.ru/tools/intrasearch/commit/e35f6cf ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-26 13:25:03+03:00

3.3.8
-----
 * ISEARCH-4993 выключаем переиндексацию коммитов каждый час  [ https://github.yandex-team.ru/tools/intrasearch/commit/b100074 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-22 19:40:21+03:00

3.3.7
-----
 * ISEARCH-4965 меняем формат типа ошибки и прячем атрибуты за фичу (#454)  [ https://github.yandex-team.ru/tools/intrasearch/commit/31db3bb ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-21 15:21:39+03:00

3.3.6
-----
 * фича bisearch_wiki_people_wizard  в админке  [ https://github.yandex-team.ru/tools/intrasearch/commit/2e9602d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-20 18:48:53+03:00

3.3.5
-----
 * ISEARCH-4969 не удаляем дубликаты в поиске по кандидатам (#453)  [ https://github.yandex-team.ru/tools/intrasearch/commit/687d111 ]
 * ISEARCH-4965 сообщения об ошибках в abovemeta (#452)             [ https://github.yandex-team.ru/tools/intrasearch/commit/85ab7d5 ]
 * убираем спам в сентри от ids.connector                           [ https://github.yandex-team.ru/tools/intrasearch/commit/b74196e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-20 14:35:50+03:00

3.3.4
-----
 * ISEARCH-4763 mini fix баги в админке интрасерча  [ https://github.yandex-team.ru/tools/intrasearch/commit/3fce0167 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-06-16 17:01:00+03:00

3.3.3
-----
 * ISEARCH-4763 - лениво получаем api директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/d5c06e9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-16 16:36:57+03:00

3.3.2
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4933 убираем всю подсветку сниппетов в commitssearch  [ https://github.yandex-team.ru/tools/intrasearch/commit/eae357a5 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4763 Проверка валидности токена (#451)  [ https://github.yandex-team.ru/tools/intrasearch/commit/d498c817 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-06-16 15:23:53+03:00

3.3.1
-----
 * ISEARCH-4970 добавляем org_directory_id и общий status_code в searchlog  [ https://github.yandex-team.ru/tools/intrasearch/commit/027e5ab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-15 18:04:32+03:00

3.3.0
-----
 * ISEARCH-4953 логи на обновление индексаций (#450)  [ https://github.yandex-team.ru/tools/intrasearch/commit/4e1986f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-09 16:37:53+03:00

3.2.2
-----
 * ISEARCH-4949 чиним джобы yt (#449)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8e9ebab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-07 16:35:57+03:00

3.2.1
-----
 * ISEARCH-4960 исправляем 500 в саджесте bisearch.people (#448)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9b85d0b ]
 * ISEARCH-4703 прячем колдунщик людей за фичу (#446)             [ https://github.yandex-team.ru/tools/intrasearch/commit/59be3c1 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-06 17:17:38+03:00

3.2.0
-----
 * ISEARCH-4943 не отправляем в сентри ошибки от ids (#443)                             [ https://github.yandex-team.ru/tools/intrasearch/commit/765a547 ]
 * ISEARCH-4952 учимся саджестить idm начиная с середины слага (#444)                   [ https://github.yandex-team.ru/tools/intrasearch/commit/34b0b98 ]
 * ISEARCH-4703 колдущик людей на вертикали вики + чиним поиск людей по группам (#445)  [ https://github.yandex-team.ru/tools/intrasearch/commit/22c1e1b ]
 * Останавливаем бомбу в тасках                                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/48ae31e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-06-05 14:01:01+03:00

3.1.2
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * Isearch 4842 обработка удаленных организаций (#440)      [ https://github.yandex-team.ru/tools/intrasearch/commit/79074f8 ]
 * ISEARCH-4925 фикс индексации в новую ревизию (#441)      [ https://github.yandex-team.ru/tools/intrasearch/commit/80fca06 ]
 * ISEARCH-4661 не прячем сообщение об ошибке в map (#442)  [ https://github.yandex-team.ru/tools/intrasearch/commit/f7964c5 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4844 поправил миграцию  [ https://github.yandex-team.ru/tools/intrasearch/commit/bf0c8ab ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-29 12:49:06+03:00

3.1.1
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4927: Ошибки в сочетании << и почти пустого запроса при поиске (#436)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ed0e311a ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4936 фикс получения урла роботного пользователя (#437)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9b7c52c3 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4844 Поправил лог пушей директории (#438)            [ https://github.yandex-team.ru/tools/intrasearch/commit/cadf8281 ]
 * ISEARCH-4913 Переиндексация candidatesearch в 2 ночи (#439)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0637cc31 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-26 16:56:21+03:00

3.1.0
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4903 не падаем при получении неизвестной организации (#435)  [ https://github.yandex-team.ru/tools/intrasearch/commit/9abd5be ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4900 Перешел на внутренние хосты API Директории (#433)  [ https://github.yandex-team.ru/tools/intrasearch/commit/f02d0fd ]

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4930: Регулярная переиндексация коммитов (#434)              [ https://github.yandex-team.ru/tools/intrasearch/commit/41fbf71 ]
 * ISEARCH-4923: Считать количество страниц коммитов по группам (#432)  [ https://github.yandex-team.ru/tools/intrasearch/commit/dfbf85a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-25 15:23:01+03:00

3.0.3
-----
 * ISEARCH-4827 убираем спам в лог из админки  [ https://github.yandex-team.ru/tools/intrasearch/commit/a612a60 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-23 17:53:37+03:00

3.0.2
-----
 * ISEARCH-4827 фикс проверки саджеста из админки  [ https://github.yandex-team.ru/tools/intrasearch/commit/df0004e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-23 17:42:36+03:00

3.0.1
-----
 * ISEARCH-4827 фикс названий архивов для yt  [ https://github.yandex-team.ru/tools/intrasearch/commit/304b240 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-23 16:46:56+03:00

3.0.0
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * releasing version 1.9.11                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/faa0a89 ]
 * ISEARCH-4869 фикс индексации алиасов                             [ https://github.yandex-team.ru/tools/intrasearch/commit/ecb9881 ]
 * releasing version 1.9.10                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/ef78adb ]
 * ISEARCH-4885 ищем только в body при поиске по кандидатам (#430)  [ https://github.yandex-team.ru/tools/intrasearch/commit/046b517 ]
 * ISEARCH-4869 добавляем алиасы к s_suggest в rolenode (#428)      [ https://github.yandex-team.ru/tools/intrasearch/commit/2aa2031 ]
 * ISEARCH-4914 правильно передаем токены в запрос за рассылками    [ https://github.yandex-team.ru/tools/intrasearch/commit/3a75c74 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * releasing version 1.9.9                            [ https://github.yandex-team.ru/tools/intrasearch/commit/ad09857 ]
 * ISEARCH-4898 крошки теперь относительные (#429)    [ https://github.yandex-team.ru/tools/intrasearch/commit/31b1c35 ]
 * releasing version 1.9.8                            [ https://github.yandex-team.ru/tools/intrasearch/commit/80c8b57 ]
 * ISEARCH-4898 Поправили фасеты документации (#427)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ed6e34a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-23 14:19:00+03:00

2.1.7
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4827 никогда не подсвечиваем урлы в сниппетах (#431)             [ https://github.yandex-team.ru/tools/intrasearch/commit/f0bd804 ]
 * ISEARCH-4827 xss в просмотре поиска в админке                            [ https://github.yandex-team.ru/tools/intrasearch/commit/3cdaf33 ]
 * правильно логируем ошибки из sources.doc.external                        [ https://github.yandex-team.ru/tools/intrasearch/commit/e775c89 ]
 * releasing version 1.9.7                                                  [ https://github.yandex-team.ru/tools/intrasearch/commit/6152801 ]
 * ISEARCH-4869 учимся задавать чистый on/off в правилах колдунщика         [ https://github.yandex-team.ru/tools/intrasearch/commit/a58f171 ]
 * releasing version 1.9.6                                                  [ https://github.yandex-team.ru/tools/intrasearch/commit/a0fdfdb ]
 * ISEARCH-4869 учимся задавать чистый on/off в правилах колдунщика (#426)  [ https://github.yandex-team.ru/tools/intrasearch/commit/cac074a ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * releasing version 1.9.5                                 [ https://github.yandex-team.ru/tools/intrasearch/commit/a69a098 ]
 * ISEARCH-4898 Поправил определение типов страниц (#425)  [ https://github.yandex-team.ru/tools/intrasearch/commit/81f7c2a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-23 12:18:46+03:00

2.1.6
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4827 избавляемся от 500 и 404 в админке        [ https://github.yandex-team.ru/tools/intrasearch/commit/88437ab ]
 * Isearch 4827 - подготовка к слиянию с мастером (#421)  [ https://github.yandex-team.ru/tools/intrasearch/commit/54d6281 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * UrlBulder bugfix  [ https://github.yandex-team.ru/tools/intrasearch/commit/e5283a7 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-16 16:19:44+03:00

2.1.5
-----
 * ISEARCH-4827 Фиксы после мержа с мастером  [ https://github.yandex-team.ru/tools/intrasearch/commit/8d97d72 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-12 14:43:50+03:00

2.1.4
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * releasing version 1.8.13                                [ https://github.yandex-team.ru/tools/intrasearch/commit/37b2f25 ]
 * отправляем регулярки кондуктора на отдельный компонент  [ https://github.yandex-team.ru/tools/intrasearch/commit/d06f33b ]
 * releasing version 1.8.12                                [ https://github.yandex-team.ru/tools/intrasearch/commit/3305030 ]
 * ISEARCH-4829 application/json в саджесте (#399)         [ https://github.yandex-team.ru/tools/intrasearch/commit/90a87c2 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * releasing version 1.9.4                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/d30e6cd ]
 * ISEARCH-4898 Добавил заголовок и убрал format из endpoint (#420)              [ https://github.yandex-team.ru/tools/intrasearch/commit/8a5ecb5 ]
 * releasing version 1.9.3                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/c4c091b ]
 * ISEARCH-4898 Поправил места, в которых не правильно генерировался урл (#418)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3657b67 ]
 * releasing version 1.9.2                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/dd3a50f ]
 * ISEARCH-4898 Поправил схему в походах к doc                                   [ https://github.yandex-team.ru/tools/intrasearch/commit/f1a0a32 ]
 * releasing version 1.9.1                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/f9fae7d ]
 * ISEARCH-4898 поправил урлы в поиске по документации                           [ https://github.yandex-team.ru/tools/intrasearch/commit/c939639 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-12 13:28:24+03:00

2.1.3
-----
 * ISEARCH-4881 увеличили время ожидания ответа от каталога вики в b2b до 10 секунд (#419)  [ https://github.yandex-team.ru/tools/intrasearch/commit/2e7886b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-11 17:10:23+03:00

2.1.2
-----
 * ISEARCH-4895 снизил нагрузку на вики до 25%  [ https://github.yandex-team.ru/tools/intrasearch/commit/4d364986 ]
 * ISEARCH-4877 Добавил дашборд голована        [ https://github.yandex-team.ru/tools/intrasearch/commit/b66af507 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-03 18:50:47+03:00

2.1.1
-----
 * ISEARCH-4873 уменьшаем таймаут кеша в run_check  [ https://github.yandex-team.ru/tools/intrasearch/commit/ea93613 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-27 18:31:14+03:00

2.1.0
-----

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-27 17:03:08+03:00

2.0.38
------
 * ISEARCH-4877 Изменил стат ручку (#417)  [ https://github.yandex-team.ru/tools/intrasearch/commit/bbae6353 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-27 15:59:17+03:00

2.0.37
------
 * ISEARCH-4872 убираем новую переиндексацию вики за переменную окружения   [ https://github.yandex-team.ru/tools/intrasearch/commit/272e9c6 ]
 * ISEARCH-4883 убираем подсветку из логина на вертикали директории         [ https://github.yandex-team.ru/tools/intrasearch/commit/47dd978 ]
 * ISEARCH-4883 убираем подсветку из рабочей почты на вертикали директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/60d1d81 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-27 14:27:57+03:00

2.0.36
------
 * ISEARCH-4873 utc время для orgs_with_changes  [ https://github.yandex-team.ru/tools/intrasearch/commit/eda96d3 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-26 20:15:00+03:00

2.0.35
------
 * ISEARCH-4873 неблокирующая блокировка на run_check  [ https://github.yandex-team.ru/tools/intrasearch/commit/d8bcf06 ]
 * ISEARCH-4873 добавляем логи                         [ https://github.yandex-team.ru/tools/intrasearch/commit/29944a9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-26 19:07:45+03:00

2.0.34
------
 * ISEARCH-4873 индексируем организации изменившиеся за последние 2 часа  [ https://github.yandex-team.ru/tools/intrasearch/commit/20d9bff ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-26 17:24:37+03:00

2.0.33
------
 * ISEARCH-4873 фикс названия настройки  [ https://github.yandex-team.ru/tools/intrasearch/commit/f9791a8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-26 16:40:41+03:00

2.0.32
------
 * ISEARCH-4872 индексируем только измененные организации вики (#415)             [ https://github.yandex-team.ru/tools/intrasearch/commit/6108989 ]
 * ISEARCH-4873 правильно считаем fail_rate при загрузке индексера из ин… (#416)  [ https://github.yandex-team.ru/tools/intrasearch/commit/c3b8632 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-26 16:13:41+03:00

2.0.31
------
 * ISEARCH-4873 переделка чеков (#412)  [ https://github.yandex-team.ru/tools/intrasearch/commit/7a5cdc6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-25 19:09:07+03:00

2.0.30
------
 * ISEARCH-4879 урлы на аватарке в саджесте людей директории (#414)  [ https://github.yandex-team.ru/tools/intrasearch/commit/82d0f1e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-25 13:53:16+03:00

2.0.29
------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4852 переименовываем фасеты в en версии  [ https://github.yandex-team.ru/tools/intrasearch/commit/b30d6ddd ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4832 Оптимизировал мониторинг активной ревизии  [ https://github.yandex-team.ru/tools/intrasearch/commit/2abff38d ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-24 19:22:58+03:00

2.0.28
------
 * ISEARCH-4875 чиним саджест  [ https://github.yandex-team.ru/tools/intrasearch/commit/62146c6 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-24 13:07:34+03:00

2.0.27
------
 * ISEARCH-4841 обрабатываем JSONDecodeError (#411)  [ https://github.yandex-team.ru/tools/intrasearch/commit/88d8475 ]
 * ISEARCH-4823 обрабатываем NoNodeError (#410)      [ https://github.yandex-team.ru/tools/intrasearch/commit/5039ef4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-21 17:54:27+03:00

2.0.26
------
 * sygopt fix  [ https://github.yandex-team.ru/tools/intrasearch/commit/502b95aa ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-21 15:00:27+03:00

2.0.25
------
 * console container fix + api urls fix  [ https://github.yandex-team.ru/tools/intrasearch/commit/514b8cd9 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-21 13:58:43+03:00

2.0.24
------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4868 урлы в сниппетах вики (#408)  [ https://github.yandex-team.ru/tools/intrasearch/commit/b63116f1 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4870 Графики индексаций  [ https://github.yandex-team.ru/tools/intrasearch/commit/f8f65cda ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-21 13:26:56+03:00

2.0.23
------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4865 name в директории не обязательный  [ https://github.yandex-team.ru/tools/intrasearch/commit/036b2b3b ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * Revert "ISEARCH-4791 lxml -> defusedxml"  [ https://github.yandex-team.ru/tools/intrasearch/commit/9a8f2a98 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-19 18:23:34+03:00

2.0.22
------
 * ISEARCH-4845 выбираем давно не индексировававшиеся организации  [ https://github.yandex-team.ru/tools/intrasearch/commit/9fff224 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-18 17:51:04+03:00

2.0.21
------
 * ISEARCH-4858 увеличиваем таймаут для restart_stale_check  [ https://github.yandex-team.ru/tools/intrasearch/commit/3337185 ]
 * ISEARCH-4858 фикс получения тасок без чека (#404)         [ https://github.yandex-team.ru/tools/intrasearch/commit/6fdfe4d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-18 12:59:09+00:00

2.0.19
------
 * ISEARCH-4791 lxml -> defusedxml  [ https://github.yandex-team.ru/tools/intrasearch/commit/d86c8479 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-17 18:20:41+03:00

2.0.18
------
 * ISEARCH-4845 массовая переиндексация вики (#402)             [ https://github.yandex-team.ru/tools/intrasearch/commit/fc8b8d3 ]
 * ISEARCH-4852 названия фасетов на вертикали директории        [ https://github.yandex-team.ru/tools/intrasearch/commit/dfbf14b ]
 * ISEARCH-4852 переименование фасетов на вертикали директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/30cb63e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-14 18:51:47+03:00

2.0.17
------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * больше ссылок на организацию в админке!  [ https://github.yandex-team.ru/tools/intrasearch/commit/291a3dc0 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4832 Поправил формат и условие мониторинга  [ https://github.yandex-team.ru/tools/intrasearch/commit/905a5d52 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-13 18:53:52+03:00

2.0.16
------
 * ISERCH-4832 Изменил формат мониторинга ревизий  [ https://github.yandex-team.ru/tools/intrasearch/commit/faf0493b ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-12 18:15:38+03:00

2.0.15
------
 * ISEARCH-4832 Добавил мониторинг активных ревизий  [ https://github.yandex-team.ru/tools/intrasearch/commit/91f3c9c6 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-12 17:30:41+03:00

2.0.14
------
 * ISEARCH-4833 фикс запроса департаментов  [ https://github.yandex-team.ru/tools/intrasearch/commit/572fd24 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-11 18:04:53+03:00

2.0.13
------
 * фикс запуска abovemeta  [ https://github.yandex-team.ru/tools/intrasearch/commit/9e2e424 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-11 18:12:42+04:00

2.0.12
------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * по умолчанию индексируем не real_time  [ https://github.yandex-team.ru/tools/intrasearch/commit/8db10f52 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4815 suggest работает без search_result          [ https://github.yandex-team.ru/tools/intrasearch/commit/e5a14f1f ]
 * ISEARCH-4795 Вынес общую логику хендлеров в MainHandler  [ https://github.yandex-team.ru/tools/intrasearch/commit/21b577e0 ]
 * ISEARCH-4795 Перенес handlers в отдельный файл           [ https://github.yandex-team.ru/tools/intrasearch/commit/845c39b8 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-04-07 19:31:21+03:00

2.0.11
------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4828 запрашиваем робота поиска у директории по nickname (#396)  [ https://github.yandex-team.ru/tools/intrasearch/commit/d17dd9e ]
 * ISEARCH-4825 не подсвечиваем url по умолчанию (#395)                    [ https://github.yandex-team.ru/tools/intrasearch/commit/b3e9782 ]
 * ISEARCH-4822 фикс ошибок об отсутствующих организациях                  [ https://github.yandex-team.ru/tools/intrasearch/commit/3daaad8 ]
 * фикс вывода сервисов организации                                        [ https://github.yandex-team.ru/tools/intrasearch/commit/6d09025 ]
 * ISEARCH-4810 улучшаем логирование запросов к директории из abovemeta    [ https://github.yandex-team.ru/tools/intrasearch/commit/1ef9ee4 ]
 * ISEARCH-4810 ссылка на саджест со страницы организации                  [ https://github.yandex-team.ru/tools/intrasearch/commit/c726cfd ]
 * ISEARCH-4807 - поиск по организациям в админке                          [ https://github.yandex-team.ru/tools/intrasearch/commit/c14cc29 ]

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4702: Правильный урл надметапоиска в тестинге и проде (#394)  [ https://github.yandex-team.ru/tools/intrasearch/commit/0e6e120 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-07 19:35:05+04:00

2.0.10
------
 * countdown при старте индексации для чека
 * ISEARCH-4816: запускаем статиста как раньше
 * Revert "ISEARCH-4816: Считать статистику индексаций последовательно"

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-04-07 13:13:59+03:00

2.0.9
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4801: Добавить опцию пусто при выборе суффикса в админке
 * batch_reindex_wiki
 * Фикс настроек запуска чека и статистов
 * ISEARCH-4818: Должна быть хотя бы одна активная ревизия
 * ISEARCH-4816: Считать статистику индексаций последовательно
 * ISEARCH-4702: Просмотр поисков и саджеста в админке (#386)

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4820 фикс подсветки найденного
 * фикс расписания индексации для isearch

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * oauth settings name fix

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-04-06 23:45:17+03:00

2.0.8
-----
 * ISEARCH-4811 фикс вывода урла на пользователей  [ https://github.yandex-team.ru/tools/intrasearch/commit/43acb60 ]
 * ISEARCH-4812 фикс сериализации дней рождений    [ https://github.yandex-team.ru/tools/intrasearch/commit/68d5515 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-05 15:47:00+04:00

2.0.7
-----
 * releasing version 1.8.11                                                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/9cf453a ]
 * ISEARCH-4808 выключаем сбор статистики пушей по настройке и убираем транзакции из group_attr  [ https://github.yandex-team.ru/tools/intrasearch/commit/01c3a6a ]
 * releasing version 1.8.10                                                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/0692995 ]
 * фиксы индексации кандидатов фемиды                                                            [ https://github.yandex-team.ru/tools/intrasearch/commit/fd5a2d9 ]
 * releasing version 1.8.9                                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/75e7553 ]
 * включаем регулярные переиндексации кондуктора и выключаем accept_pushes у него                [ https://github.yandex-team.ru/tools/intrasearch/commit/537ab02 ]
 * releasing version 1.8.8                                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/c5a95e5 ]
 * Фикс индексатора групп idm                                                                    [ https://github.yandex-team.ru/tools/intrasearch/commit/2b7fc61 ]
 * releasing version 1.8.7                                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/1cef5ce ]
 * времено выключаем постоянные переиндексации кондуткора                                        [ https://github.yandex-team.ru/tools/intrasearch/commit/ba617b2 ]
 * releasing version 1.8.6                                                                       [ https://github.yandex-team.ru/tools/intrasearch/commit/d2d287f ]
 * Фикс фильтра по updated_at кондуктора                                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/59623b2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-04 18:12:56+04:00

2.0.6
-----

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4790 вернул старые настройки логгинга celery

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-04-03 17:24:27+03:00

2.0.5
-----
 * ISEARCH-4793 зонный фактор по позиции       [ https://github.yandex-team.ru/tools/intrasearch/commit/8a5d847 ]
 * ISEARCH-4793 ищем пользователей по позиции  [ https://github.yandex-team.ru/tools/intrasearch/commit/7af9124 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-03 17:31:29+04:00

2.0.4
-----
 * ISEARCH-4767 добавляем локальное кеширование http стадий директории  [ https://github.yandex-team.ru/tools/intrasearch/commit/fc6b113 ]
 * ISEARCH-4799 переименовываем вертикаль директории                    [ https://github.yandex-team.ru/tools/intrasearch/commit/ad2fb04 ]
 * не пятисотим при ошибке валидации формы в _abovemeta                 [ https://github.yandex-team.ru/tools/intrasearch/commit/93cbdb2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-03 15:00:26+04:00

2.0.3
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4789: Выдать доступ к админке egorova@  [ https://github.yandex-team.ru/tools/intrasearch/commit/3ab2af67 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4779 Поправил отдачу логов в админке                [ https://github.yandex-team.ru/tools/intrasearch/commit/c3790d93 ]
 * ISEARCH-4773 Падаю если нет ревизий для search_results      [ https://github.yandex-team.ru/tools/intrasearch/commit/d1ec0c15 ]
 * ISEARCH-4783 Правильно обрабатываю пользовательские группы  [ https://github.yandex-team.ru/tools/intrasearch/commit/8acd973f ]
 * ISEARCH-4769 Добавляю X-Request-ID к запросам               [ https://github.yandex-team.ru/tools/intrasearch/commit/1880422c ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-03-31 16:30:48+03:00

2.0.2
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * Фикс celerybit schedule
 * ISEARCH-4676 заменяем урл фемиды для теста
 * ISEARCH-4676 фикс продакшен урла фемиды
 * ISEARCH-4501 готовим кондуктор к запуску

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Регулярные индексации джаббера отправлять в компоненты, настроенные для jabber
 * В индексаторе нужно название очереди без суффикса (#372)

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-03-29 16:04:52+03:00

2.0.1
-----
 * ISEARCH-4770 фикс индексации директории без фильтров  [ https://github.yandex-team.ru/tools/intrasearch/commit/600801d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-27 20:06:35+04:00

2.0
---

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Фикс changelog после мержа
 * restart_stale_check нужен в обоих конфигах селерибита (#366)
 * Дефолтное количество партиций в индексаторе - 1
 * Фикс чекина хоста в базе и работы с суффиксом при запуске селери
 * Правки docker-compose

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4776 Поправил получение логина

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-03-27 18:21:04+03:00

1.5.bisearch.21
---------------

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4766 логируем, если пришло несколько организаций                                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/0b279be ]
 * ISEARCH-4766 использование tvm тикетов для походов в директорию                                               [ https://github.yandex-team.ru/tools/intrasearch/commit/d4d58f6 ]
 * ISEARCH-4770 добавляем синхронизацию пользователей при изменении групп и департаментов                        [ https://github.yandex-team.ru/tools/intrasearch/commit/2e36a28 ]
 * ISEARCH-4780 улучшаем логирование в сентри                                                                    [ https://github.yandex-team.ru/tools/intrasearch/commit/f98ad24 ]

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Правки docker-compose                                                          [ https://github.yandex-team.ru/tools/intrasearch/commit/0413531 ]
 * Правки для bisearch после мержа мастера                                        [ https://github.yandex-team.ru/tools/intrasearch/commit/832d6da ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-27 15:47:14+04:00

1.9.11
------
 * ISEARCH-4869 фикс индексации алиасов  [ https://github.yandex-team.ru/tools/intrasearch/commit/ecb9881 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-19 19:38:22+03:00

1.9.10
------
 * ISEARCH-4885 ищем только в body при поиске по кандидатам (#430)  [ https://github.yandex-team.ru/tools/intrasearch/commit/046b517 ]
 * ISEARCH-4869 добавляем алиасы к s_suggest в rolenode (#428)      [ https://github.yandex-team.ru/tools/intrasearch/commit/2aa2031 ]
 * ISEARCH-4914 правильно передаем токены в запрос за рассылками    [ https://github.yandex-team.ru/tools/intrasearch/commit/3a75c74 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-19 17:13:58+03:00

1.9.9
-----
 * ISEARCH-4898 крошки теперь относительные (#429)  [ https://github.yandex-team.ru/tools/intrasearch/commit/31b1c352 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-19 15:55:10+03:00

1.9.8
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * правильно логируем ошибки из sources.doc.external  [ https://github.yandex-team.ru/tools/intrasearch/commit/e775c894 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4898 Поправили фасеты документации (#427)  [ https://github.yandex-team.ru/tools/intrasearch/commit/ed6e34a1 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-18 16:55:34+03:00

1.9.7
-----
 * ISEARCH-4869 учимся задавать чистый on/off в правилах колдунщика  [ https://github.yandex-team.ru/tools/intrasearch/commit/a58f171 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-17 19:18:44+03:00

1.9.6
-----
 * ISEARCH-4869 учимся задавать чистый on/off в правилах колдунщика (#426)  [ https://github.yandex-team.ru/tools/intrasearch/commit/cac074a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-05-17 18:33:51+03:00

1.9.5
-----
 * ISEARCH-4898 Поправил определение типов страниц (#425)  [ https://github.yandex-team.ru/tools/intrasearch/commit/81f7c2a0 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-17 17:24:00+03:00

1.9.4
-----
 * ISEARCH-4898 Добавил заголовок и убрал format из endpoint (#420)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8a5ecb51 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-11 16:16:50+03:00

1.9.3
-----
 * ISEARCH-4898 Поправил места, в которых не правильно генерировался урл (#418)  [ https://github.yandex-team.ru/tools/intrasearch/commit/3657b675 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-10 21:10:14+03:00

1.9.2
-----
 * ISEARCH-4898 Поправил схему в походах к doc  [ https://github.yandex-team.ru/tools/intrasearch/commit/f1a0a321 ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-10 16:53:27+03:00

1.9.1
-----
 * ISEARCH-4898 поправил урлы в поиске по документации  [ https://github.yandex-team.ru/tools/intrasearch/commit/c939639d ]

[Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru) 2017-05-10 15:54:13+03:00

1.8.13
------
 * отправляем регулярки кондуктора на отдельный компонент  [ https://github.yandex-team.ru/tools/intrasearch/commit/d06f33b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-12 14:57:50+03:00

1.8.12
------
 * ISEARCH-4829 application/json в саджесте (#399)  [ https://github.yandex-team.ru/tools/intrasearch/commit/90a87c2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-11 14:36:47+00:00

1.8.11
------
 * ISEARCH-4808 выключаем сбор статистики пушей по настройке и убираем транзакции из group_attr  [ https://github.yandex-team.ru/tools/intrasearch/commit/01c3a6a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-04-04 17:39:41+04:00

1.8.10
------
 * фиксы индексации кандидатов фемиды  [ https://github.yandex-team.ru/tools/intrasearch/commit/fd5a2d9 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-31 14:23:55+04:00

1.8.9
-----
 * включаем регулярные переиндексации кондуктора и выключаем accept_pushes у него  [ https://github.yandex-team.ru/tools/intrasearch/commit/537ab02 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-31 12:28:37+04:00

1.8.8
-----
 * Фикс индексатора групп idm  [ https://github.yandex-team.ru/tools/intrasearch/commit/2b7fc61 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-30 18:30:52+04:00

1.8.7
-----
 * времено выключаем постоянные переиндексации кондуткора  [ https://github.yandex-team.ru/tools/intrasearch/commit/ba617b2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-30 16:01:34+04:00

1.8.6
-----
 * Фикс фильтра по updated_at кондуктора  [ https://github.yandex-team.ru/tools/intrasearch/commit/59623b2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-29 16:38:40+04:00

1.8.5
-----
 * Фикс celerybit schedule  [ https://github.yandex-team.ru/tools/intrasearch/commit/3181763 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-29 14:04:49+04:00

1.8.4
-----
 * Фикс celerybit schedule  [ https://github.yandex-team.ru/tools/intrasearch/commit/f8d564d ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-29 13:52:24+04:00

1.8.3
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Регулярные индексации джаббера отправлять в компоненты, настроенные для jabber  [ https://github.yandex-team.ru/tools/intrasearch/commit/5cd14d2 ]
 * В индексаторе нужно название очереди без суффикса (#372)                        [ https://github.yandex-team.ru/tools/intrasearch/commit/2371202 ]

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * Фикс celerybit schedule  [ https://github.yandex-team.ru/tools/intrasearch/commit/3da4fa8 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-29 13:15:37+04:00

1.8.2
-----
 * ISEARCH-4676 заменяем урл фемиды для теста  [ https://github.yandex-team.ru/tools/intrasearch/commit/d94bd33 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-28 17:00:09+04:00

1.8.1
-----
 * ISEARCH-4676 фикс продакшен урла фемиды  [ https://github.yandex-team.ru/tools/intrasearch/commit/c4aafe4 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-28 08:44:01+04:00

1.8
---
 * ISEARCH-4501 готовим кондуктор к запуску  [ https://github.yandex-team.ru/tools/intrasearch/commit/81ad765 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-27 19:30:54+04:00

1.7.4
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Дефолтное количество партиций в индексаторе - 1  [ https://github.yandex-team.ru/tools/intrasearch/commit/7c86f47 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-03-27 14:20:22+00:00

1.7.3
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Фикс чекина хоста в базе и работы с суффиксом при запуске селери  [ https://github.yandex-team.ru/tools/intrasearch/commit/9eb9822 ]
 * Правки docker-compose                                             [ https://github.yandex-team.ru/tools/intrasearch/commit/bb95482 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-03-27 13:23:16+00:00

1.7.2
-----
 * Скачиваем леммер из sandbox                          [ https://github.yandex-team.ru/tools/intrasearch/commit/ccd466f ]
 * Избавление от fabfile.py                             [ https://github.yandex-team.ru/tools/intrasearch/commit/b4ad21b ]
 * Фикс проверки очередей при генерации конфига celery  [ https://github.yandex-team.ru/tools/intrasearch/commit/4605ff7 ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-03-23 07:08:08+00:00

1.7.1
---
 * Переключание на Ubuntu 14.04 Trusty  [ https://github.yandex-team.ru/tools/intrasearch/commit/1dbde5c ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-03-22 17:28:51+00:00

1.7
-----

* [Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru)

 * Упрощение конфигурации логгинга внутри celery                                [ https://github.yandex-team.ru/tools/intrasearch/commit/8f23e77 ]
 * Прокидывание полной конфигурации celery воркеров через переменные окружения  [ https://github.yandex-team.ru/tools/intrasearch/commit/7c440c8 ]
 * Используем gunicorn и для разработки                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/bcfce9f ]
 * Уровень логирования supervisord задается переменной окружения                [ https://github.yandex-team.ru/tools/intrasearch/commit/5acc55b ]
 * Используем supervisord из pypi                                               [ https://github.yandex-team.ru/tools/intrasearch/commit/26fcc7c ]
 * Наследование в docker-compose                                                [ https://github.yandex-team.ru/tools/intrasearch/commit/1bd9c53 ]
 * Использование ENTRYPOINT и другой раскладки конфигов supervisord             [ https://github.yandex-team.ru/tools/intrasearch/commit/bf32d96 ]
 * Использование ENTRYPOINT и другой раскладки конфигов supervisord             [ https://github.yandex-team.ru/tools/intrasearch/commit/57d9571 ]

* [Alexander Koshelev](http://staff/alexkoshelev@yandex-team.ru)

 * избавился от пакета headless (#348)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8762d2f ]

[Alex Koshelev](http://staff/alexkoshelev@yandex-team.ru) 2017-03-22 15:05:01+00:00

1.6.2
-----
 * ISEARCH-4676 доработки по поиску кандидатов  [ https://github.yandex-team.ru/tools/intrasearch/commit/9f61a3b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-20 20:20:05+04:00

1.6.1
-----
 * ISEARCH-4757 - индексируем дельту idm раз в час        [ https://github.yandex-team.ru/tools/intrasearch/commit/7b8f1ae ]
 * ISEARCH-4723 избавляемся от тысяч зон в idm_rolenodes  [ https://github.yandex-team.ru/tools/intrasearch/commit/6adb99e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-20 20:02:18+04:00

1.6
---

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4676 поиск по найму. начало.                                             [ https://github.yandex-team.ru/tools/intrasearch/commit/9bf038e ]
 * ISEARCH-4735 новые стат факторы в саджест по группам idm и фикс реквест билдера  [ https://github.yandex-team.ru/tools/intrasearch/commit/4c2de14 ]

* [Alexander Koshelev](http://staff/alexkoshelev@yandex-team.ru)

 * Правка использования Docker (#335)  [ https://github.yandex-team.ru/tools/intrasearch/commit/8bf782f ]

* [knopka](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4715: При рестаре celery не рестартятся очереди с walk (#340)  [ https://github.yandex-team.ru/tools/intrasearch/commit/155a1f7 ]

* [Alexander Lavrukov](http://staff/lavrukov@yandex-team.ru)

 * ISEARCH-4582 Раскомментировал хедеры sentry  [ https://github.yandex-team.ru/tools/intrasearch/commit/4753072 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-16 19:22:04+04:00

1.5.3
-----
 * ISEARCH-4721 ускоряем саджест по пустым запросам  [ https://github.yandex-team.ru/tools/intrasearch/commit/f8c9d8f ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-09 19:01:31+04:00

1.5.2
-----
 * ISEARCH-4721 фикс parent_path в idm.rolenodes                                              [ https://github.yandex-team.ru/tools/intrasearch/commit/0e77739 ]
 * ISEARCH-4711 добавляем описание в саджест по рассылкам и поле is_robot в саджест по людям  [ https://github.yandex-team.ru/tools/intrasearch/commit/c72766e ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-09 16:20:47+04:00

1.5.1
-----
 * Доступы в админку для новых членов команды

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-03-06 15:27:24+03:00

1.5
---
 * ISEARCH-4690 добавляем фильтры по дате изменения в индексатор idm  [ https://github.yandex-team.ru/tools/intrasearch/commit/a0ea458 ]
 * ISEARCH-4689 окончательно избавляемся от mysql                     [ https://github.yandex-team.ru/tools/intrasearch/commit/e62f3dd ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-03-01 14:23:46+04:00

1.4.1
-----
 * ISEARCH-4656 включаем регулярные переиндексации idm правильно  [ https://github.yandex-team.ru/tools/intrasearch/commit/94d1c55 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-20 18:59:56+04:00

1.4
---

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-20 14:56:35+04:00

1.3.9
-----
 * ISEARCH-4674 фикс урлов на таски кондуктора  [ https://github.yandex-team.ru/tools/intrasearch/commit/bf49017 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-17 19:38:18+04:00

1.3.8
-----
 * ISEARCH-4669 принимаем пуши кондуктора                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/bbaf6ee ]
 * ISEARCH-4668 индексация тикетов кондуктора                                     [ https://github.yandex-team.ru/tools/intrasearch/commit/7e82679 ]
 * ISEARCH-4669 меняем факторы кондуктора                                         [ https://github.yandex-team.ru/tools/intrasearch/commit/9cdc73a ]
 * ISEARCH-4673 поиск по таскам кондуктора                                        [ https://github.yandex-team.ru/tools/intrasearch/commit/d183a62 ]
 * ISEARCH-4667 фикс авторизации в кондукторе                                     [ https://github.yandex-team.ru/tools/intrasearch/commit/c2cc202 ]
 * ISEARCH-4667 принимаем пуши от кондуктора + фильтруем по последним изменениям  [ https://github.yandex-team.ru/tools/intrasearch/commit/fa175a2 ]
 * ISEARCH-4669 обход потери кондукторных прав в тестинге                         [ https://github.yandex-team.ru/tools/intrasearch/commit/19339b6 ]
 * ISEARCH-4669 переход на api v2 кондуктора                                      [ https://github.yandex-team.ru/tools/intrasearch/commit/fe5fd52 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-17 17:37:27+04:00

1.3.7
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4674 меняем время выгрузки задач в yt  [ https://github.yandex-team.ru/tools/intrasearch/commit/f866993 ]

* [knopka](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4625: Рестартить celery в qloud (#309)  [ https://github.yandex-team.ru/tools/intrasearch/commit/6879ced ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-17 17:07:52+04:00

1.3.6
-----
 * ISEARCH-4670 чиним неуникальные урлы у групп idm  [ https://github.yandex-team.ru/tools/intrasearch/commit/2a0322b ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-15 16:56:23+04:00

1.3.5
-----
 * ISEARCH-4656 Регулярные переиндексации idm  [ https://github.yandex-team.ru/tools/intrasearch/commit/8e68cbd ]
 * ISEARCH-4619 фикс 500 в саджестах           [ https://github.yandex-team.ru/tools/intrasearch/commit/85c6970 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-14 15:34:49+04:00

1.3.4
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4663 фикс экспорта даты в kiwi merge  [ https://github.yandex-team.ru/tools/intrasearch/commit/d5013ee ]
 * ISEARCH-4662 Фильтр по слагу в idm/rolenodes  [ https://github.yandex-team.ru/tools/intrasearch/commit/142c569 ]

* [knopka](http://staff/knopka@yandex-team.ru)

 * Update README.md  [ https://github.yandex-team.ru/tools/intrasearch/commit/88e403a ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-13 17:00:58+04:00

1.3.3
-----
 * ISEARCH-4659 явно включаем все апишки на слейв

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-09 16:42:08+03:00

1.3.2
-----
 * ISEARCH-4654 Параллельная индексация idm
 * ISEARCH-4575 фикс datasourses для дева

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-08 14:57:55+03:00

1.3.1
-----
 * ISEARCH-4575: Фикс определения токена в индексациях вики и коммитов
 * ISEARCH-4575: Фикс определения токена для yt
 * ISEARCH-4575: правильный oauth в QueuesStep

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-02-06 17:02:59+03:00

1.3
---
 * ISEARCH-4575: Удален intrasearch_oauth из devds
 * ISEARCH-4575: удален ненужный комментарий
 * ISEARCH-4575: токен для yt получаем одинаково во всех окружениях
 * ISEARCH-4575: .isearch добавлен в gitignore
 * ISEARCH-4575: OAuth токены для девелопмента в секретном файле
 * ISEARCH-4575: Спрятать OAuth токены в datasources

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-02-06 15:07:38+03:00

1.2.10
------
 * ISEARCH-4569 Починить индексацю infradocs

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-06 13:23:49+03:00

1.2.9
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4645 оптимизация in в facet_labels для pgaas
 * ISEARCH-4620 id в саджесте по rolenodes
 * ISEARCH-4641 лок в yt export_searchlog

* [knopka](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4496: Новый адрес апи этушки в продакшене (#291)

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4437: Поменять адрес опечаточника в проде

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-03 13:49:24+03:00

1.2.8
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4512 mysql to postgresql migration
 * ISEARCH-4620 по настоящему уникальные айдишники у систем

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4607: Удалены ненужные requirements.txt
 * ISEARCH-4607: Удалила неактуальные команды из fabfile
 * ISEARCH-4607: container_name в docker compose
 * ISEARCH-4607: Питон-зависимости ставятся до копирования папок проекта

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-02-01 19:29:20+03:00

1.2.7
-----
 * ISEARCH-4620 по настоящему уникальные айдишники у систем

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-01-27 16:35:58+03:00

1.2.6
-----
 * ISEARCH-4617 индексируем rolenodes по 1000 штук на страницу
 * ISEARCH-4620 добавляем фильтр по parent_path в idm.rolenodes

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-01-27 15:57:21+03:00

1.2.5
-----

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4612 фикс 500 в саджесте с пробелами

* [knopka](http://staff/knopka@yandex-team.ru)

 * Isearch 4609 - Фиксы сборки, правки для yt (#285)

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH 4609: забытый up версии tornado

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-01-26 14:39:15+03:00

1.2.4
-----
 * ISEARCH-4572 чиним просмотр саджеста/поиска на тесте

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-01-25 12:18:44+03:00

1.2.3
-----

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-01-25 11:43:37+03:00

1.2.2
-----
 * ISEARCH-4572 система в idm rolenodes и другие доработки

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-01-24 18:00:05+03:00

1.2
---

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4557 регулярный запуск export_searchlog                        [ https://github.yandex-team.ru/tools/intrasearch/commit/520a5fd ]
 * ISEARCH-4557 команда для заполнения пустых данных в searchlogrecord    [ https://github.yandex-team.ru/tools/intrasearch/commit/e97d34f ]
 * ISEARCH-4597 убираем необходимость передачи пользователей в abovemeta  [ https://github.yandex-team.ru/tools/intrasearch/commit/bf30953 ]
 * ISEARCH-4586 фикс загрузки сообщений из эластика в detailview session  [ https://github.yandex-team.ru/tools/intrasearch/commit/4baabc0 ]

* [knopka](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4496: Доступ к Этушке и замена хоста/урла  [ https://github.yandex-team.ru/tools/intrasearch/commit/276a5e2 ]

[Taisiya Malikova](http://staff/tmalikova@yandex-team.ru) 2017-01-24 17:04:19+04:00

1.1
---

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * ISEARCH-4598: admin utils
 * ISEARCH-4598: 404 при проверке поиска в деве
 * Правки docker-compose: имена образов, более правильный mount
 * Конвертация changelog
 * ISEARCH-4325: Переезд Поиска в Qloud
 * ISEARCH-4590: Отключить рестарт селери в продакшене

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH-4557 исправляем миграции удаления мусорных сессий
 * ISEARCH-4471 описание сниппета стартрека
 * ISEARCH-4571 добавляем возможность пустого запроса в саджесте
 * ISEARCH-4557 переносим миграции
 * ISEARCH-4586 фикс импорта статистики запросов из эластика
 * ISEARCH-4557 добавляем схему в таблички yt
 * ISEARCH-4557 scope по умолчанию в логах
 * ISEARCH-4557 расширяем статистику по кликам и доавбялем команду выгрузки таблиц в yt
 * ISEARCH-4556 не создаем пустые сессии
 * ISEARCH-4556 не учитываем поиск по коммитам в пользовательских сессиях
 * ISEARCH-4566 убираем 500 в саджесте без авторизации
 * ISEARCH-4587 добавляем пользователя в get параметры саджеста

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-01-23 15:03:11+03:00

1.0.14.13
---------
 * Возможно включать и выключать переиндексации через переменные окружения
 * ISEARCH-4496: Доступ к Этушке и замена хоста/урла
 * В образ добавлен yt
 * Включен listener для стартрека

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-01-19 17:55:05+03:00

1.0.14.11
---------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Прокидывать Authorization если есть

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-01-11 18:47:02

1.0.14.10
---------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Revert "preload в конфиге gunicorn в надметапоиске"
 * Правильный адрес для логов в логстеше

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2017-01-11 16:36:18

1.0.14.9
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * preload в конфиге gunicorn в надметапоиске

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-27 18:59:53

1.0.14.8
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * tornado 4\.4\.2
 * В девелопменте запускать веб\-часть без гуникорна

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-26 17:46:07

1.0.14.7
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Использовать CurlAsyncHTTPClient в надметапоиске

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-26 16:04:37

1.0.14.6
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * celeryopts неправильно определяла суффикс

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-21 21:04:52

1.0.14.5
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Фикс heartbeat

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-21 20:15:49

1.0.14.4
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Индекс на status и backend для индексации
 * Статика в админке

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-21 20:14:08

1.0.14.3
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Фикс настроек celery в production
 * Фикс обновления info у ноды

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-19 17:55:40

1.0.14.1
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * В админке рассчитывать на то, что не всегда для ноды есть info

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-19 13:16:49

1.0.14
------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Временно отключаем переиндексацию в production для кулауда
 * В node добавила данные про суффикс
 * Настройки подключения к зукиперу в деве
 * Подняла версию ylock
 * Фикс логгирования
 * Правки для запуска в девелопменте
 * Количество воркеров гуникорна берем из WEB\_CONCURRENCY

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-15 16:51:42

1.0.13.1
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Host в запросе в блекбокс берем из переменных окружения
 * Фикс именования базового образа в push\_to\_registry
 * Фикс запуска селери контейнеров

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-13 14:48:08

1.0.13
------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * В настройках лои апи и админки были перепутаны
 * Правильный форматтер для логов логстеша
 * Вернула запуск отдельного образа в fabric
 * Или партиция, или суффикс
 * Фикс сборки \(два докер\-образа\)

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-12 17:16:27

1.0.12.2
--------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Путь до пинга в апи
 * пинг в надметапоиске

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-08 15:41:24

1.0.12
------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * zookeeper в docker compose
 * логирование в индексациях
 * Путь до апи в настройках для дева
 * Суффикс в админке
 * Суффик правильно проставляем для очередей celery
 * Настройки суффиксов воркеров
 * Запуск индексаций через compose
 * Редис кладет данные в эфемерный диск
 * Правильный путь при запуске индексации

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-12-06 15:16:57

1.0.11
------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * По одному волку на инстанс
 * Партиции не нужны
 * fetch local app
 * Убрать партиции для не\-волков
 * в push\_to\_registry не было api, добавила

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-30 16:40:11

1.0.10
------

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Revert "fetch \- глобальная и обязательная стадия"
 * Revert "fetch глобальный"
 * Забытые зависимости для yt
 * Запускать все от www\-data
 * Уровень логов в супервизоре для isearch
 * Везде меняем права на датасорсы
 * docker\-compose для админки, апи, надметапоиска
 * Возможность слать в регистри не все образы
 * fetch глобальный
 * Временно выключила пуши от стартрека
 * Возвращаем redis
 * debug из переменной окружения
 * concurrency для celery
 * Не нужно смотреть на QLOUD\_ENVIRONMENT
 * Возможность задавать воркеры селери через переменную окружения
 * fetch \- глобальная и обязательная стадия
 * Настраиваемый celeryopts
 * Конфиги celery \+ скрипт для запуска
 * Отдельная бд в монге для qloud

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-25 17:28:09

1.0.9
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * логирование для supervisord

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-16 13:06:33

1.0.8
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Настройки logstash
 * Удаляем logstash из логирования в деве

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-15 20:17:17

1.0.7
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * user\_session\_id в саджесте

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-14 13:21:25

1.0.6
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Не нужно пробрасывать хедеры в запросе к апи из надметапоиска

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-12 12:06:06

1.0.5
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * verify\_false в запросах из торнадо
 * Не логировать некоторые параметры
 * Используем правильные сертификаты для запросов
 * Пуш в регистри в fabfile
 * Вернула сокет для логстеша
 * Фикс auth степа

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-11 19:51:41

1.0.4
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * AuthStep ходит в blackbox напрямую
 * Мелкие фиксы
 * фиксы логирования
 * Фикс настроек
 * Временно отключила логи в sentry
 * Разрешить ipv6 в запросах торнадо
 * Фикс логирования
 * Настройки путей до апи в тестинге и проде
 * Фикс урлов админки
 * Выкинула еще немного лишнего из зависимостей

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-10 15:58:21

1.0.3
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Выкинула настройки баз в тестинге
 * Настройки гуникорна

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-03 17:46:07

1.0.2
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Порты у supervisord

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-02 19:03:58

1.0.1
-----

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Logstash
 * Правки настроек

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-11-02 17:48:13

1.0
---

* [Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru)

 * Прокидывание портов в докерфайлах
 * Revert "Changelog"
 * Логирование в json
 * Dockerfile
 * Удалила ненужные настройки
 * changelog fix
 * Запускалка одного контейнера
 * Правильные права на папку для celery\-beat
 * celery beat
 * Правки генерилки конфигов для селери
 * Минимальные настройки celery
 * Changelog
 * Удалила почти всю дебиан папку
 * Для девелопмента менять только concurrency в celery
 * Запуск celery
 * Настройки редиса \(работают\)
 * Настройки редиса \(не работают\)
 * админка и индексации \(редис\)
 * надметапоиск
 * случайные фиксы
 * копируем в intrasearch
 * Установка
 * Зависимости докер

* [Taisiya Malikova](http://staff/tmalikova@yandex-team.ru)

 * ISEARCH\-4451 убираем лишнее из пассажей кондуктора
 * ISEARCH\-4410 прибираемся в тестах
 * ISEARCH\-3826 \- дополнительные параметры при просмотре саджеста в админке
 * ISEARCH\-3826 \- добавляем в админку саджеста ссылки на запросы

[Nataliya Kryuchkova](http://staff/knopka@yandex-team.ru) 2016-10-28 16:22:16

0.1099
---

  * ISEARCH-4570: Отдельные саджесты по юзерам и группам в idm

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-12-28 20:25:47

0.1098
---

  * ISEARCH-4568 добавляем first и last name в выдачу саджеста idm\_persons

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-28 18:54:59

0.1097
---

  * ISEARCH-4543 параллелим волки в индексаторе кондуктора
  * ISEARCH-4546 улучшаем админку сажеста
  * ISEARCH-3291 - фактор по устаревшим вики страницам

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-23 12:06:57

0.1096
---

  * ISEARCH-4560 меняем staff.yandex.ru на staff.y-t.ru

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-22 11:15:23

0.1095
---

  * ISEARCH-4522 фикс опечатки в факторе
  * ISEARCH-4533 правильно обрабатываем пуши о создании очереди

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-20 17:45:46

0.1094
---

  * ISEARCH-4533 обрабатываем пуши очередей стартрека
  * ISEARCH-4533 обрабатываем пуши очередей стартрека
  * ISEARCH-4527 сообщения об ошибках в новом саджесте
  * ISEARCH-4527 подставляем параметры для запроса факторов в саджест в админке
  * ISEARCH-4522 саджест групп стафф
  * ISEARCH-4522 факторы в саджест по группам стафф
  * ISEARCH-4539 принимаем пуши от idm

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-19 11:43:00

0.1093
---

  * ISEARCH-4507 переносим idm в intrasearch-suggest

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-15 11:50:50

0.1092
---

  * ISEARCH-4537 увеличиваем количество воркеров апи

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-14 14:23:34

0.1091
---

  * ISEARCH-4474 чиним подсчет ссылок в yt

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-13 19:16:56

0.1090
---

  * iSEARCH-4507 фикс idm.sources

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-12 13:52:45

0.1089
---

  * UNRELEASED

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-12 13:42:14

0.1088
---

  * ISEARCH-4507 индексатор idm.rolenodes
  * ISEARCH-4507 индексация idm.users
  * ISEARCH-4507 индексация idm.groups
  * ISEARCH-4507 саджест по мета поиску
  * ISEARCH-4507 факторы в саджесты для idm
  * ISEARCH-4507 добавляем данные для людей и групп
  * ISEARCH-4507 правки по ревью

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-12 12:50:23

0.1087
---

  * ISEARCH-3471 убираем дублирование в рассылках

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-09 17:20:59

0.1086
---

  * ISEARCH-4474 меняем кластер на hahn, обновляем версию библиотек и заменяем экспорт на PQ
  * ISEARCH-4474 чиним джобы yt

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-06 18:48:08

0.1085
---

  * ISEARCH-4516 фикс индексатора очередей

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-05 17:17:53

0.1084
---

  * ISEARCH-4516 саджест по очередям стартрека
  * ISEARCH-4516 ранжируем очереди по принадлежности пользователю
  * ISEARCH-4516 добавляем транслитерацию и смену раскладки в саджест стартрека
  * ISEARCH-4516 acl в саджесте по очередям
  * ISEARCH-4516 добавляем транслитерацию и смену раскладки в саджест стартрека
  * ISEARCH-4516 добавляем транслитерацию и смену раскладки в саджест стартрека
  * ISEARCH-4516 лишние настройки
  * ISEARCH-4516 добавляем acl в саджест по очередям
  * ISEARCH-3471 индексация рассылок сепаратора и яндекс денег
  * ISEARCH-3471 саджест по рассылкам
  * ISEARCH-3471 сниппет рассылок
  * ISEARCH-3471 оставляем только ml рассылки в визарде
  * ISEARCH-3471 добавляем урл в ответ саджеста рассылок
  * ISEARCH-4516 добавляем транслитерацию и смену раскладки в саджест стартрека
  * ISEARCH-4519 пагинация в саджесте
  * ISEARCH-4520 errors если саас не вернул документы

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-12-05 15:06:11

0.1083
---

  * ISEARCH-4509 аккуратно конвертируем в юникод при удалении служебных символов

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-30 15:04:17

0.1082
---

  * ISEARCH-4509 исправляем миграцию по удалению спец символов в вики
  * ISEARCH-4515 избавляемся от вертикали ask
  * ISEARCH-3914 добавляем в админку indexstat от сааса
  * ISEARCH-4517 Переиндексация отдельных документов вики

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-28 12:22:56

0.1081
---

  * ISEARCH-4505 логируем отсутствие clickUrl
  * ISEARCH-4508 возможность прокидывать кастомный запрос в саджест
  * ISEARCH-4509 удаляем служебные символы в метках фасетов
  * ISEARCH-4509 добавляем миграцию по удалению спец символов в вики

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-24 10:57:29

0.1080
---

  * ISEARCH-4473 используем новую апи метрики
  * ISEARCH-4493 индексируем пакеты кондуктора
  * ISEARCH-4493 факторы для поиска по пакетам
  * ISEARCH-4493 правки по ревью
  * ISEARCH-4494 индексация воркфлоу кондуктора
  * ISEARCH-4494 добавляем комментарий в сниппет воркфлоу
  * ISEARCH-4495 индексация групп воркфлоу кондуктора

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-16 17:55:29

0.1079
---

  * ISEARCH-4490 правильно исправляем click\_url пришеший от сааса

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-15 13:15:15

0.1078
---

  * ISEARCH-4498 gta=clickUrl при запросе к саасу

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-14 14:12:02

0.1077
---

  * ISEARCH-4453 фикс 500 при запросе abovemeta без пользователя
  * ISEARCH-4453 тест на валидацию формы при запросе abovemeta
  * ISEARCH-4479 тесты и рефакторинг апи приема пушей
  * ISEARCH-4479 правильный запуск тестов апишек
  * ISEARCH-4492 чиним графики в админке
  * ISEARCH-4490 добавляем clickUrl2 даже если не пришел урл от сааса

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-10 18:34:13

0.1076
---

  * ISEARCH-4457 рефакторинг апишек фич и ревизий
  * ISEARCH-4457 рефкторинг апи формул
  * ISEARCH-4457 тесты на апи фасетов
  * ISEARCH-4457 тесты на апи групповых атрибутов
  * ISEARCH-4457 тесты на апи правил колдунщика
  * ISEARCH-4457 убираем фильтрацию групповых атрибутов по id
  * ISEARCH-4457 тест на комбинацию ревизий из фич и базы
  * ISEARCH-4458 использование revision\_id при получении фасетов и группировочных атрибутов
  * ISEARCH-4470 обрезаем длинные описания в сниппетах в поиске по стартреку
  * ISEARCH-4470 не обрезаем слова при обрезке длинного описания в вики
  * ISEARCH-4468 не подсвечиваем уточняющую часть запроса
  * ISEARCH-4459 удаляем не нужные фасеты и ревизии

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-11-07 16:01:35

0.1075
---

  * ISEARCH-3826 - добавляем в админку саджеста ссылки на запросы
  * ISEARCH-3826 - дополнительные параметры при просмотре саджеста в админке
  * ISEARCH-4410 прибираемся в тестах
  * ISEARCH-4451 убираем лишнее из пассажей кондуктора

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-31 14:54:49

0.1074
---

  * ISEARCH-4390 улучшаем админку формул
  * ISEARCH-4390 не падаем при любой ошибке от сааса
  * ISEARCH-4154 поиск по 'о себе' среди неуволенных сотрудников
  * ISEARCH-4351 улучшаем саджест по номеру машины

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-26 17:27:30

0.1073
---

  * ISEARCH-4430 избавляемся от swarm флага в индексаторах
  * ISEARCH-4430 переносим sources.swarm в sources
  * ISEARCH-4430 понятное сообщение об ошибке в индексаторе
  * ISEARCH-4436 разбиваем фамилию на слова для саджеста по людям

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-24 15:48:21

0.1072
---

  * ISEARCH-4429 описание сниппета проектов планнера

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-20 14:03:34

0.1071
---

  * ISEARCH-4429 правильно сериализуем body для индексатора swarm

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-20 11:55:54

0.1070
---

  * ISEARCH-4145 учитываем строковые группировочные атрибуты
  * ISEARCH-4429 переписываем индексатор plan на swarm

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-19 18:23:39

0.1069
---

  * ISEARCH-4424 хлебные крошки для хостов в поиске по кондуктору
  * ISEARCH-4145 добавляем информацию о группах в выдачу апи

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-18 14:09:18

0.1068
---

  * ISEARCH-4412 убираем None из пассажей кондуктора
  * ISEARCH-4362 переписываем индексатор переговорок на swarm
  * ISEARCH-4363 переписываем индексацию оборудования на swarm
  * ISEARCH-4364 переписываем индексатор сервисов на swarm

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-12 16:57:45

0.1067
---

  * ISEARCH-4408: Отключить поход за группами для commitssearch

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-10-11 12:48:20

0.1066
---

  * ISEARCH-4339 миграция wiki\_new
  * ISEARCH-4399 правильно обрабатываем удалённые вики-страницы
  * ISEARCH-4399 избавляемся от регулярок при получении удаленного урла
  * ISEARCH-4403 переводим индекс wiki.en на новую апишку вики

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-10 17:25:53

0.1065
---

  * ISEARCH-4356 убраны персоны из сниппетов
  * ISEARCH-4356 breadcrumbs в сниппетах
  * ISEARCH-4404 добавляем сортировку по дате обновления

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-10 17:07:25

0.1064
---

  * ISEARCH-4100 стрипаем пробелы в ключах
  * ISEARCH-4400 фикс xss в админке поиска
  * ISEARCH-4398 добавляем дополнительные стадии поиска в настройки

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-07 15:02:27

0.1063
---

  * ISEARCH-4393 добавлен стат фактор isWikiDoc в мета поиск
  * ISEARCH-4359 добавляем фактор по письмам
  * ISEARCH-4338 поиск по тексту письма из комментов в стартреке

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-04 18:23:50

0.1062
---

  * ISEARCH-4357 фикс настроек фасетов кондуктора
  * ISEARCH-4395 проверка пермишшенов на поиск по кондуктору

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-10-03 17:02:01

0.1061
---

 * [Taisiya Malikova](https://staff.yandex-team.ru/Taisiya%20Malikova)

  * ISEARCH-4358 начало поиска по кондкутору
  * ISEARCH-4358 индексатор проектов
  * ISEARCH-4375 индексатор хостов
  * ISEARCH-4375 добавляем сниппет проектов
  * ISEARCH-4376 индексатор групп
  * ISEARCH-4376 change default names
  * ISEARCH-4356 добавляем стат факторы
  * ISEARCH-4356 правки по ревью
  * ISEARCH-4357 фасеты для поиска по кондуктору
  * ISEARCH-4357 меняем токен на правильный

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4383: Исправить логику выбора мета-факторов
  * ISEARCH-4358: Собственный SaaS-сервис у кондуктора
  * ISEARCH-4359: Факторы для поиска по кондуктору - настройки
  * ISEARCH-4352: Костыль для формул в метапоисках

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-09-30 18:13:26

0.1060
---

  * ISEARCH-4389: accounts в стафф-апи есть не всегда - 2

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-09-29 10:35:03

0.1059
---

  * ISEARCH-4389: accounts в стафф-апи есть не всегда

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-09-28 17:06:58

0.1058
---

 * [Taisiya Malikova](https://staff.yandex-team.ru/Taisiya%20Malikova)

  * ISEARCH-3534 фильтруем индексацию персон при заданных keys
  * ISEARCH-4257: Странный статус 0 в целях
  * ISEARCH-3919 дергаем st-api по ключу тикета при пушах
  * ISEARCH-3738 добавляем поиск по кандидату в очередь JOB

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4365: Не делать лишних запросов в staff-api

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-09-28 11:23:11

0.1057
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4318: Новое апи саджеста
  * ISEARCH-4317: Выключить регулярную индексацию вики старым индексатором

 * [Taisiya Malikova](https://staff.yandex-team.ru/Taisiya%20Malikova)

  * ISEARCH-4153 переходим на использование accounts вместо contacts
  * ISEARCH-4241 добавляем в версии номеров форму с разделением по границам цифр и букв

 [Taisiya Malikova](https://staff.yandex-team.ru/tmalikova@yandex-team.ru) 2016-09-22 16:16:04

0.1056
---

 * [tmalikova](https://staff.yandex-team.ru/tmalikova)

  * ISEARCH-4233: Добавить в саджест людей поиск по номеру машины и номеру мобильного телефона

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4341: Фейлы в пушах коммитов

 * [Taisiia Malikova](https://staff.yandex-team.ru/Taisiia%20Malikova)


 [Taisiia Malikova](https://staff.yandex-team.ru/tmalikova@search02.dev.yandex-team.ru) 2016-09-20 16:03:37

0.1055
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Чаще индексировать документацию
  * Показывать английские сниппеты
  * Доступ tmalikova в админку

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Информация о сборке и запуске проекта в readme

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-09-19 16:41:47

0.1054
---

  * Фикс настроек индексации внешней документации
  * Удален старый индексатор рассылок
  * Revert "ISEARCH-4226: Логирование в индексаторе документации"
  * Менять индекс вики на new\_wiki для метапоиска тоже

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-25 15:52:25

0.1053
---

  * ISEARCH-4264: Сломалась индексация invite
  * ISEARCH-4310: Сломалась индексация описаний рассылок
  * ISEARCH-4310: Перевела индексацию mldescription на swarm
  * ISEARCH-4226: Индексация документации в проде

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-25 12:23:12

0.1052
---

  * ISEARCH-4264: Сломалась индексация invite
  * ISEARCH-4226: Логирование в индексаторе документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-23 15:29:01

0.1051
---

  * ISEARCH-4296: Хайлайтер подсечивает нули и логины в коммит-мессаджах и ссылках в поиске по коммитам
  * ISEARCH-4307: Запросы в поиск по коммитам с двойным pruncount
  * ISEARCH-4306: Не работает удаление kps в админке

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-18 16:11:02

0.1050
---

  * Подняла версию django-yauth
  * SEARCH-4226: Ходить в документацию с OAuth токеном
  * Revert "ISEARCH-4301: Временно отключить новый индексатор вики"
  * ISEARCH-4305: Понизить приоритет для пушей из догмы

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-17 14:12:57

0.1049
---

  * ISEARCH-4240: фикс определения ветки в индексаторе коммитов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-16 12:18:07

0.1048
---

  * ISEARCH-4240: Фикс создания коммита в пуше
  * ISEARCH-4301: Временно отключить новый индексатор вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-16 11:28:00

0.1047
---

  * ISEARCH-4240: Коммиты в пушах приходят пачками

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-15 19:45:24

0.1046
---

  * ISEARCH-4261: Убрала фасеты из поиска по коммитам
  * version 0.1045
  * ISEARCH-4261: фикс добавления поискового атрибута

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-12 14:24:22

0.1045
---

  * ISEARCH-4279: Добавить больше данных про коммит в сниппет
  * ISEARCH-4261: 40к документов для прунинга в поиске по коммитам
  * ISEARCH-4290: Некорректные ссылки из поиска
  * ISEARCH-4261: Убрала фасеты из поиска по коммитам

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-12 13:09:20

0.1044
---

  * ISEARCH-4287: Не работают пуши в этушке
  * ISEARCH-4284: Обновить pytz

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-08-10 13:51:09

0.1043
---

  * Фикс работы с временем коммита

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-08-02 21:39:59

0.1042
---

  * ISEARCH-4258: В догму прилетает дата в формате который не парсится
  * ISEARCH-4217: Поиск по номеру тикета / ключи очереди из коммит-мессаджей
  * ISEARCH-4243: Добавить группировку по идентификатору/хэшу коммита
  * ISEARCH-4260: Увеличить число документов в выдаче поиска коммитов до 100

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-08-02 17:40:35

0.1041
---

  * ISEARCH-4252: Сниппет для вики
  * ISEARCH-4259: Этушка 500 на create
  * Revert "ISEARCH-4207: Добавить индексацию догмы по расписанию"

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-29 14:39:38

0.1040
---

  * ISEARCH-4252: Фикс request\_builder

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-26 16:12:15

0.1039
---

  * ISEARCH-4252: Индексировать вики через оба апи
  * ISEARCH-4252: Фича для использования нового индексатора вики
  * ISEARCH-4251: Регулярная переиндексация для нового апи вики
  * ISEARCH-4250: Скрыть поиск по коду
  * ISEARCH-4207: Добавить индексацию догмы по расписанию

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-26 15:31:04

0.1038
---

  * ISEARCH-4240: Ручка для пуша коммитов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-25 17:42:57

0.1037
---

  * Фикс настроек индексатора вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-25 16:35:23

0.1036
---

  * ISEARCH-4235: label фасета по продукту для внешней документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-25 14:53:27

0.1035
---

  * Убрала поход за фичами для саджеста

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-25 13:29:14

0.1034
---

  * ISEARCH-4235: Проиндексировать qloud docs
  * Включить всем навигационный саджест

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-25 12:43:47

0.1033
---

  * Доступ к админке для chapson и nadyaka
  * 3 результата в выдаче саджеста сервисов
  * Добавить логирование при запросе страниц через isearch.utils.http

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-20 16:21:49

0.1032
---

  * Правка сниппета вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-15 18:10:25

0.1031
---

  * ISEARCH-3704: peoplesearch: не работает звонок на мобильный
  * ISEARCH-4162: Перейти на новое API вики
  * ISEARCH-4141: Передавать признак "Документация" у вики-документов в xml
  * ISEARCH-4144: wikisearch: Добавить фасет "Документация"
  * ISEARCH-4162: Правка сниппета вики (выкинула не нужные верстке поля)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-15 16:23:11

0.1030
---

  * Проверять является ли фасет строкой

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-13 13:02:49

0.1029
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4125: 500 на беке если несуществующая вертикаль

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Revert "Ходим в staff-api в продакшене на localhost"
  * Приводим фасет is\_merge к строке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-13 09:49:17

0.1028
---

  * Фикс сниппета для сервисного саджеста

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-08 14:32:16

0.1027
---

  * Фикс сборки результатов поиска

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-08 13:14:52

0.1026
---

  * Фикс запроса за саджестом из админки
  * ISEARCH-4228: Добавить регулярную индексацию для саджеста по навигационным ссылкам

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-08 10:48:57

0.1025
---

  * Не сохранять длинные атрибуты
  * Саджест по сервисам
  * Фикс формирования настроек для поиска
  * Добавила фичу про навигационный саджест
  * Показывать информацию про саджестовый запрос в админке
  * Возможность ходить за группами из саджеста
  * Фикс импорта модуля индексации при запуске
  * Учитывать пробелы во всех саджестах
  * Поддержать параметр s[] для саджеста
  * Привела в порядок сниппет саджеста по сервисам

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-07-07 19:09:39

0.1024
---

  * Отключаем глобальный debug в над-мета-поиске

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-07-04 17:19:43

0.1023
---

  * Фикс настроек

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-29 13:35:15

0.1022
---

  * Другая обработка ошибок в надметапоиске

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-27 17:28:08

0.1021
---

  * ISEARCH-4222: Починить трейсбэки таймаутов
  * Фикс opensearch dressing

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-27 14:31:17

0.1020
---

  * Ходим в staff-api в продакшене на localhost

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-24 14:08:54

0.1019
---

  * Вернула headers в ping

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-09 16:15:54

0.1018
---

  * Фикс саджеста

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-09 15:37:10

0.1017
---

  * ISEARCH-4198: Документы с 404 на поиске документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-09 14:29:45

0.1016
---

  * Фикс пинга
  * Релевантность и факторы в просмотре поисков в админке
  * ISEARCH-4174: group\_attrs не всегда есть в search
  * ISEARCH-4194: Обрабатывать 500 от SaaS
  * ISEARCH-4074: Проверять признак архивности по мета-тегу
  * ISEARCH-4198: Документы с 404 на поиске документации
  * ISEARCH-4197: Даты в документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-09 11:56:11

0.1015.2
---

  * Фикс указания коллекции поиска коммитов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-03 22:13:53

0.1015.1
---

  * Фикс правила для поиска коммитов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-03 21:53:22

0.1015
---

  * Вернул потерянный колдунщик для поиска по коммитам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-06-03 21:26:11

0.1014
---

  * ISEARCH-4172: Удалить старый надметапоиск
  * Убрала просмотр визарда из админки
  * ISEARCH-4184: В админке сломался просмотр поисков

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-03 15:12:32

0.1013
---

  * ISEARCH-4074: Проверять признак архивности по мета-тегу
  * Revert "ISEARCH-4074: Проверять признак архивности по мета-тегу"
  * ISEARCH-4188: Перейти на хост staff-api в надметапоиске

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-06-02 15:03:49

0.1012
---

  * Фикс ошибки парсинга query для саджеста

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-24 17:33:19

0.1011
---

  * ISEARCH-4177: Перейти на хост wiki-api
  * ISEARCH-4179: Перейти на новый саджест

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-24 13:32:41

0.1010
---

  * ISEARCH-4173: Ревизии и фичи не умеют post-запросы

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-19 11:03:30

0.1009
---

  * Сохранять запрос при ошибке
  * Если нет поисков - это ошибка
  * ISEARCH-4156: Поиски для en, ru

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-18 16:19:44

0.1008
---

  * ISEARCH-4156: Ошибка в parallel step

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-18 15:21:03

0.1007
---

  * Фикс парсинга запроса
  * ISEARCH-4156: Ошибка в parallel step

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-18 11:07:38

0.1006
---

  * Фикс обхода индексов в админке

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-17 11:34:30

0.1005
---

  * ISEARCH-4098: Распилить SearchStep
  * Использовать коллекции, а не index
  * SEARCH-3966: Обработка запроса для саджеста
  * Включить саджест на kameta на команду поиска
  * Сохранять порядок сниппетов
  * OpenSearch в kameta
  * Фикс обхода сниппетов в саджесте
  * Фиксы выбора каметного саджеста
  * ISEARCH-4165: Правильно определять имя формулы для мета-поисков и саджеста

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-16 18:20:00

0.1004
---

  * ISEARCH-4157: Ошибка parse\_query в search степе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-11 13:24:55

0.1003
---

  * Фикс сохранения ошибки в степе ревизий
  * ISEARCH-4108: Подсветка не всегда срабатывает
  * ISEARCH-4132: searchlog

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-10 11:41:29

0.1002
---

  * ISEARCH-4136: Время ответа kameta (ISEARCH-4111: Пустые фасеты в стартреке)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-05 15:38:26

0.1001
---

  * Добавила в backends 599-ки
  * ISEARCH-4134: kameta stsearch нет блока snippet в документе в xml
  * ISEARCH-4131: Очереди стартрека

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-05-04 19:15:20

0.1000
---

  * Доступ в админку для annvas
  * Не падать если нет search\_results
  * ISEARCH-4138: Изменить урл тестинга апи этушки и протестировать
  * Даже при ошибке пытаться нарисовать xml в kameta
  * Фикс правила колдунщика для клубов в камете
  * ISEARCH-4113: Ошибка обработки сниппетов (в логах)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-04-21 17:18:52

0.999
---

  * ISEARCH-4111: Если нет label для фасета, использовать value
  * ISEARCH-4116: Сломалась индексация людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-04-19 11:51:06

0.998
---

  * ISEARCH-4112: 500 на пустой запрос
  * ISEARCH-4110: Камета за фичей
  * debug в state всегда есть
  * Более правильная проверка зоны при подсчете количества документов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-04-18 10:19:02

0.997
---

  * Удалила лишний параметр в set\_error
  * ISEARCH-4104: Длинные запросы в апи поиска отправлять через post
  * ISEARCH-4107: Подвинуть selected в сортировках
  * ISEARCH-4103: Нет selected во view
  * ISEARCH-4103: фикс обхода views
  * ISEARCH-4106: В случае пустого запроса никуда не ходить
  * Фикс выбора сервисного фасета при группировке по сервисам
  * Обработка ошибок в старом визарде
  * Вернула фиксы старых правил визарда
  * Перенесла фиксы весов колдунщиков в kameta
  * ISEARCH-4109: Нет второго колдунщика

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-04-13 17:20:07

0.996
---

  * Фикс импорта в state

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-04-11 11:40:09

0.995
---

  * Новый надметапоиск
  * Переименования
  * Правильно считать длительность ответа
  * Фиксы сборки результатов
  * Выбранный фасет
  * Правильная инициализация фасета из параметров запроса
  * ISEARCH-4089: Сортировка фасетов
  * Обработка ошибок в kameta

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-04-08 16:50:07

0.994
---

  * Забытый импорт сниппета коммита

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-04-07 19:41:28

0.993
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4094: Поменять путь до индексных файлов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Апдейт индексатора коммитов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-04-06 21:12:41

0.992
---

  * Поиск по коммитам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-22 16:13:15

0.991
---

  * ISEARCH-4079: Сделать настройку no check для индексаций
  * ISEARCH-4084: Не работает колдунщик сервисов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-03-22 15:41:46

0.990
---

  * Фикс load\_conf для стартрека (меньше фетчей и волков)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-03-17 14:17:41

0.989
---

  * ISEARCH-4004: Настроить правила для колдунщика этушки
  * ISEARCH-4072: Веса колдунщиков сервиса и проектов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-03-16 16:54:21

0.988
---

  * Ходим в СТ по http

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-15 14:59:47

0.987
---

  * Celery версии 3.1.23
  * Рестартим celery каждые два часа

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-14 00:07:22

0.986
---

  * Динамически формируем список очередей
  * Апдейт индексатора СТ и зависимость от своего startrek\_client
  * Revert "Убрал рестарт celery"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-03 04:26:53

0.985
---

  * Явно указываем app для глобальных очередей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-02 15:29:53

0.984
---

  * Использование replace\_one вместо update
  * Ланиво соединяемся с монгой
  * Подавляем ворнинги в kombu

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-01 15:49:04

0.983.1
---

  * Фикс соединения с монгой

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-01 03:03:37

0.983
---

  * ISEARCH-3979: соединение к монги с аутентифкацией
  * Убрал рестарт celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-03-01 02:36:11

0.982.1
---

  * Фикс вызова find\_one

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-24 09:46:41

0.982
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4058: убрать real-url из reindex

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Апдейт celery и новый pymongo

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-23 22:21:17

0.981
---

  * ISEARCH-4058: Выпилить real url
  * Добавила сортировку ревизий в админку

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-02-18 17:27:18

0.980
---

  * Лишнее логирование в индексаторе вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-02-15 12:05:46

0.979
---

  * ISEARCH-4048: Фикс хождения в метрику

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-02-15 11:22:05

0.978
---

  * ISEARCH-4048: wiki: Ошибка в индексации вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-02-10 14:28:33

0.977
---

  * ISEARCH-3988: Включить регулярную переиндексацию людей раз в 15 минут
  * Переиндексация джаббера

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-02-02 16:52:13

0.976
---

  * Вернул ISEARCH\_LOCAL\_QUEUE\_TMPLT

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-01-28 11:53:32

0.975
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4019: Группировочным атрибутам прокидывать имя атрибута

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-4016: Перенести статистов в редис
  * ISEARCH-3879: Сделать init скрипт для запуска редисов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2016-01-27 19:03:13

0.974
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс саджеста (не падать если нет телефонов)

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * правки по мелочи
  * ISEARCH-4010: Обернуть в лок переключение приложения celery

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-22 14:59:18

0.973
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс сообщения для условно-успешной индексации

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Блее быстрый setup в джаббере

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-20 19:18:50

0.972
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Передвинул рестарт

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-4003: Некоторые индексации продолжают стелятся
  * Убрать подробный логгинг статистов
  * Добавить логирование для сетапа вики

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-20 14:32:35

0.971
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Начинать индексацию вики после рестарта селери

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-4002: Не работает стадия  cleanup

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-19 13:18:56

0.970
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix updated

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-15 18:50:19

0.969
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Увеличил количество воркеров у дефолтной очереди
  * add TODO

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Еще один фикс логирования

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2016-01-15 18:21:45

0.968
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Revert "Локальные таски ставить в локальный редис"

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-15 17:15:43

0.967
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Дополнительно логирование для статистов
  * Выключить переиндексацию джаббера
  * Fix logging for state stats

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Локальные таски ставить в локальный редис

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-15 16:13:21

0.966
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не верно считались дельты

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-14 20:44:10

0.965
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Перенес проверку устаревшей статистики в самое начало do\_check

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-13 17:51:41

0.964
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падаем в is\_statistics\_outdated если еще ни один статист не отработал

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-13 16:51:54

0.963
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Чиню сборку на ci

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-13 15:44:39

0.962
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix intformat
  * Настройки нагрузки для ячана
  * fix отпускания лока при завершении индексации
  * Галочка "Отключить реалтайм" поумолчанию включена
  * Уменьшил количество волков для стартрека
  * fix итерирования по списку
  * ISEARCH-3955: не работает автоматический фейл зависших индексаций

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2016-01-13 14:51:31

0.961
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix gunicorn

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-21 16:39:13

0.960
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновляем gunicorn
  * Опитимизация индексации дельты

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-21 15:57:24

0.959
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падать волкам джаббера при редиректах на блекбокс
  * Регулярная переиндексация джаббера
  * Добавил сортировку по дате

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-17 17:23:54

0.958
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Revert "ISEARCH-3876: Сохранение фасетов и группировок через replace"
  * Заворачиваем \_flush в транзакцию

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-17 15:33:28

0.957
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Ретраим редиректы на паспорт
  * Убрал захардкоженный id

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-17 14:57:55

0.956
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падаем в create jabber'а
  * Красиво выводим количество дкоументов в админке
  * ISEARCH-3881: Поправить логи в админке
  * ISEARCH-3876: Сохранение фасетов и группировок через replace

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-16 22:35:38

0.955
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падаем в джббере в фетче когда нет больше разговоров
  * Не используем глобальный стек в env.py
  * не падаем при пустом body в джаббере
  * fix title сниппета в джаббере

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-15 18:26:15

0.954
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3918: Удалить \_new\_suggest из поиска
  * Не посылать пустой product в документации

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Буферизация фасетов через очередь в редисе
  * Изменения в сниппете джаббера
  * Индексация дельты в джаббере

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-14 16:07:09

0.953
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Доудалил пинговалку

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-09 18:07:00

0.952
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3935: Проверить группировочные атрибуты у лего

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * выпилил пинговалку
  * Исправляем рестарты в кроне
  * Не давать создавать пустые группировочные атрибуты
  * не создавать пустые группировочные атрибуты в документации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-09 17:31:07

0.951
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * забыл отладку

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-08 16:32:02

0.950
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавляем url в группировочный атрибут
  * Всегда добавляем name, id, value в ноду categ

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-08 16:30:29

0.949
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix индексации документации
  * Всетаки ловим ConnectionError

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-07 17:01:12

0.948
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Переименование
  * Больше воркеров для бога воркеров
  * Не подновляем индекс индексаций в конструкторе
  * Убрал из админки галочку swarm индексация

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3921: Потерялись статические факторы в поиске людей
  * Фикс индексации статистики

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-07 16:13:31

0.947
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Используем настоящий урл в saas по дефолту

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Правильный ответ нового саджеста

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-03 17:02:02

0.946
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Игнорируем ошибки если нет кеша
  * Fix dev celery settings
  * fix id'шников группировочных атрибутов и фасетов

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-03 14:58:01

0.945
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Строковые номера телефонов в саджесте

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3878: Отключить --max-tasks-per-child
  * ISEARCH-3880: Использовать unix сoкет для общения с redis
  * ISEARCH-3877: Буфферизация фасетов и группировок в redis
  * участил рестарты
  * ISEARCH-3875: Перейти на строковые группировочные атрибуты
  * ISEARCH-3906: Не сохранять пустые группировочные атрибуты
  * ISEARCH-3909: Кешировать динамические данные индексации
  * Фиксы замечаний по оптимизациям
  * Правильные хосты зукипера в деве

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-12-02 20:03:36

0.944
---

  * В саджесте департамент бывших сотрудников
  * Саджест по ручке /suggest/
  * Группировка в саджесте (забирать строго 5 результатов)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-12-02 16:27:54

0.943
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3904: Неправильный docurl на выдаче

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Пробрасывать куки из админки в запрос к саджесту

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-12-01 16:35:49

0.942
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Для саджеста определяем юзера аутентификатором
  * ISEARCH-3885: Фичи для саджеста
  * ISEARCH-3873: Переключить opensearch саджест на новый саджест

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix indexation delete

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3780: Поддержать параметр staleOk при переиндексации тикетов и комментариев в стартреке

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-12-01 15:15:00

0.941
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix cron.d

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3856: Не умеем искать в неправильной раскладке (саджест)

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Собираем один venv на все компоненты

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-11-27 09:16:32

0.940
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix cron.d

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-26 13:18:58

0.939
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * забыл зависимость от threadpool

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-25 20:05:00

0.938
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Используем тред пул для store и fetch
  * Рестартуем селери каждые три часа

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-25 18:53:08

0.937
---

  * Фикс индексатора людей (временный)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-11-23 12:16:08

0.936
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3850: Поменять настройки партиций

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-20 13:42:14

0.935
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix keys iteration
  * max\_tasks\_per\_child

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3824: Фейлится индексация людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-11-19 17:31:19

0.934
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Возможность жестко задать количество партиций для индексации
  * увеличил размер чанка ключей во время итерации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-17 21:22:36

0.933
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс путей до нового саджеста
  * Таймауты в запросах к стаффу

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Изменил метод компрессии в celery

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-17 18:13:35

0.932
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Чанками получаем и обрабатываем ключи в сборщике статистики

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-17 14:46:59

0.931
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix создания индексации из админки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-16 18:10:35

0.930
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix дебианизации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-16 16:42:10

0.929
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Прототип саджеста

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Потюнил стейдж статистику
  * Отдельный редис под статистику

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-16 15:31:46

0.928
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил kbakba доступ в админку

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-11 16:28:59

0.927
---

  * ISEARCH-3786: Поменять хост для документов вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-11-11 09:55:38

0.926
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * увеличил пул конектов
  * Поменял урлы для веб версии истории джаббера

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3799: legosearch: Битые данные в выдаче

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-10 14:55:23

0.925
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Пишем в логи когда запустился pm statistician

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-09 14:42:15

0.924
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix ask snippet
  * Переделал индексатор jabber'а

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-05 18:37:37

0.923
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix jabber indexer
  * reraise в истории джаббера
  * Индексируем только неуволенных

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-03 14:28:45

0.922
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Единый коннект к редису

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-02 16:53:43

0.921
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix grafana url
  * fix celery tasks conf

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-11-02 15:27:29

0.920
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3595: Сделать порт баз mysql опциональным
  * ISEARCH-3797: Подчищать статусы зафейленых индексаций

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-30 19:30:53

0.919
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3789: Настроить статистов
  * ISEARCH-3788: Изменить вес колдунщика этушки
  * Удалить фичу про колдунщик стартрека
  * Удалила фичу для abcsearch

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3794: Удалять старые пуши из редиса

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-27 17:59:27

0.918
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Забытая отладка

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3776: Создаются лишнии записи в таблице IndexationStats

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-10-16 13:01:05

0.917
---

  * ISEARCH-3763: Фикс работы с кодировкой

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-10-08 15:54:49

0.916
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Потюнил приоритеты статиста

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-08 12:54:17

0.915
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не ходим лишний раз за несуществующими логинами

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3763: Проиндексировать clickhouse
  * Фикс регулярной переиндексации внешней документации

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-07 18:54:40

0.914
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix настроек хоста jabber history
  * забыл show=False для джаббера

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-06 19:08:57

0.913
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3596: страницы-редиректы в выдаче

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Изменил путь до графита
  * ISEARCH-3708: Индексация истории джаббера

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-06 17:29:46

0.912
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3746: Разобраться департаментами в goals

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix поиска по коду
  * ISEARCH-3730: Факторы по итогам сбора статистики

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-02 17:58:42

0.911
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix админки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-10-01 17:57:59

0.910
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Revert "ISEARCH-3744: Написать raw sql для апдейта группировочных атрибутов и фасетов"

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-30 17:24:39

0.909
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Изменил схуме clck урла
  * визард этушки за фичей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-30 15:27:07

0.908
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3744: Написать raw sql для апдейта группировочных атрибутов и фасетов
  * Колдунщик этушки, уменьшил количество результатов в выдаче

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-29 19:43:19

0.907
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3751: Правила для колдунщика по этушке
  * fix темплейта админки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-29 18:10:12

0.906
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Выводим дату последнего статиста
  * fix get\_clicks
  * Вывод метрик в админке

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3756: В вики индексируется только 200 документов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-09-28 13:33:49

0.905
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix tasks

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-24 17:10:36

0.904
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix tasks

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-24 16:18:33

0.903
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix ZeroDivision

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-23 17:50:59

0.902
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Получение профиля по id
  * ISEARCH-3739: Вернуть отправку кликов в Saas в верстку
  * ISEARCH-3745: Перестала работать индексация wiki
  * ISEARCH-3729: Метрики по полученным данным
  * ISEARCH-3747: Пропушить данные из базы в графит

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-23 16:43:42

0.901
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не прописывать scopes во всяких формах
  * fix yachan snippet
  * Не возвращаем пустую страницу метапоиском
  * fix clicks proxy

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Дата в дефолтном сниппете (на примере стади)

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-16 14:03:10

0.900
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * real\_url для сервисов в регулярной индексации
  * Регулярная переиндексация стади

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Расширенный роботный индексатор
  * yachan

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-07 18:18:02

0.899
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * https в стади

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3724: Не разинкоживается кликурл
  * ISEARCH-3725: Сделать фильтр сессий "только с нотификацией"

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-09-03 18:08:08

0.898
---

  * Фикс search триггера
  * Игнорировать пустые поля в сниппете стади
  * Фикс SearchTrigger - в саас только get-запросы

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-09-02 14:45:13

0.897
---

  * Брать для abcsearch формулу abc

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-31 17:15:09

0.896
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс кодирования урлов для кликов
  * fix админки
  * Добавил отладки кликов

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3703: Добавить вертикаль поиска сервисов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-31 15:24:46

0.895
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Новый тестинг документации в настройках
  * Фиксы индексатора стади

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3715: Не отправлять в оранж сообщения без кликов
  * fix ответа оранджу
  * Фикс логирования кликов

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-27 16:45:21

0.894
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3714: Собирать клики для оценки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-26 15:54:27

0.893
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Ограничение доступа до админки

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс хоста стади
  * ISEARCH-3702: Добавить статус к заголовку цели

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-26 10:04:46

0.892
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3699: Отдавать в scopes атрибут show
  * ISEARCH-3699: Отдавать в scopes атрибут hidden для скрытых вертикалей
  * 30 документов на странице для фемиды
  * Принимаем пуши из фемиды
  * fix hidden scope

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-19 16:36:43

0.891
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix'ы оранджа
  * Админка: просмотр сессий
  * ISEARCH-3689: В оранж приходят сообщения о старых запросах
  * Не пишем ворнинги при неудачной попытке взять лок
  * Документация всегда по https
  * Регулярная переиндексация фемиды

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Регулярная переиндексация целей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-18 15:13:16

0.890
---

  * Фикс формирования урла для гоалс
  * Фикс запроса в колдунщике стартрека

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-14 09:53:55

0.889
---

  * Стартрек-колдунщик срабатывает на тикет/задача/таск

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-13 16:51:34

0.888
---

  * Спрятать цели за фичу
  * ISEARCH-3677: Изменить вес колдунщика стартрека

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-13 15:01:31

0.887
---

  * ISEARCH-3497: Фикс сниппета целей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-12 17:43:05

0.886
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Не падать при индексации, если в базе есть новый поиск для saas-сервиса
  * Не падать конфигурялкой если в конфигах нет источника из базы
  * ISEARCH-3497: Сделать индексатор goals

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3687: Поиск по задачам Фемиды
  * person в дефолтной выдаче
  * fix конфликтов в settings.yaml

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-12 16:10:13

0.885
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3568: Переписать индексатор study
  * ISEARCH-3568: описание сниппетов стади
  * ISEARCH-3674: Нормализовать факторы  STAT\_ask\_viewCount, STAT\_ask\_score, STAT\_ask\_answerCount
  * ISEARCH-3675: Регулярная переидексация ask

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Пофиксил проблемы с нотификациями
  * ISEARCH-3667: Сохранять в базу только опции индексации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-10 13:32:36

0.884
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix query\_id

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-06 19:04:19

0.883
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фиксы оранджа
  * Фиксы распикливания
  * Записываем query\_id для поклейки с кликами

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-06 18:18:07

0.882
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падаем при тейлинге логов
  * Починил yt
  * Джоба для парсинга таблиц с кликами

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-06 11:55:53

0.881
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Ловим UnpicklingError в индексаторе

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-08-05 16:00:16

0.880
---

  * Правильно сортировать по дате создания вопроса

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-05 12:02:47

0.879
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3660: Ограничить количество нотификаций в орандж
  * Выпилил настройки shrinked-startrek в тестинге

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3653: переименовала фичу колдунщика стартрека
  * Не подсвечивать урл в аске
  * Добавить колдунщик сервисов на вертикаль планера

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-08-04 15:43:54

0.878
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Прописал роуты новым таскам
  * Завернул в лок

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-31 20:05:02

0.877
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Нотификации через орандж

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-31 18:00:48

0.876
---

  * ISEARCH-3653: Колдунщик по стартреку
  * ISEARCH-3640: В колдунщике аска смотрим только на вопрос и на принятый ответ

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-31 14:55:35

0.875
---

  * Фикс добавления сортировки
  * ISEARCH-3640: фикс колдунщика для аска

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-29 17:10:59

0.874
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * подправил test\_celery
  * Вернул регистрацию сниппетов

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3640: Колдунщик для ask в мета-поиске

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-27 11:20:25

0.873
---

  * ISEARCH-3621: Колдунщик по ask (за фичей)
  * ISEARCH-3621: В комментариях и ответах не нужно искать по урлу
  * ISEARCH-3621: Сортировки на вертикали аска
  * ISEARCH-3637: Добавить урл и название группировки в просмотре поиска

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-24 12:53:19

0.872
---

  * Английские имена в документе аска
  * Фасеты по автору вопроса и комментария/ответа
  * Поиск по ask за фичей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-23 13:22:09

0.871
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Переделал индексатор этушки
  * Удалил неиспользуемое барахло

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Факторы в поиске по аску
  * http\_with\_retry в поиске по аску
  * Теги у комментов и ответов на вертикали аска
  * Выводить в пассажах ask только description

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-22 17:57:19

0.870
---

  * ISEARCH-3621: Классовые сниппеты в аске
  * Фиксы описания сниппетов в аске
  * Фикс импорта описаний сниппетов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-21 20:08:22

0.869
---

  * ISEARCH-3621: Поиск по ask - настройки
  * ISEARCH-3621: Поиск по ask.yandex-team.ru

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-21 18:14:27

0.868
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3627: st indexer: Ошибка в creatах
  * Лишнее логирование в индексаторе стартрека

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Выровнял таблицу sources
  * убрал оборачивание хендлера в try;except в пользу штатного механизма
  * Фикс проблемы с индексацией в одну и туже ревизию st

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-21 17:44:49

0.867
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновил кафку
  * ISEARCH-3625: wiki indexer: Ошибка в формате сниппетов
  * Ошибка в обработке последних событий из кафки

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Доп логирование в индексаторе стартрека

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-17 18:39:30

0.866
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix хайлайтера
  * Переименовал страницу с логом пушей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-16 19:26:27

0.865
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix проблем со сниппетами

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-16 16:15:54

0.864
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил выгрузку контента для этушки в kiwi
  * ISEARCH-3612: Поудалять лишние kps
  * ISEARCH-3610: Переделать завершение индексации через админку
  * Мониторинг селери очередей
  * Запускать run\_stage\_statistician с sync=True в блокирующем режиме
  * ISEARCH-3146: Статически описать сниппеты

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3603: Ошибки в индексаторе людей
  * ISEARCH-3620: Ошибки в индексаторе переговорок

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-16 14:51:41

0.863
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Лишняя запятая
  * Ограниченный event-buffer событий страртрека

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-15 19:06:54

0.862
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Fix пушей в стартрек

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-14 17:29:05

0.861
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix логгирования пушей этушки
  * fix api приема пушей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-09 18:00:51

0.860
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix индексаций пушей
  * fix индексаций пушей этушки
  * fix настроек celery-beat в девелопменте

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-09 12:40:32

0.859
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не делим пуши на партиции

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-08 20:30:05

0.858
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Изолируем все окружения кроме abovemeta

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-08 13:54:13

0.857
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Перенес зависимость от redis в isearch

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-06 20:34:50

0.856
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Перенес импорт наверх

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-06 19:28:01

0.855
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Прописал версию питона

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-07-06 17:25:19

0.854
---

  * Фикс определения real\_url

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-02 17:53:28

0.853
---

  * Фикс пути до визарда

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-02 12:43:34

0.852
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновляем зависимости yt
  * fix fabfile
  * Не запускать в девелопменте yt задачи по расписанию
  * fix пушей

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3499: Вернуть просмотр сработавших визардов в админку
  * ISEARCH-3517: Перейти на реальный урлы в индексаторе стратрека
  * ISEARCH-3517: фикс настроек индексации в пуше

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-07-01 14:22:18

0.851
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3487: Делать ретраи тасок при ошибках апи
  * Разбить celery воркеры на 4 группы
  * ISEARCH-3528: Запуск индексации с выбранной квотой
  * ISEARCH-3527: Сделать модель ноды
  * ISEARCH-3529: Запуск индексации на выбранных нодах

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-29 16:53:47

0.850
---

  * Переход на robe 1.0

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-06-24 16:00:52

0.849
---

  * ISEARCH-3587: не отображаются нажатыми кнопки группировки на вертикали стаффа

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-06-24 15:23:18

0.848
---

  * Убрать замену запроса в колдунщике людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-06-23 14:28:35

0.847
---

  * ISEARCH-3490: Убрать индексацию стади и колдунщик
  * ISEARCH-3499: Вернуть просмотр сработавших визардов в админку

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-06-23 11:46:04

0.846
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Завершаем индексацию при индексации из кеша
  * ISEARCH-3544: в колдунщике рассылок не выделяется strong'ом текст с нижним подчеркиванием

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3548: не отображается блок пейджинга
  * ISEARCH-3557: Если на первом месте нет колдунщика, то на это место надо поднять колдунщик с 5-го
  * ISEARCH-3536: Поменять хосты fml\_ops

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-06-18 11:24:53

0.845
---

  * ISEARCH-3535: Поменять запрос в админке за кол-вом документов
  * ISEARCH-3540: Присылать ссылку на переговорку

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-06-15 16:21:28

0.844
---

  * Колдунщик не ломается, если пришла только одна врезка

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-06-15 12:05:53

0.843
---

  * ISEARCH-3273: Отдавать scopes даже в случае ошибки
  * ISEARCH-3483: Реализовать логику врезок для мета-поиска
  * Правки колдунщика людей
  * Правки правил колдунщиков
  * ISEARCH-3504: В колдунщике проектов показывать первые три проекта
  * ISEARCH-3494: Не отправлять пустой виззард в xml
  * ISEARCH-3511: В колдунщике сервисов отдавать один сервис
  * ISEARCH-3499: Вернуть просмотр сработавших визардов в админку
  * Фикс индексатора сервисов (title для очередей)
  * Для search\_results всегда отдавать ответ
  * Подняла рейтинг у колдунщика, который форсится

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-06-15 09:58:25

0.842
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3467: Не индексировать витрины в beminfo

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-08 14:10:25

0.841
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3502: мета-поиск: Не подсвечивается слово из запроса
  * ISEARCH-3502: мета-поиск: Не подсвечивается слово из запроса
  * Проблемы с зависающими апдейтами статистики из базы
  * Индексируем стартрек в тестинге в правильный kps

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3467: Настройка поиска по bem.info
  * Фикс работы с формулой
  * Регулярная переиндексация лего и beminfo (раз в неделю)
  * В индексаторе сервиса пока рано менять ссылку на стартрек

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-04 19:35:24

0.840
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3377: поменять формирование урлов в индексаторе этушки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-02 19:07:47

0.839
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил в админку хосты на которых запускалась индексация
  * Изменил is\_check\_relevant

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-02 17:43:57

0.838
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил логов в таску
  * fix шаблона индексации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-02 12:42:33

0.837
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Пишем время последнего статиста

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-02 11:08:25

0.836
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3507: Админка: не отображаются свойства документа в админке
  * ISEARCH-3188: в колдунщике сервисов неправильная ссылка на этушку

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Улучшения графиков
  * Вызываем подсчет статистики перед cleanup
  * Запускаем подсчет статистики пушей только там где это нужно
  * ISEARCH-3496: Не работает переиндексация этушки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-06-01 17:14:37

0.835
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix орфографии
  * Графики выполнения стадий
  * ISEARCH-3516: Вернуть статистику по пушам

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс последней миграции
  * ISEARCH-3489: Использовать формулу как фактор

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-29 13:21:33

0.834
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix пушей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-27 11:25:32

0.833
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Забыл отладку
  * Не делить на ноль

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-26 21:34:34

0.832
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Revert "ISEARCH-3377: поменять формирование урлов в индексаторе этушки"

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-26 17:00:29

0.831
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс mldescription
  * Уменьшил пыл логгера стартрек клиента
  * Убираем ворнинги про несекурное соединение
  * ISEARCH-3481: Хранить статусы задач в локальном redis

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-26 15:43:35

0.830
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix урлов для комментариев в этушке

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-14 16:14:05

0.829
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3377: поменять формирование урлов в индексаторе этушки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-14 14:15:04

0.828
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Изменить натсройки инексации стартрека в тестинге

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-05-13 15:00:12

0.827
---

  * ISEARCH-3442: Регулярные индексации запускаются раз в день (кроме вики)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-05-06 13:46:24

0.826
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3463: слишком много запросов в st/v2/fields

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-28 15:02:27

0.825
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Индексируем только код

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-24 16:02:40

0.824
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Включить legosearch на всех

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновляем ids

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-23 18:11:35

0.823
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Изменил настройки индексации кода
  * Класть в кэш стартрека только простые типы

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-23 15:52:19

0.822
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix clear\_pushes

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3457: stsearch: один тикет дважды в результатах поиска
  * Отключаем регулярные индексации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-22 14:19:39

0.821
---

  * Отключить регулярную переиндексацию кода

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-20 16:13:43

0.820
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Факторы по метрике в лего

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix проблемы с сериализацией сессии в github3.py

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-17 17:23:08

0.819
---

  * Вешаем обработчик на сигнал task\_prerun
  * Не указываем зависимости в setup.py

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2015-04-17 10:22:46

0.818
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix ids requirements

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-16 20:08:00

0.817
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3295: Добавить название и url в группировочные атрибуты кода
  * 5000 GET!

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-16 19:54:45

0.816
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3420: В лего считать кол-во страниц выдачи по группам
  * ISEARCH-3252: Опциональный переход на url как id документа
  * Правильное название для результатов поиска для statsearch
  * ISEARCH-3252: В пушах тоже смотреть на последнюю индексацию
  * ISEARCH-3434: Не присылать сортировки и группы если ничего не найдено
  * ISEARCH-3255: Ходить в Аутентификатор для проверки пользователя
  * ISEARCH-3415: Починить KeyError в админке
  * Фактор популярности библиотеки в лего-поиске

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix фасеты в коде
  * ISEARCH-3392: yt зависимости положить в requirements.txt
  * ISEARCH-3436: сломалось параллельное исполнение мержей в yt
  * ISEARCH-3435: Брать 200 последних коммитов к файлу
  * ISEARCH-3433: Перейти на multipart в индексаторе коде
  * Индексатор репозиториев тоже body\_format=xml
  * ISEARCH-3388: Сниппеты кода должны смотреть в Догму
  * ISEARCH-3387: Перевести индексатор репозиториев на Догму
  * ISEARCH-3435: Брать 200 последних коммитов к файлу

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-16 16:04:51

0.815
---

  * ISEARCH-3391: Починить сортировку по дате обновления
  * ISEARCH-3419: Всегда отдавать в scopes тот scope, по которому актуальный поиск
  * current\_page=0 если страницы нет в запросе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-10 15:19:47

0.814
---

  * ISEARCH-3411: Присылать label="Нет" при value="none" в фасете assignee

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-09 14:29:39

0.813
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3397: Включить регулярную индексацию вики

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3411: Присылать label="Нет" при value="none" в фасете

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3395: Сломался просмотр поиска в админке
  * ISEARCH-3399: Не индексировать примеры в блоках лего

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-09 13:45:37

0.812
---

  * ISEARCH-3405: Исправить обработку формата данных в админке
  * ISEARCH-3303: Поиск не видит пост из Этушки

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-06 12:03:30

0.811
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3283: Ломаются фасеты по исполнителю/автору если в логине содержится дефис
  * Достаем отключенные правила колдунщика из админки

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3389: Перестала работать индексация wiki

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-04-03 17:03:54

0.810
---

  * ISEARCH-3394: Фикс вывода количества результатов поиска в людях

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-02 16:33:07

0.809
---

  * Показывать в тайтле блока уровень переопределения
  * SEARCH-3394: Выводить общее количество людей в scope

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-02 15:41:31

0.808
---

  * isDescription в поиске по лего

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-01 17:25:57

0.807
---

  * ISEARCH-3255: Ходить в Аутентификатор для проверки пользователя
  * ISEARCH-3366: Не присылать сортировки и группы если пустой запрос
  * ISEARCH-3314: Сделать группировку Библиотека-версия-название блока
  * ISEARCH-3380: Много 404 в индексации лего

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-04-01 16:40:54

0.806
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Прокидывать юзерагент в запросе к лего
  * Смотреть на метатеги при индексации внешней документации
  * ISEARCH-3255: Правильный Host в запросе к auth
  * ISEARCH-3363: Нормировать фактор STAT\_stat\_popularity в поиске по статистике
  * Фикс вики-индексатора (забытый метод)
  * ISEARCH-3324: Нормировать фактор STAT\_people\_wikiLinksCount в поиске по людям

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3201: ничего не находится в колдунщике клубов в вертикали этушки

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-30 15:28:53

0.805
---

  * Фикс индексатора лего
  * Не забирать текстовые файлики с github pages

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-26 14:35:29

0.804
---

  * Фикс дебиан-зависимости
  * ISEARCH-3313: Добавить фактор current

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-25 16:37:13

0.803
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3329: Поламалась индексация кода в продакшене

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3255: Ходить в Аутентификатор для проверки пользователя
  * ISEARCH-3268: Индексация документации на github pages

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-25 16:10:33

0.802
---

  * ISEARCH-3280: Добавить сортировку на выдачу по Статистике
  * ISEARCH-3288: Не подтягиваются данные в title в сниппете на Лего
  * ISEARCH-3326: Убрать фичу statsearch

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-19 14:44:35

0.801
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3296: Эскейпить текст запроса в хайлайтере
  * ISEARCH-3312: Индексация кода в тестинге и деве через Догму
  * fix получения логов из эластика

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3308: Перейти на индексацию настоящих урлов в Этушке

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-18 09:40:18

0.800
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3272: Сделать группировку для универсальной выдачи

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фиксы кода
  * ISEARCH-3298: Сломались словарные Intranet расширения
  * fix settings

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-03-13 16:07:51

0.799
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Еще зависимость для ipython

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-03-05 17:26:57

0.798
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * забытые принты
  * ISEARCH-3212: Изменить настройки индексации вики
  * ISEARCH-3215: Изменить настройки переиндексации этушки
  * ISEARCH-3283: Ломаются фасеты по исполнителю/автору если в логине содержится дефис

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3284: Проставлять selected для sorts

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-05 15:10:01

0.797
---

  * ISEARCH-3022: Причесать факторы вики / мета / документации
  * ISEARCH-3228: Добавить зонные факторы для поиска по Лего
  * ISEARCH-3022: Поменяла формулу прунинга для вики (изменились стат факторы)
  * ISEARCH-3207: Определять content и title для лего по атрибуту data-search

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-03-04 14:04:19

0.796
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Самый свежий celery и зависимости
  * Не используем compat модули для celery
  * Настраиваем логирование через явный вызов logging.config.dictConfig

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * add ipython to requirements.txt
  * ISEARCH-3212: Изменить настройки индексации вики
  * Поменял oauth\_token токен для всего

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-03-03 15:48:35

0.795
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3270: Смотреть в desc\_wiki на статистике
  * ISEARCH-3269: Добавить фасеты регионов на Статистике

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2564: Прокидывать id пользователя в SaaS

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-03-02 14:39:40

0.794
---

  * ISEARCH-3207: Подготовить lego.yandex-team.ru для индексации
  * фикс внешней документации
  * ISEARCH-3240: Добавить scope legosearch за фичу
  * Удаление старых ревизий лего
  * Фикс формулы прунинга для сервиса intrasearch (без лего)
  * ISEARCH-3228: Добавить зонные факторы для поиска по Лего
  * ISEARCH-3266: Передавать на фронтенд параметр current\_page

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-02-27 16:52:33

0.793
---

  * ISEARCH-3251: Добавить в пассаж description в Статистике
  * SEARCH-3262: Добавить фасеты на Статистике

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-02-25 16:07:49

0.792
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падать если нет бранчей
  * Скрипты для подсчета языков программирования
  * ISEARCH-3259: Не фейлится индексаци после нужного числа ретраев

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-24 15:40:04

0.791
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падать при поиске в кеше если монга сломалась
  * ISEARCH-3192: XMLSyntaxError at /search/viewer/ на запросы ШАД, ШМЯ
  * Переименовал кнопку в админке

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-19 15:43:08

0.790
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix code.py

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Уровень логирования warning для celery

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-19 14:57:30

0.789
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3224: Ошибки при индексации Статистики
  * Настройки визарда и надметапоиска в деве

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3233: в проде nothingness and code 200 при поиске из кластера вложенностью > 5
  * ISEARCH-3242: Распилить fetch на два этапа
  * ISEARCH-3227: Доделать логи в админке

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-19 14:16:56

0.788
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3215: Изменить настройки переиндексации этушки
  * ISEARCH-3237: Поддержать авторизацию в http API гитхаба
  * ISEARCH-3227: Доделать логи в админке
  * ISEARCH-3225: Сломалась индексация стаффа

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-17 18:40:49

0.787
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3212: Изменить настройки индексации вики
  * Вынес новый хайлайтер для всех
  * Визард на qtree
  * ISEARCH-3183: Переписать индексатор на http api github
  * ISEARCH-3185: Класть кеш кода в контент-систему
  * ISEARCH-3217: баг с сериализацией в коде

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-16 21:06:16

0.786
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Убрал CDATA
  * ISEARCH-3209: При индексации ошибку "Incoming document is obsolete" не считать ошибкой

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-11 15:09:52

0.785
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3205: Ограничение в 256 символов в поле "правила колдунщика"

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix xml.py
  * fix схемы для эластика

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-11 14:42:37

0.784
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Спрятал CDATA за фичу

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-10 18:23:27

0.783
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3193: Сломались юзерские факторы в поиске по стартреку

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix логов в админке в случае с индексацией без очереди
  * fix настроек эластика
  * fix do\_load
  * Не создаем do\_content таску когда индексируем из кеша

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3196: Некорректные данные в сниппете в поле content
  * ISEARCH-2709: Теряются переносы строк при индексации комментариев стартрека

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-02-10 15:10:01

0.782
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Забыл отладку

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-06 16:14:12

0.781
---

  * ISEARCH-3182 — На статистике не применяется формула

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-02-05 13:48:48

0.780
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Удалила старого робота из settings
  * ISEARCH-3158 — Переписать индексацию Статистики на swarm
  * ISEARCH-3159 — Добавить вертикаль statsearch в scopes (за фичу)
  * ISEARCH-3154 — Потеряли фактор STAT\_meta\_pageViews в индексе Вики

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3178 — Не корректно обрабатывается запрос со знаками препинания
  * ISEARCH-3122 — Логи индексаций из ES
  * ISEARCH-3180 — Вернуть CDATA
  * fix даты в админке

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-05 12:07:02

0.779
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Немного ускорил load стадию
  * ISEARCH-3123 — Журнал запуска задач на YT
  * ISEARCH-3160 — Вьювер профилей
  * Ссылки на профиль
  * ISEARCH-3164 — В сообщении опечаточника не отображаются исправленные буквы
  * fix fabfile
  * ISEARCH-3173 — 500ка на запрос [морда] в тестинге с новым хайлатером

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3155 — Подготовить данные для сниппета статистики
  * ISEARCH-3157 — Добавить зонные факторы для поиска по Статистике
  * ISEARCH-3156 — Добавить статические факторы для поиску по Статистики

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Используем env форматер для логов
  * Дополнительная настройка django.db.backends логера
  * Ленивая загрузка информации о факторах в saas сторадже
  * Апдейт выставления таймзоны в форматере логов
  * Уменьшил число воркеров для нагруженных очередей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-02-03 15:56:31

0.778
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * перенес load в swarm\_walk.conf
  * Неправильное условие записи в кэш
  * fix дефолтных тегов для хайлайтера

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3094 — Сделать в админке выпадушку для view
  * ISEARCH-3149 — 500 на вертикали людей с пустым запросом

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-29 16:59:40

0.777
---

  * Отключить индексацию вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-29 11:42:23

0.776
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3141 — 500 при запуске индексации вики из кеша
  * ISEARCH-3142 — отрефакторить функции работы с деревом запроса
  * ISEARCH-3127 — Починить удаление старых kps

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3137 — Удалить старый индексатор wiki

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-28 18:42:40

0.775
---

  * SEARCH-3121 — Асинхронные счетчики SaaS в админке
  * ISEARCH-3136 — Убрать левый сайдбар из админки

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-28 13:56:02

0.774
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Избавился от старья для запуска яндекс сервера
  * ISEARCH-3134 — Привести хайлайтинг пассажей к виду как и новые сниппеты
  * ISEARCH-3111 — справляться с ошибками синтаксиса в запросе

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-27 19:40:21

0.773
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix компиляции в строку унарных операторов
  * Настройки для тестов

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Переиндексация вики по расписанию в swarm

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-27 12:52:43

0.772
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix функции query.join
  * Расширил язык запросов #{плейсхолдером}# для визарда
  * Забыл зависимость от funcparserlib

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3103 — Файлы в индексе внешней документации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-23 15:39:42

0.771
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3117 — Не работает индексации Вики "из кэша"
  * ISEARCH-3119 — Смержить новый хайлайтер за фичей
  * fix iteration

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-22 17:24:30

0.770
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поправленный redis транспорт для celery
  * Redis сохраняет свою базу раз в 5 минут
  * Выпилил кастомный приоритет у compat индексаторов.

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-22 11:56:13

0.769
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Контекстный логгинг индексаций

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix урлов тестинга
  * Выпилил неиспользуемые триггеры
  * ISEARCH-3125 — Ходить последовательно по страницам в стартреке

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3106 — Смигрировать с параметра timebound в SaaS

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-21 16:04:49

0.768
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3106 — Смигрировать с параметра timebound в SaaS

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * В документации не менять урлы

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-20 11:11:30

0.767
---

  * Фикс просмотра поисков в админке

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-19 13:04:36

0.766
---

  * Фикс ошибки подсчета результатов в поиске по людям
  * Фикс просмотра поисков в админке
  * ISEARCH-2649 — Выводить количество статусов на странице ревизии
  * ISEARCH-3112 — Иногда ломается подсчет результатов
  * ISEARCH-3108 — Дубликаты в выдаче поиска по Вики из-за разного регистра в урле

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-16 17:52:56

0.765
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3096 — В админке не работает галочка "новая ревизия"
  * ISEARCH-3097 — Сломался bulk fail

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3100 — Поправить урл ml api

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Универсальная выдача - фасеты и view
  * ISEARCH-3032 — Доработать выдачу информации про фасеты с бекэнда
  * ISEARCH-3032 — по-другому формируется информация про фасеты
  * ISEARCH-3033 — Выдавать список вертикалей с бекэнда
  * ISEARCH-3031 — Выдавать сортировки вертикалей с бекэнда
  * ISEARCH-3059 — Добавить количество результатов в информацию про вертикали
  * ISEARCH-3034 — Выдавать информацию для паджинации с бекэнда
  * ISEARCH-3034 — функции для определения количества результатов
  * Добавить к внешней документации фактор isDoc

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-16 14:06:44

0.764
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix зависимостей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-14 17:03:13

0.763
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновление ids

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-14 14:42:00

0.762
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не сохраняем в kiwi во время dry-run
  * Переделал walk'и в индексаторе стратрека
  * fix версий libgit2-dev и libssl1.0.0
  * Починил пуш в этушку

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2015-01-14 13:29:10

0.761
---

  * ISEARCH-3019 — Добавить внешнюю документацию и архив в общий метапоиск

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2015-01-13 17:40:06

0.760
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3069 — Починить время в логах

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-18 17:04:55

0.759
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3067 — Правильные дефолты в форме в админке

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Ловим еще больше ошибок от OpenSSL
  * ISEARCH-3063 — Писать warning если нет прав на пост

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-17 18:08:10

0.758
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3066 — Внутри cdata еще раз дополнительно экспейпить
  * Мелкие фиксы

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3064 — Добавить в админку галочку --from-cache переиндексации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-17 15:33:21

0.757
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3061 — Обрабатывать ошибки от OpenSSL
  * ISEARCH-2968 — Переиндексация по данным из KiWi
  * Добавил load стадию в админку и конфиги
  * Уменьшил таймаут ожидания ответа от saas при индексации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Уровень логирования warning для redis

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-17 13:14:49

0.756
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2995 — Запакетировать свежий lxml
  * ISEARCH-2971 — Не весь текст оборачивается в CDATA
  * ISEARCH-3055 — Выбрать поля для QueueUpdated события

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-15 17:04:52

0.755
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3042 — Приглушить ошибки в add\_user
  * fix пересборки

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-15 13:16:55

0.754
---

  * ISEARCH-3056 — Ошибки celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-12 17:58:03

0.753
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3044 — Переделать экспорты из киви на новые атрибуты
  * Изменил приоритет переиндексаций пушей очередей
  * ISEARCH-2969 — Сделать команду kafkareset
  * ISEARCH-3052 — Зависшие переиндексации очередей / компонентов в стартреке
  * Не добавлять номера строк в сниппет кода

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3019 — Добавить внешнюю документацию и архив в общий метапоиск

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-12 17:42:31

0.752
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3050 — Не правильно прокидывается таймаут в requests
  * Не зажигаем error в чекалке пушей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-11 16:35:36

0.751
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обратный порядок сортировки в админке пушей
  * ISEARCH-3047 — Поломалась дата в пуше от СТ

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Свежий requests 2.5

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-10 19:56:29

0.750
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2965 — Обновить сторадж и индексаторы под новые атрибуты
  * ISEARCH-3037 — Кеширование сессий
  * ISEARCH-3045 — Придумать как десериализовывать индексаторы

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-10 18:22:00

0.749
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил в пакет конфиг проверки пушей

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-09 16:34:35

0.748
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Скрипт сборки новой версии
  * ISEARCH-2967 — Переделать FactorStorage в ProfileStorage
  * Много забытых отладчиков
  * fix fabfile

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-09 15:20:57

0.747
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Зависимость от libssl1.0.0 1.0.1-4ubuntu5.20

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-3012 — Выпилить старый индексатор Документации

 * [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/Nikita%20Zubkov%20(Hello%20World!))


 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-08 17:03:54

0.746
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3024 — Странный сниппет кода "0"
  * ISEARCH-2950 — Обрезать ведущие пробелы в коде сниппета
  * Лишние импорты
  * ISEARCH-3026 — Проблемы с сериализацией в github3.py
  * Github3.py version 1.0.0a1

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Дополнительный логгинг при падении стадии

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-08 15:30:56

0.745
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3016 — Не показываются мантайнеры репозиториев
  * fix shadow\_revision больше не делает активную ревизию ready

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-04 17:33:24

0.744
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix logging level
  * ISEARCH-2966 — Чтение из KiWi потоком
  * fix ids version

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-03 20:37:52

0.743
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поправил имена логгеров

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Переделал walk'и стартрека

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Делаем ревизию активной в транзакции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-03 18:29:10

0.742
---

  * Прописываем cleanup\_* стадии в global очереди

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-03 10:39:05

0.741
---

  * Убрал ссылку на flower
  * Отключаем gossip у celery воркеров, т.к. он не работает с pickle event сообщениями

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-02 23:17:55

0.740
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-3005 — Ошибка в индексаторе ST

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Выключаем в celery SEND\_TASK\_SENT\_EVENT

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-02 21:33:30

0.739
---

  * Выставляем ACCEPT\_CONTENT для celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-02 20:25:30

0.738
---

  * Удаляем старый конфиг swarm-local

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-02 19:15:18

0.737
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2926 — Определять дефолтный бранч и поднимать его в формуле
  * Правки по пушам стартрека
  * ISEARCH-3003 — Много дублированных коммитов
  * fix потенциальной ошибки
  * ISEARCH-3004 — Не показываются сниппеты кода

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-3002 — По дефолту использовать локальные очереди

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-12-02 18:09:10

0.736
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2973 — Определять и пессимизировать форки репозиториев
  * ISEARCH-2978 — Схлоповать репозитории форки
  * ISEARCH-2882 — Перейти на api v2 СТ
  * ISEARCH-2633 — Мониторинг пуша
  * Монран чекалки тикетов
  * Переделал чекалку пушей чтобы принимала секунды
  * ISEARCH-2985 — Выводить лог пуша в админке
  * fix fabfile

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Генерировать пассажи в документации только по контенту
  * ISEARCH-2992 — Хлебные крошки в индексе проектов
  * Лишние docsearch\_meta в админке

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-12-01 13:00:40

0.735
---

  * ISEARCH-2988 — Включаем мета-документацию всем
  * ISEARCH-2976 — Починить поиск в найденном

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-11-27 14:36:38

0.734
---

  * ISEARCH-2982 — Не переводить название продукта во внешней документации
  * ISEARCH-2983 — Обновить расписание переиндексаций Документации
  * Фактор isStartPage для внутренней документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-11-26 17:02:17

0.733
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2970 — Кривое время коммитов в поиске по коду

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Имя очереди для удаления локальных статусов как настройка
  * Строгая зависимость от версии headless

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2958 — Никого не найдено по запросу theigel@yandex-team.com
  * ISEARCH-2942 — Фасеты в поиске по Документации
  * ISEARCH-2940 — Парсинг reverbrain
  * Сборные фасеты для метапоиска
  * Правки факторов для документации
  * ISEARCH-2940 - Правильно считать статические факторы
  * Мелкие фиксы swarm-индексатора документации
  * Хлебные крошки во внешней документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-11-26 12:05:57

0.732
---

  * Хост надметапоиска по умолчанию - localhost

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-11-24 15:16:28

0.731
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix урла до этушки

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фасты по документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-11-20 17:38:39

0.730
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Зависимость ylock с правильным entry\_point
  * Использование архивов, а не чекаута из cvs в зависимостях

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2955 — Фича для новой документации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Отключаем CELERYD\_FORCE\_EXECV для локальных воркеров
  * Отключаем события в Celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-11-19 16:12:45

0.729
---

  * Отключаем direct очереди для локальных воркеров
  * У нас пока нету выделенного инстанса для cleanup очереди

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-11-18 19:10:45

0.728
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2930 — Перейти на авторизацию в этушечном индексаторе

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2931 — Поддержать нативный маркер направления у подразделения

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Отключаем переиндексацию очереди по событию из кафки

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал init скрипт intrasearch-flower из пакета
  * Убрал лишнее из /var/run

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2933 — Сделать мета-поиск для индексов Документации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не убиваем при сборке *.egg-info директории
  * Явное использование celery app
  * Свежая pytz
  * ISEARCH-2908 — Поднять redis рядом с celery воркерами
  * ISEARCH-2909 — Сделать два celery app
  * ISEARCH-2910 — Научить next ставить задачи в разные app
  * ISEARCH-2911 — Сделать мапинг стадий на app'ы

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-11-17 17:21:45

0.727
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Revert "Отключил индексацию кода по расписанию"
  * ISEARCH-2923 — слишком много зон в документах с кодом
  * ISEARCH-2920 — Включить переиндексацию индекса репозиториев в продакшне

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2889 — Индексатор RobotIndexer

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-11-07 15:56:06

0.726
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * зазэнковыживаем данные из формы
  * Отключил индексацию кода по расписанию

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-31 15:00:08

0.725
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2917 — Удалить поддержку ci, cn аргементы из бекенда поиска по вики

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-30 15:33:49

0.724
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2915 — принимать на вход так же facet.cluster=qwe/qwe

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-30 13:26:00

0.723
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Ходить в продакшене в продакшен этушки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-29 17:01:57

0.722
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2907 — Разнести fetch и create по разным воркерам
  * Отдавать фичи на фронтенд всегда.

 [Nikita Zubkov](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-28 18:51:51

0.721
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2544 — Добавить фасет по типу тикета в поиске по Стартреку
  * ISEARCH-2898 — Бекенд возвращает пустой ответ с кодом 200
  * ISEARCH-2905 — Добавить фичу codesearch\_enabled
  * fix kiwi\_export.cfg.tpl
  * ISEARCH-2892 — Добавлять фасеты очереди к файлам, если в него был хотя бы один комит с указанием данной очереди
  * ISEARCH-2893 — Придумать как группировать коммиты без файлов (лего, например)

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-27 15:39:06

0.720
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Revert "используем hiliteHTML3"
  * Поддержка пуша очереди стартрека
  * Новые репозитории для индексации
  * фича code\_enable
  * ISEARCH-2897 — показывать выбранный уровень фасета вики

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-23 14:01:58

0.719
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2863 — Стрипать правила колдунщиков

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * используем hiliteHTML3
  * ISEARCH-2874 — Разделить фасеты в поиске по Вики

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-17 15:47:23

0.718
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2833 — Удалить старый индексатор people и зависимость DIS
  * Города в документе департамента
  * ISEARCH-2709 — Теряются переносы строк при индексации комментариев стартрека

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2875 — Генерировать конфиги для экспорта из kiwi

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-16 14:06:24

0.717
---

  * Фасеты по типу на вертикали людей
  * ISEARCH-2848 — Ранжирование групп-подразделений в поиске людей
  * ISEARCH-2848 — Фасеты по направлению и городу у департаментных документов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-14 10:45:05

0.716
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2840 — Неверное количество документов по фасету в поиске по Вики
  * ISEARCH-2868 — Нормировать фактор \_modifiedAt в поиске по вики
  * Засовываем в киви пикленный объект

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-10 16:58:45

0.715
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix фикс линковых факторов в индексаторе

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-09 17:19:33

0.714
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Избавился от вики-форматтера
  * Ходить за факторами в вики, а не в людей
  * ISEARCH-2796 — Удалять документы из KiWi+YT

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-09 15:54:07

0.713
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2788 — Инкрементальная индексация кода раз в час
  * ISEARCH-2858 — Добавить расчет линковых факторов по расписанию
  * ISEARCH-2859 — Попробовать использовать pygments для выделения имён классов / функций / текстов комментариев / etc
  * убрал лишние импорты
  * Ограничение на количество отдаваемых фасетов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-09 13:30:32

0.712
---

  * ISEARCH-2813 — Убрать из поиска людей инфомацию про удалённые и закрытые сервисы
  * ISEARCH-2851 — Поиск людей по ssh key fingerprint

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-07 14:32:07

0.711
---

  * Игнорировать ворнинг для миграции
  * doc\_url ведет на htpps у людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-03 13:37:36

0.710
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2367 — Заворачивать в CDATA контент пассажей и сниппетов

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс миграции - raw sql

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-03 11:50:08

0.709
---

  * Наполнять табличку фасетов не в транзакции

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-02 16:40:00

0.708
---

  * Фикс названия ручки с фасетами

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-02 13:43:26

0.707
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс рассчета текстов ссылок вики

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-10-02 13:26:11

0.706
---

  * ISEARCH-2810 — Не показывается вхождение в некоторых полях
  * SEARCH-2602 — Сделать локализацию фасетов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-10-02 13:14:27

0.705
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix парсинга wiki\_links\_texts

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-30 17:13:12

0.704
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * В ml'е https у апи
  * ISEARCH-2819 — Подкрутить правила для срабатываня колдунщика рассылок

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-30 16:08:03

0.703
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2824 — Добавить фактор isPrWaves для поиска по Вики ISEARCH-2844 — Линковые факторы в поиске по Вики / Метапоиске

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-30 14:10:47

0.702
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2801 — Если не указан стол, то в сниппете вовсе не выводится офис сотрудника

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Новые факторы в mldescription.
  * ISEARCH-2819 — Подкрутить правила для срабатываня колдунщика рассылок
  * ISEARCH-2815 — Ошибка с контекстом
  * ISEARCH-2843 — падает фетч ромочки
  * Вытаскиваем текст линков в вики

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-30 13:31:18

0.701
---

  * ISEARCH-2829 — У сотрудников группы HR нет доступа к тикетам очереди HR в поиске

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-09-25 12:24:58

0.700
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2811 — Не показываются сниппеты кода в поиске по коду
  * Локи yt джобов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-24 17:25:26

0.699
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2791 — Подготовка к релизу поиска людей

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-24 16:01:32

0.698
---

  * Фикс переключения визарда

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-09-24 14:45:34

0.697
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2751 - новое поле в правилах внешнего колдунщика
  * ISEARCH-2751 - использовать доп параметры запроса из правил колдунщика

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2804 — В урлах KiWi сделать всегда https

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-24 14:10:51

0.696
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix имени создания файла

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-24 12:22:18

0.695
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Вместо хардлика делать копию архива с модулями для yt

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-23 21:44:23

0.694
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2785 — 500 по запросу [рассылки]
  * ISEARCH-2790 — Некорректно проставляются факторы isHead и isDeputyHead

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2798 — Переиндексация выбранных организаций и репозиториев
  * удаляем контент из вики
  * ISEARCH-2788 — Инкрементальная индексация кода
  * Правки людского джоба
  * Не падаем при походе в викиформаттер
  * ISEARCH-2794 — Запускать YT джобы по расписанию

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-23 19:45:08

0.693
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2768 — выводить название сработавшего колдунщика в админке
  * ISEARCH-2768 — добавить в админке возможность выбора группировки в интерфейсе
  * ISEARCH-2769 — в админке не скрываются результаты поиска по зонам

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Описание людского джоба
  * fix запуска джобов
  * kiwi\_merge джоб

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-22 19:28:33

0.692
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Пишем в лог при ошибках фетча
  * Фиксы в запускалке job'ов
  * ISEARCH-2775 — добавить в документ-файл информацию про коммитеров
  * ISEARCH-2629 — Слишком длинные строки у минимизированных файлов
  * fix падения фетча в индексаторе кода

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-19 18:07:11

0.691
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2770 — Плохое ранжирование групп при группировке по сервисам и выборе фасета по городу/группе
  * Поменял имя поля

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал переиндексацию статистики по расписанию

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2783 — Проверить что старый индекс людей работает

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-18 15:22:36

0.690
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Игнорируем лего и svn
  * Возмжность передавать организацию, а не только репозиторий

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-17 17:12:24

0.689
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не пытаться индексировать пустые репозитории

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-17 15:40:39

0.688
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал start/stop директивы из intrasearch-celry-instance

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Перевел все на simplejson

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-17 13:01:14

0.687
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Конетенты выполняются в одном инстансе celery со сторами

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-16 17:53:03

0.686
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2753 — при фильтрации по facet.city=none получаем 500
  * ISEARCH-2767 — Проверить и нормировать фактор STAT\_people\_pageViews в поиске людей
  * ISEARCH-2753 — Ускорение работы визарда для поиска людей
  * ISEARCH-2724 — Добавить в сниппет направление и рассылки подразделения

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2766 — Перестали использовать переколдованный текст для подсветки сниппетов
  * fix'ы в yt

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-09-16 16:58:44

0.685
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix control

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-15 15:45:16

0.684
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix запуска команд из консоли и celery

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-12 20:13:57

0.683
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Забыл убрать несуществующий пакет из control

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-12 17:48:27

0.682
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2694 — Правильно считать документы по людям
  * ISEARCH-2761 — Разное количество результатов до и после переключения группировки на выдаче
  * ISEARCH-2734 — Ничего не найдено по запросу [кукуц] в тестинге

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2557 — Перейти на новое апи стаффа для получения групп пользователя
  * Все про Yt
  * Выводим в админке информацию про стадию content

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-12 17:24:30

0.681
---

  * ISEARCH-2745 — Не правильно проставляется фактор STAT\_people\_isOutstaff
  * ISEARCH-2654 — Поменять дефолтную группировку
  * ISEARCH-2747 — Искать по короткому названию направления
  * ISEARCH-2736 — Не сработала автоматическая группировка по департаменту по запросу [зомбики]

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-09-10 14:34:56

0.680
---

  * ISEARCH-1740 — Фичи для групп
  * ISEARCH-2676 — Пробрасывать фасеты в колдунщик

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-09-09 11:53:24

0.679
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2585 — Унифицировать раскладку модулей индексации
  * Везде ходим в интраситу
  * Унифицированное имя хоста для kiwi

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2728 — Увеличить количество тикетов на одной странице выдачи поиска по стартреку до 20
  * ISEARCH-2725 — Не искать бывших по названию сервиса / ключевым словам

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-08 19:08:55

0.678
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2546 — Перенести services в источник plan
  * Включил обратно content backend
  * отключил nort для документации

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-05 14:05:24

0.677
---

  * Фикс нового индексатора людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-09-03 17:48:47

0.676
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Временно отключил сохранение в киви

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-03 16:00:10

0.675
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2702 — Включить персонализацию в СТ

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * отправлять flush документ нужно в формате
  * ISEARCH-2707 — Прокидывать параметры pron=timebound<us> и timeout с запросом в SaaS

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-09-02 14:14:22

0.674
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2636 — Не работает изменение формулы в продакшне
  * Вернул обратно DummyContentStorage
  * добавил доку к KiwiContentStorage

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2699 — Конектиться к монге один раз

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-09-01 14:44:23

0.673
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * запись документов в kiwi
  * fix таймаута в этушке
  * не ходить за сниппетами кода когда нет пассажей
  * Таймаут на получение формулы

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2677 — При группировке по сервису поднимать наиболее релевантную группу на первое место
  * Админка не падает, если данных про группировочный атрибут нет в базе
  * ISEARCH-2685 — Добавить дату рождения в сниппет людей
  * ISEARCH-2677 — Не искать в сервисных документах, если группировка не по сервису
  * ISEARCH-2682 — Потеряли поиск по описанию подразделения
  * ISEARCH-2676 — При включенном фасете по сервису + группировке по сервису показывать только одну соответствующую группу

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-08-29 10:00:53

0.672
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2662 — Убирать doc\_snippet\_ru из xml
  * "Нет направления" вместо "Нет" в фасете по направлению в людях
  * ISEARCH-2666 — Для людей без сервисов задавать пустую сервисную группу
  * ISEARCH-2340 — Поиск по модели телефона

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * DOCENGINE-534 — Сломался поиск по документации
  * add .agignore

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-08-26 14:33:43

0.671
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * забыли закрыть тег в админке
  * улучшения внешнего вида страницы search в админке
  * repo\_url
  * Отображаем группировки в админке

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-08-21 16:49:21

0.670
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2653 — Убрать origin/ из имени бранча
  * ISEARCH-2646 — Группировка коммитов без файлов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-08-20 18:50:02

0.669
---

  * Переименовать фасет по направлению в новом поиске людей
  * ISEARCH-2652 — Нет названий проектов в выдаче поиска по проектам в en интерфейсе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-08-20 17:39:49

0.668
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2650 — Поле для задания приоритета индексации
  * Переключалка статуса в админке отображается для всех ревизий
  * ISEARCH-2584 — Убрать лишние поля у индексаций

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал обработку сигнала task\_revoked из-за непонятных данных, которые стали приходить

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-20 17:21:07

0.667
---

  * Игнорируем результаты тасок

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-19 17:47:08

0.666
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2586 — Кнопка, останавливающая старые индексации
  * Фикс остановки индексации в админке
  * Фикс on\_air со страницы ревизии

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Отключаем переиндексацию в тестинге

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-19 16:48:21

0.665
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2647 — Обработка фасета по кластеру Вики
  * Вынес настройку вики фасетов в другое место
  * fix проблем с индексацие кода

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Вернул переиндексацию людей по расписанию
  * Не переиндексируем клубы ночью

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс получения пользовательских факторов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-08-19 12:41:02

0.664
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * перенес зависимости из isearch в settings
  * ISEARCH-2646 — Группировка коммитов без файлов

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  *  Фикс пользовательских факторов
  * Построение конфига по пользовательским факторам
  * При построении фасетов не парсить --sum элементы

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Использование своего celery шедулера, пока в стоковом есть бага
  * Фикс расписания задач
  * Отключаем переиндексацию людей в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-18 15:23:00

0.663
---

  * Убрал ограничение уровня логиронивая на дефолтный syslog хендлер
  * Отключаем эскейпинг у всех syslog хендлеров

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-14 22:38:26

0.662
---

  * info логи у celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-14 20:04:32

0.661
---

  * Ссылка на isearch-flower в /usr/bin

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-13 16:53:18

0.660
---

  * Явное подключение requirements.txt из settings

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-13 15:47:39

0.659
---

  * Зависимость MySQL-python 1.2.5

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-13 15:07:01

0.658
---

  * Симлинк на flower в init.d

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-13 12:58:34

0.657
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix не добавлять фасет по кластеру users

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс прокидки имени индекса в расписании celery

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix wiki фасетов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Свежие celery и kombu
  * MongoDB транспорт с ttl и доп. опциями
  * Включение событий и ttl в очереди
  * Отключение подсчета размера очереди
  * fix transport
  * Явное подключение чужих requirements.txt
  * Подключение celery flower
  * ISEARCH-2641 — Уменьшить количество групп на странице в поиске людей с группировкой по сервисам
  * Убрал очередь remove из конфига

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-13 12:55:43

0.656
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фасеты в вики
  * ISEARCH-2615 — Индексатор code на ids staff
  * ISEARCH-2614 — Индексатор at на ids staff
  * Спрятал за фичу фасеты в вики

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2631 — Для поиска со страницы очереди в стартреке перейти на ключ вместо id
  * Фикс опечатки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-08-04 19:17:16

0.655
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обязательный эскейпинг
  * удалил лишнее из snippets.py
  * Увеличил полезную площадь вьювера поиска в админке
  * Эскейпинг пассажей в админке

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Пользовательские факторы в стартреке
  * Персонализация st за фичей
  * Комментарий в надметапоиске

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-07-31 17:22:41

0.654
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс неправильного хайлайтинга кода

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-07-31 13:04:32

0.653
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Переименовала фактор для людей
  * Revert "Переименовала фактор для людей"
  * Правки в фасетах по департаментным группам на вертикали людей
  * ISEARCH-2612 — Индексатор study на ids staff
  * ISEARCH-2611 — Перевести services на ids staff
  * ISEARCH-2609 — Перевести индексатор equipment на ids\_staff
  * ISEARCH-2610 — Индексатор invite на ids staff
  * name\_dns в индексаторе оборудования

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Ссылки на бранчи

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-07-30 16:18:20

0.652
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * возвращаем несколько сниппетов кода в правильном порядке
  * уменьшил контекст до 3х строчек
  * стрип пустого в конце кода

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фасеты по департаментной группе в поиске людей
  * Расширить сниппет для поиска людей
  * Увеличить количество групп на странице для группировки по сервисам

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-07-25 11:06:52

0.651
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Ссылка на коммит в сниппете
  * Новая версия ids.
  * ISEARCH-2622 — странные сниппеты кода по запросу contrib.staticfiles

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-07-24 14:30:12

0.650
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2616 — Название пакетов в репозиториях в отдельной ноде
  * ISEARCH-2552 — Выпилить логику работы со старыми фасетами

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-07-23 13:04:40

0.649
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не добавляется префикс для css класса hll
  * Забыл добавить фасет в настройки
  * Название пакета в репозитории в отдельной ноде

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2613 — Индексатор people (swarm) на ids staff
  * Фикс swarm поиска по людям (body)

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2608 — ошибка при старте индексации
  * Фикс логирования в прокси Календаря

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)


 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-07-21 13:59:59

0.648
---

  * Фикс инициализации стораджа контента

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-07-16 14:34:55

0.647
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2554 — Двойной хайлайтинг сниппетов
  * update .gitignore
  * pygments css prefix
  * ISEARCH-2607 — Число документов в группе кода
  * fix поиска по коду (не работал через celery)

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-07-16 13:11:44

0.646
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Включил обратно переиндексацию Планера
  * Фикс опечатки

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фиксы сниппета нового индексатора людей
  * ISEARCH-2600 — Фасеты в поиске людей
  * ISEARCH-2601 — Переключение группировки людей спрятать за фичу
  * Фикс номера машины в новом индексаторе людей

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * вытащил получение классов и функций в отдельную функцию
  * не работали зонные факторы в поиске по коду
  * ISEARCH-2576 — Фактор для документов с типом code
  * ISEARCH-2590 — Разработчики в сниппете репозитория
  * ISEARCH-2591 — Последний коммит файла

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-07-15 14:11:54

0.645
---

  * ISEARCH-2530 — Дефолтные параметры для индексатора
  * Ничего не возвращаем в isearch reindex
  * ISEARCH-2395 — Сломается виджет сервиса в выдаче поиска
  * ISEARCH-2596 — В поиске пропали названия сервисов в сниппетах
  * https в урлах на сервисы + правильный тестинг Планера

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-07-11 13:57:33

0.644
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2556 — Умная загрузка модуля индексатора
  * ISEARCH-2555 — Удалить старый код индексаторов СТ и Этушки

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2522 — Переход на plan api v2
  * Временно отключить индексацию планировщика по расписанию
  * Реже индексировать оборудование

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-07-08 14:37:33

0.643
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2528 — Выводить параметры индексаций в админке

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс хостов Sentry
  * Обработка отсутствия лексера

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-07-03 17:07:53

0.642
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2562 — Принимать выбранные группировки с фронтэнда
  * stubdir для индесации лего-блоков
  * Фикс комбинации правил в колдунщике
  * ISEARCH-2574 — Не учитывать роботов в правилах колдунщика
  * ISEARCH-2563 — Использовать в админке быстрый запрос на количество документов
  * ISEARCH-2562 — Уникальные названия правил на вертикали людей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2570 — KeyError в конструкторе Kafka консьюмера

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-07-02 16:31:56

0.641
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * SEARCH-2503 — last\_check\_at и перезапуск check
  * ISEARCH-2561 — Честный id подразделения в группировке
  * ISEARCH-2561 — Фикс названия группировки по сервисам

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Таймаут на чтение из Kafka - 60 секунд
  * Удаляем дефолтные syslog хендлеры для celery воркеров

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-07-01 13:07:05

0.640
---

  * ISEARCH-2559 — Включить Kafka в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-27 10:24:27

0.639
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Название поиска в синей плашке при просмотре всех индексаций

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2559 — Включить Kafka в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-26 16:50:22

0.638
---

  * ISEARCH-2547 —  Комментарий к индексации обязательный в админке
  * ISEARCH-2548 — NoReverseMatch на странице ревизии
  * ISEARCH-2500 — Cводный список индексаций по всем поискам

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-25 17:16:08

0.637
---

  * Фикс миграции stale deleted

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-24 17:05:42

0.636
---

  * Фикс опций индексатора
  * В миграции в любом случае менять статус ревизии

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-24 16:22:23

0.635
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не проверять сертификат сервера в надметапоиске
  * ISEARCH-2541 — Выгрузка документов Вики в hadoop

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс миграции ревизий (часть сервисов уже не актуальны)

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-24 15:18:21

0.634
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фиксы purge индексатора
  * ISEARCH-2499 — Cмигрировать ревизии stale -> deleted
  * ISEARCH-2527 — Сохранять информацию об инициаторе индексации

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2551 — Включить нативные фасеты всем в СТ

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-24 14:14:25

0.633
---

  * Отключил пока параллельную сборку venv из-за бага

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-23 15:52:01

0.632
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2539 - verify=False для всего кроме продакшена в mldescription
  * ISEARCH-2539 - новый хост тестинга для mldescription
  * ISEARCH-2533 — Миграция по удалению updated
  * ISEARCH-2499 — Cмигрировать ревизии stale -> deleted

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2545 — Реплика мускуля видимо отстает
  * Параллельная сборка venv
  * Revert "ISEARCH-2499 — Cмигрировать ревизии stale -> deleted"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-23 15:39:34

0.631
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2537 — Сломалась индексация некоторых документов Вики
  * ISEARCH-2538 — Сломалось получение заголовка last-modified в индексаторе Документации

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-19 15:31:03

0.630
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2525 — Парсить через вики-форматер коммиты и вычленять тикеты
  * ISEARCH-2524 — Фасет по очереди СТ в поиске по Коду
  * ISEARCH-2532 — Ломает диагностика внутри do\_store
  * ISEARCH-2261 — 500 при поиске по пробелу в кавычках

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-18 18:15:34

0.629
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс стопа индексации со страницы ревизии

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-18 14:23:09

0.628
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2502 — check пишет текущее число документов
  * ISEARCH-2510 — Смигрировать на новый requests

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2504 — Остановка индексации на странице индексации
  * Фикс верстки запуска индексации
  * ISEARCH-2513 — Считать "успешную индексацию" с учетом ревизии
  * ISEARCH-2501 — Комментарий для индексации

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-18 13:11:17

0.627
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2520 — Окончательное выпиливание сниппетов
  * Удалил лишний файл забытый при мерже
  * ISEARCH-2519 — Принудильный flush индекса
  * ISEARCH-2502 — check пишет текущее число документов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс имени таски reindex в расписании

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2509 — Паджинация на странице со списком индексаций

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-17 13:13:45

0.626
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс получения id фасетов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-16 17:12:32

0.625
---

  * Фикс работы с новым django\_yauth

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-16 15:57:14

0.624
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * django-yauth=3.39

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2496 — Кнопка "удалить" для ревизии
  * ISEARCH-2486 — Группировка блоков по библиотеке

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-16 15:08:43

0.623
---

  * Сливаем в одну точки входа isearch и isearch-headless
  * ISEARCH-2498 — Добавить для чтения еще одну реплику mysql

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-11 19:42:29

0.622
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2471 — Последовательное получение id'шников фасетов
  * ISEARCH-2505 — Включаем нативные фасеты в Эткушке всем

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-11 18:13:38

0.621
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2497 — Выставлять параметр timeout= в запросах-счетчиках

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Кидаем ворнинг если не нашли пользователя
  * включаем для этушке новую схему индексации в celery-beat
  * ISEARCH-2494 — Починить колдунщик Клубов
  * ISEARCH-2483 — Падает индексатор Этушки по IndexError
  * ISEARCH-2495 — Починить поиски кода в админке

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-11 17:11:46

0.620
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс когда папки создавались только на одной машине

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-10 19:23:44

0.619
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс флажка realtime (должен быть булевским)
  * Фикс подсчета документов в SaaS в админке

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-10 17:18:00

0.618
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Прокидывать опцию nort при пуше
  * Создаем группировочные атрибуты для фасетов даже если они числа
  * Изменил работу с временными файлами для генерации тегов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-10 16:05:38

0.617
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2430 — Колдунщик репозитория
  * Подключаю колдунщик репозиториев

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-09 18:44:16

0.616
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2394 — Пробрасывать флаг realtime=no для больших переиндексаций
  * ISEARCH-2474 — Не использовать в нативных фасетах служебные символы

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2440 — Факторы для лего-документации
  * Не падать в админке, если не удалось получить количество документво

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2435 — Перестала работать сортировка по дате в поиске по Вики

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2402 — Поддержать jsonwithrefs формат SaaS

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не выставляем content-type сами
  * Возможность трассировки http запросов
  * Удалять документы надо тоже через тот же формат
  * Фикс проверки размера body в индексаторе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-09 13:17:36

0.615
---

  * Не проверяем серверный сертификат в роботе
  * ISEARCH-2435 — Перестала работать сортировка по дате в поиске по Вики

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-05 15:07:27

0.614
---

  * При удалении документа не отправлять check\_only\_before\_reply
  * Фикс определения формулы в визарде
  * ISEARCH-2476 — Эвристика для посылки флага check\_only\_before\_replay

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-05 14:09:30

0.613
---

  * Датамиграция для неправильных ревизий кода

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-03 16:26:23

0.612
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2467 — Поломались фасеты по клубу в этушке

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-06-03 13:42:07

0.611
---

  * Фикс создания документа в обучаторе
  * Дефолтное значение у количества тредов при запуске из админки

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-06-02 15:24:57

0.610
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * забыл удалить отладчик

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Удаление service=*-new ревизий

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-06-02 14:17:13

0.609
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс конфигов индексации (отдельные пути для дева не нужны)
  * Фикс индексатора study
  * Для всех сервисов индексация из дева смотрит в тестинг SaaS
  * ISEARCH-2452 — threads в админке
  * Стоп индексации при достижении лимита количества документов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-30 16:35:29

0.608
---

  * ISEARCH-2458 — Переключиться на новый SaaS в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-29 19:00:21

0.607
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не хайлайтим сниппеты в апи
  * не хайлайтим etree дерево, а сначала переводим в текст

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2458 — Переключиться на новый SaaS в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-29 18:09:22

0.606
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Новые хосты fml\_ops

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2453 — импорты в отдельной зоне
  * pygments в зависимостях
  * ISEARCH-2449 — имена классов и функций в отдельных зонах
  * ISEARCH-2457 — Поправить урл документа в бранчах

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-05-29 14:23:44

0.605
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix неправильной подвязки кода к документам
  * fix группировки
  * fix админки поиска по коду
  * ISEARCH-2447 — Фикс расцветки кода
  * причесал подсветку найденного кода

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс хостов api и wizard в настройках

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-28 15:52:28

0.604
---

  * Фикс сериализации lxml.html объектов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-27 16:34:28

0.603
---

  * SAAS-1940 - Некорректно прокидывается ql в restrict\_config, если запрос идет сразу в несколько сервисов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-26 20:49:39

0.602
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Очередной прототип поиска по коду

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * DummyCacheStorage для пуша. Миграция подчистки старых кешей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-26 18:50:46

0.601
---

  * ISEARCH-2438 — Доделать индекс по библиотекам лего
  * ISEARCH-2439 — Индекс по лего-блокам
  * Правило для поиска по лего

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-05-22 16:09:14

0.600
---

  * Фикс логирования ошибок Кафки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-20 15:09:19

0.599
---

  * ISEARCH-2436 — Перенести acl в параметр rescrict=

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-19 21:38:16

0.598
---

  * ISEARCH-2436 — Перенести acl в параметр rescrict=

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-19 17:20:14

0.597
---

  * Убрал выключение хождения в визард при фиче force\_new\_saas

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-19 14:22:59

0.596
---

  * Поддержка обновленного формата сообщения от СТ в Kafka

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-15 19:56:21

0.595
---

  * ISEARCH-2419 — Читать нотификации из Кафки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-15 17:31:18

0.594
---

  * Подчищаем протухшие соединения с базой после каждой таски

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-14 18:08:01

0.593
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Возможность проиндексировать несколько репозиториев через keys

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2427 — Кнопка on air! на странице ревизии
  * ISEARCH-2426 — Перекрестные ссылки в админке
  * ISEARCH-2428 — Выводить число индексаций у ревизии

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-05-14 16:55:07

0.592
---

  * Доделка стораджа ревизий

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-14 10:07:14

0.591
---

  * Фикс прокидки имени поиска в робот
  * Фикс получения активных ревизий для всех поисков

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-13 17:59:57

0.590
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2406 — Правильно считать группировочные атрибуты в админке

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс получения ревизии в compat бекэнде
  * Выставляем wait\_timeout для mysql соединения

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-13 16:28:21

0.589
---

  * Фикс получения текущих ревизий

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-13 12:29:05

0.588
---

  * Фикс выставления id таски для статуса
  * Прокидываем оргинальное исключение при ретрае

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-13 11:07:41

0.587
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2404 — Поиск по Лего-сайту
  * Информация про ревизии в админке

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Первичный рефакторинг reindex
  * Убираем использование search\_id и index по возможности
  * Фикс редиректа с морды админки

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * STALE\_TIMEOUT = 15 минут для codesearch
  * Переносим чекаут codesearch'а в /var/run/

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-05-12 16:33:51

0.586
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Рефакторинг стораджа статусов
  * Нативно форматируем дельты

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix ctags'ов в индексаторе кода

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-05-08 11:18:50

0.585
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Свой префикс для ylock в деве
  * Рефакторинг остановки индексации

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил в зависимости exuberant-ctags

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-05-07 17:00:23

0.584
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Прототип поиска по коду

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-05-07 14:26:40

0.583
---

  * ISEARCH-2407 — Прокидывать нужные правила колдунщика в запросе к SaaS

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-05-05 09:22:23

0.582
---

  * Revert "переписал на pygit2"
  * Revert "зависимости codesearch"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-25 17:37:25

0.581
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * переписал на pygit2

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Новый хост тестинга внешнего колдунщика в настройках

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * зависимости codesearch

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Забытый импорт yenv

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-25 15:41:40

0.580
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Фикс построения сниппета в старом индексаторе людей
  * Фикс генерации телефонов в swarm-индексаторе людей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Дефолтный datasource для дева
  * Выставляем в 5 минут жизнь соединения с базой

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-24 17:58:34

0.579
---

  * Убрал ненужный импорт cleanup
  * Проверяем в check в начале что индесация не сломалась
  * Фикс работы визарда для ml поиска
  * Фикс получения числа результатов для лога

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-23 13:35:20

0.578
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * AssertionError в пушах от этушки

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Рисуем правильно продолжительность индексации

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * codesearch: поменял местами индексацию кода и коммитов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Отрефакторил подчистку старых артефактов. Команда purge вместо clear и cleanup
  * Фикс получения соседей по сервису
  * Фикс сообщения об ошибке при формировании мета-запроса
  * Выставление таймзоны для celery
  * unicode\_literals в индексаторе людей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-23 10:28:53

0.577
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * В новом поиске людей класть отсутствия в кеш

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс использования лока в обычных тасках
  * Джанга 1.6.3
  * 32 воркера для обычных swarm очередей
  * Логирование ошибок базы на уровне таски

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * мелкие оптимизации поиска по этушке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-22 17:22:48

0.576
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * codesearch: индексируем только коммиты привязанные к файлам
  * codesearch: индексируем все коммиты в master банче

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-04-21 18:32:05

0.575
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ускоряем поиск по коду
  * fix кодировки в именах людей в этушке

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поднял число воркеров для базовых swarm очередей
  * Максимальный приоритет для пушей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-21 16:32:04

0.574
---

  * Поднимаем prefetch count для воркеров до 32
  * mongodb транспорт для celery с приоритетом
  * Прокидка дефолтного приоритета
  * Прокидка приоритета в reindex

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-21 14:44:43

0.573
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не сохраняем в сниппет документа с кодом коммиты
  * включаю фасет по языку программирования

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-04-18 17:50:31

0.572
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поднял число воркеров для очередей

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Протитип поиска по коду wiki

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-04-18 16:37:01

0.571
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Добавил забытый emit\_sort\_attr в документ
  * Конфиг nginx для api в тестинге свой

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Кеш в индексаторе людей
  * Фикс отсутствия города у офиса

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-04-17 14:56:48

0.570
---

  * Фикс импорта хайлайтера из api
  * Фикс формирования полного набора факторов для отправик в SaaS
  * В исключениях от SaaS прокидываем содержимое ответа
  * Не глотаем исключения, когда запускаем индексаторы без очереди

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-15 17:26:02

0.569
---

  * Фикс работы с формулой для мета-поиска

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-15 15:49:54

0.568
---

  * Фикс работы с локами

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-15 13:39:31

0.567
---

  * ylock 0.14
  * Теоретически лока может не быть

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-15 02:56:40

0.566
---

  * Фикс формирования имени лока
  * Используем другой префикс для локов в девелопменте

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-15 01:56:03

0.565
---

  * Используем неэфемерный лок

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-15 01:09:38

0.564
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Подвинул список источников в админке в /sources/
  * Убрал вывод хоста со страницы со списком индексаций

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)


 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-04-14 14:24:03

0.563
---

  * Запуск celery из upstart с полным путем к интерпретатору. Иначе execv не работает

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-13 16:36:15

0.562
---

  * Опять включил CELERYD\_FORCE\_EXECV

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-13 15:38:58

0.561
---

  * Обрабатываем ситуацию когда стадий за fail интервал не обновилось
  * Отрефакторил использование ylock

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-13 03:48:27

0.560
---

  * Фикс обертки над requests
  * Фикс отступов
  * Причесал get\_fails\_rate у стораджа статусов
  * Проавильно делем ретраи только том случае, если они нужны
  * Причесал параметры для next и do\_stage
  * Добавил параметр body\_format в emit\_body для совместимости со старыми индексаторами

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-13 01:17:10

0.559
---

  * Обобщение проверки актуалности запуска check
  * Проверка окончания индексации в отдельном методе
  * Вынес проверку рейта ошибок в отдельный метод
  * Проверка живости индексации смотрит на last\_updated стадий
  * Для старых индексаторов не делаем проверку на stale
  * Убрал работу с моделью индексации из индексера
  * Ещё апдейт стораджа индексации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-12 20:31:53

0.558
---

  * Включаем -Ofair для воркера
  * Включаем ACKS\_LATE
  * У старого документа тоже был id

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-10 21:21:56

0.557
---

  * Выстялаем мультипликатор для воркеров в единицу
  * Запускаем людей в 10 минут часа
  * Revert "Используем autoscale для воркеров celery"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-10 19:53:30

0.556
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Индексация людей каждые 2 часа
  * Используем autoscale для воркеров celery
  * Очередь cleanup в настройках

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Добавить к формуле сервис
  * В надметапоиске не собирать фичи вручную

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-04-10 16:42:21

0.555
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix создания сессии
  * fix 404х ошибок в индексаторе этушки
  * Кеш в монге для индексатора этушки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-04-10 16:00:00

0.554
---

  * Сторадж для кеша
  * Убрал ограничение на число тасок для воркера.
  * Проставялем статус canceled для отозванных тасок

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-10 01:38:41

0.553
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix логгинга новго индексатора этушки

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Таски по расписанию ставятся в swarm\_reindex очередь
  * Убрал qv таски из расписания
  * Фикс расписания для clear\_pushes

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-09 16:57:57

0.552
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Поиск по людям в swarm индексаторе

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2383 — Обновить индексатор этушки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-08 18:42:52

0.551
---

  * Свежий lxml 3.3.4
  * Убрал переопределение celery брокера в девелопменте
  * Отдельый модуль для работы с xml. Кастомные pickle сериализаторы для lxml сущностей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-08 14:20:13

0.550
---

  * Фикс итерации по бекэндам
  * Забытый импорт настроек

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-07 19:47:07

0.549
---

  * Фикс редиректа после начала индексации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-07 17:49:13

0.548
---

  * Форсирование использования нового SaaS через фичу

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-07 17:14:46

0.547
---

  * Ещё перенес код из моделей в стораджи
  * Убрал из настроек поиска вложенность про бекэнд. Плюс починил формирование урлов-счетчиков на странице индексации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-07 16:24:47

0.546
---

  * Ленивая подгрузка модуля индексации
  * Обработка пуша в старых индексаторах

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-04 20:18:33

0.545
---

  * Фикс запуска переиндексации в старую ревизию

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-04 18:48:18

0.544
---

  * Фикс опечатки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-04 17:46:23

0.543
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Причесывал новый индексатор
  * Распилил стораджи на модули
  * Убил IndexContext, заменив на revision
  * Подвинул swarm таски в isearch.tasks
  * Фикс работы с ревизией при индексации
  * Убрал методы open и finish у старых бекэндов
  * Избавился от self.context в старом бекэнде
  * Новый индексатор и DocumentStorage не зависит от backend
  * У консольного хендлера нету ограничения на уровень
  * Слой совместимости для старых индексаторов поверх новой инфраструктуры
  * Правильное удалание документов
  * Перенeс базовый индексатор в isearch.swarm
  * Сделал self.revision у индексатора
  * Избавился от модели Navigation
  * Если включен dry-run, то не сохраняем документ в do\_store
  * Флаг verbose больше не нужен
  * \_\_str\_\_ для документа
  * Выводим табличку со статусами в админке всегда
  * walk в своей отдельной ноде
  * Убрал do\_delete стадию
  * Не передаем request таски в do\_stage
  * Не ретраем setup
  * Убил внешние кофиги робота
  * Фикс циклического импорта

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Красивый запуск индексации
  * Возможность не делать ревизию активной после индексации
  * Только новая ревизия может сломаться

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убил revisions.json
  * Ревизия new рисуется желтой

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-04 17:27:09

0.542
---

  * Зафиксировал версию django-intranet-stuff
  * Фикс ручки принимающей push

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-03 16:05:36

0.541
---

  * Фикс выбора формулы в визарде

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-04-03 14:51:35

0.540
---

  * Индексация в определенную очередь стартрека

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-04-03 14:07:46

0.539
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * изменения в swarm индексаторе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-03 10:52:53

0.538
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Запятая в abovemeta

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Хеши для индексации в *-testing сервисы
  * Прокидывание user в revisions из визарда

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-04-01 14:06:40

0.537
---

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Правильный хост дева в настройках

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Ненужный параметр --force в reindex

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Правильно отправлять параметр check\_only\_before\_reply в SaaS

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Форсирование ревизий через фичи
  * Подвинул настройки в api.saas и сделал ключ indexer
  * Рефакторинг формирования урл'а для поиска
  * Новые хосты saas для dev и testing

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-31 19:59:04

0.536
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2391 — Закрасить совсем qv

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-03-27 18:28:24

0.535
---

  * Группировка по департаменту на вертикали людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-03-27 15:10:41

0.534
---

  * Revert "ISEARCH-2352 — Переехать на новый SaaS в продакшене"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-25 14:23:36

0.533
---

  * Убрал удаление gunicorn.* из postinst

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-25 13:01:50

0.532
---

  * ISEARCH-2352 — Переехать на новый SaaS в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-25 12:43:31

0.531
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Откатил комит 91c50ee

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * gunicorn пишет свой лог в syslog
  * Использование kombu=3.0.14
  * Индексация в новые сервисы через админку

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-24 18:31:09

0.530
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * delete copytruncate from logrotate

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * logrotate конфиг для celery-worker не нужен

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2382 — Включить новые фасеты в СТ всем

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-03-20 17:34:56

0.529
---

  * Колдунщик на вертикали людей всегда называется одинаково

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-03-17 16:12:58

0.528
---

  * Убрал statbox-logrotate из install

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-17 13:52:30

0.527
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Избавился от prepare\_document
  * Отключаем HIJACK\_ROOT\_LOGGER
  * Апдейт настройки окружения
  * Дефолтный логгинг в intrasearch-headless
  * Убрал statbox
  * searchlog -> abovemeta
  * Celery пишет в syslog
  * Старый индексатор тепер тоже пишет логи в intrasearch-headless
  * Подчистка старых директорий с логами
  * Убрал флаг -l у reindex

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Лок в удалении статусов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-03-17 13:18:23

0.526
---

  * Фикс рекурсивного вызова QueryDict

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-13 18:03:59

0.525
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2373 — Добавить в <backend> информации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Перенес логику из таски \_do\_stage в метод do\_stage индексатора
  * Делаем ретраи для DatabaseError
  * Хождение по http в новом индексаторе через isearch.utils.http
  * Поднял retries до 8
  * Используем COUNTDOWN только для check

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-13 17:27:36

0.524
---

  * Обработка большего числа ошибок получения данных от СТ

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-12 15:59:21

0.523
---

  * Явный флаг отключения сохранения статусов
  * Причесал setup
  * Чуть-чуть поправил логгинг и прокидку ошибок в индексаторе
  * Поднял число параллельных walk до 4

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-12 10:50:14

0.522
---

  * Фикс транспорта для Celery

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-11 12:52:16

0.521
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Положил исправленный kombu транспорт

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-03-07 15:49:46

0.520
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2319 — Native фасеты

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-03-06 14:07:52

0.519
---

  * Убрал лишний параметр в \_do\_stage
  * walk в 2 куска

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-03-04 19:08:24

0.518
---

  * Фикс старта таски

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-03-04 17:35:43

0.517
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Включаем компрессию Celery
  * tornado 3.2

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Revert "Пуш через старый индексатор"
  * ISEARCH-2358 - Фикс пуша в новый индексатор
  * ISEARCH-2306 — Ходить в st с User-Agent

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-03-04 16:38:22

0.516
---

  * ISEARCH-2369 — Пессимизировать GRAPHCONTENT в поиске по стартреку
  * Чанки волка
  * Логи check'a в индексацию
  * Не выполнять стадию, если индексация в статусе fail

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-03-03 15:42:00

0.515
---

  * Не рейзить ошибку
  * ISEARCH-2328 в swarm-индексаторе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-28 16:07:14

0.514
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Явно пишем в лог scope

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Волк
  * Брать task\_id сразу после таска, обновлять стадии апдейтом
  * store в отдельной ноде, 12 воркеров swarm

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-28 14:07:10

0.513
---

  * Схлопнул таблицу статусов
  * Записываем task\_id внутри стадии

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-02-27 10:14:41

0.512
---

  * Прописал индексации по расписанию к очереди reindex
  * Проверяем, что взялся лок
  * Поднял минимум до 2х воркеров все ноды кроме дефолтной. И 16 в swarm

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-02-26 22:29:27

0.511
---

  * Правильный запуск celery-instance

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-02-26 17:58:01

0.510
---

  * ISEARCH-2366 — Разломана индексация Вики
  * Уменьшил число воркеров

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-02-26 17:03:43

0.509
---

  * Фиксы swarm индексации: добавление атрибута, cleanup

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-26 14:10:56

0.508
---

  * Поменять commited и online статусы ревизий на active

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-25 17:04:11

0.507
---

  * Возможность индексировать из амдинки в определенную ревизию
  * Фикс создание swarm-индексации
  * Фикс обхода стартрека
  * Больше ретраев для похода в саас

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-25 14:55:01

0.506
---

  * Фикс key\_hash в новой индексации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-24 18:08:38

0.505
---

  * Пуш через старый индексатор

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-24 17:19:03

0.504
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не ходим за именами фасетов в базу, а берем из конфига

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Правильный native\_id в swarm индексаторе стартрека
  * ISEARCH-2362 — Чекбокс запуска индексации с новой ревизией в админке
  * ISEARCH-2358 — Пуш в swarm индексатор
  * Ретраи для новой индексации
  * Количество воркеров в основных стадиях swarm - 16

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-24 16:06:50

0.503
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2357 — Пуш в несколько ревизий

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * В чеке считать errors rate

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-20 16:19:20

0.502
---

  * Забирать из intrasearch-celery только *.conf файлы
  * Отправлять неиндексации в management очередь

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-19 13:55:12

0.501
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Зафиксировал версии celery, kombu и billiard
  * Зафиксировал версию ipdb

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * ISEARCH-2356 — Сломалась логика остановки swarm индексации
  * celery конфиги

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-19 11:13:35

0.500
---

  * yandex-dh-clearvcs в Build-Depends

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-18 11:13:15

0.499
---

  * git в Build-Depends

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-18 10:20:24

0.498
---

  * Миграция для статуса таски

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-17 12:56:09

0.497
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Правильная настройка celery result backend'а

 * [Nataliya Kryuchkova](https://staff.yandex-team.ru/Nataliya%20Kryuchkova)

  * Миграция с дефлотами для новой джанги
  * Статус in progress для таски
  * Фейлить индексацию, если долго не меняется количество завершенных тасков

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-14 17:40:32

0.496
---

  * Фикс создания SimpleBackend

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-13 16:35:18

0.495
---

  * Фикс создания бекенда для платформы
  * Админка для новой индексации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-13 14:20:08

0.494
---

  * Для пуша используем старую индексацию

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-11 16:59:24

0.493
---

  * Новая индексация

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-11 16:20:38

0.492
---

  * ISEARCH-2338 — Внедрение нового визарда

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2014-02-05 15:32:43

0.491
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2325 — С главной админки не запускается переиндексация клубиков

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2332 — Переиндексировать этушку один раз в неделю
  * Переводим все индексаторы на новые сниппеты

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-02-03 14:39:37

0.490
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2328 — проперти разделяются пополам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-27 16:23:50

0.489
---

  * Переделал raw\_post\_data в body

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-23 19:12:03

0.488
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2323 — Проблемы с сервисными сниппетами

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-01-23 15:36:07

0.487
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Забыл некоторые проперти

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-01-23 13:17:07

0.486
---

  * Добавил *.egg-info в игнор
  * Над-мета-поиск ходит в api на localhost

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-22 23:34:19

0.485
---

  * Обработка runtime ошибок хайлайтинга

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-22 21:58:50

0.484
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2322 — нет информации о данных для колдунщика в сниппете

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-01-22 20:41:16

0.483
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Спиппеты по новой схеме в mldescription

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-01-22 17:24:52

0.482
---

  * Пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-21 08:50:02

0.481
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Апдейт шаблона информации об индексации

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * update gitignore
  * Не ходить за сниппетами в базу когда не надо

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2014-01-20 19:56:09

0.481
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2318 — Перенести сниппеты в проперти документа

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс конфигов урлов
  * Зависимость от Django 1.6.1

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-19 21:17:45

0.480
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Убрал инфологи от kazoo

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Явный set names utf8 в настройках соединения с базой
  * mysql-client в зависимостях в правильный местах

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-15 17:24:24

0.479
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Причесал documents.py

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс имени параметра

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-14 16:37:39

0.478
---

  * Фикс запуска переодических команд
  * Фикс запуска celery воркера
  * Фикс пидфайла для celery beat

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-14 13:01:13

0.477
---

  * Фикс прокидывания настроек ylock
  * ISEARCH-2312 — в заголовках не выделяется болдом текст из запроса
  * Использование su для запуска celery beat
  * Фикс индексации клубов без постов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-13 19:56:49

0.476
---

  * Лишнее использование datasources
  * Подавляем ворнинги от datasources

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2014-01-09 14:09:30

0.475-1
---

  * Пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-12-25 02:02:28

0.475
---

  * kombu из git'а с патчем для mongodb

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-12-24 17:00:17

0.474
---

  * Выпиливаем раскладку nginx конфигов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-12-19 20:06:51

0.473
---

  * ISEARCH-2300 — Выпилить оставшиеся nginx конфиги.
  * Активация nginx конфигов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-12-19 19:27:34

0.472
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1677 — Подчистка старых артефактов
  * Убрал зависимость от conductor

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Убил пакет memcached

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Пока не получаем memcached хосты из ds

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-12-16 14:29:27

0.471
---

 * [Никита Зубков](https://staff.yandex-team.ru/Никита%20Зубков)

  * fix rules

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2280 — Запуск индексации с флагом --debug в админке

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Еще раз починил багу с юникодом и пост запросом
  * Добавил pytils в зависимости

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс нового визарда

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-12-09 14:45:17

0.470-1
---

  * Удалил из потрохов дебиана упоминания nginx.conf'ов для админки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-12-05 13:48:47

0.470
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не используем python деб-хелперы

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Исправления nginx конфига
  * В продакшен стафф ходим только из продакшена

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-12-05 13:34:59

0.469
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновил ylock
  * ISEARCH-2293 — Зависимость от rsyslog
  * Неправильно пробрасывали таймауты
  * Обновил версию lxml

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-12-04 18:56:32

0.468
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2279 — Выключить DEBUG в тестинге
  * ISEARCH-2274 — Поддержать datasources
  * Заменил порт опечаточника
  * ISEARCH-2275 — monrun для /ping
  * ISEARCH-2264 — Перейти на upstart
  * Апстарт для визарда
  * Переключил в фабфайле сборку на пресайз
  * fix datasources
  * Переделал upstart
  * ISEARCH-2277 — Перейти на celery scheduler вместо cron
  * Удалил из постинстала все про гуникорн
  * ISEARCH-2291 — Симлинки для upstart конфигов

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2238 — Заготовка приложения для отдельного визарда
  * Фикс хоста для девелопмента

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-12-04 14:21:35

0.467
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Разрешаем заход с любого хоста

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-28 17:52:41

0.466
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2265 — Добавить подробное логирование с таймингами для
    индексации источников

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-28 13:51:38

0.465
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обход ошибки с сохранением бинарных данных

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-27 15:06:43

0.464
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Баг с пост-запросами

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-26 19:01:42

0.463
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2250 — Перейти на hilite3
  * Выпилил из кверивьювера генерируемые чойсезы
  * ISEARCH-2080 — Добавить в индекс по людям описание группы со стаффа
  * Зависимость от свежих ylock и kazoo
  * Фиксы виртуального окружения
  * Fix конфига ngnix админки поиска

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2243 — Упаковка в virtualenv

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-25 15:52:41

0.462
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2241 — Перейти на внешний ylock
  * ISEARCH-2249 — Data-миграция удаления старых артефактов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-12 14:45:06

0.461
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс модтайма для комментов этушки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-11 14:29:38

0.460
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2240 — Условная зависимость от хайлайтера

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс прокидывания mod\_time в индексаторах Этушки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-11-11 13:55:35

0.459
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2239 — Не прибивается индексация
  * Фикс запуска индексации из админки

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-11-07 14:51:06

0.458
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не создаем ненужные директории

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2152 — Неправильно работает сортировка по дате
  * SEARCH-2237 — Убрать final и множественный target у правил

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-11-07 13:04:22

0.457
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2231 — Ломается админка правил внешнего колдунщика

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поменял пункты меню в шапке админки
  * ISEARCH-2170 — Выпилить работу с Я.Сервером

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-11-06 14:54:21

0.456
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс вывода колдунщиков

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-11-05 16:54:12

0.455
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил статус код в xml с данными об ответах бекендов
  * Некоотрые улучшения производительности кверивьювера
  * Упростил пагинатор
  * Вкомпилил старые датафильтерзы, в кверивьювер
  * Ссылка на кверивьювер больше не ведет на топ
  * ISEARCH-2179 — Перевести все формы api на wtforms

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс добавления статус кода в ответах бекендов
  * Фикс фактора численности команды сервиса
  * Цвета для шапки админки такие же, как в бутстрапе
  * Фикс запуска индексации
  * ISEARCH-2223 — Редактирование списка правил внешнего колдунщика
  * Мелкие фиксы странички про формулы

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-11-05 15:57:02

0.454
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2210 — неправильно считаются факторы по заголовкам в Вики
  * ISEARCH-2222 — Не индексировать серые проекты

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Эпичный баг в сериализаторе xml
  * ISEARCH-2220 — в колдунщике сервисов в team\_size считать только
    уникальных пользователей
  * ISEARCH-2218 — Обрабатывать сокетные ошибки
  * ISEARCH-2194 — Ходить за страницами Вики по https

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-31 15:54:03

0.453
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2215 — Страницы-редиректы не удаляются из индекса

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix бага к пятисоткам приводящего
   Забыл отладку в тестах
  * ISEARCH-2200 — Не пятисотить если фасеты не вернули данные

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2216 — Убрать правило custopwords из вызова внешнего
    колдунщика в поиске по вики и метапоиске

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)


 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-29 15:17:28

0.452
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2202 — Добавить ретраи на 5xx ошибки при индексации
    стартрека

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2178 — Выводить ответы бекэндов в xml

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2072 — Фактор isTrashTitle для вики-страниц
  * ISEARCH-2070 — Вынести офис в отдельную зону в поиске людей
  * ISEARCH-2171 — Удалила фактор isDIY
  * ISEARCH-2126 — Сервисы: фактор STAT\_services\_teamCount

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2176 — Починить тесты abovemeta

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2213 — Ходить в API стартрека с токеном в хедере

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2187 — Не пускать без логина в админку

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2198 — Колдунщик внутреннего поиска не считает руководителя
    сервиса частью команды сервиса

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2201 — Запуск индексации из админки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-29 14:01:40

0.451
---

  * Пересборка с новой версией

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-25 17:53:05

0.450
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс просмотра результатов поиска в админке
  * ISEARCH-2158 — Мета-информацию об индексации оформить в таблицу
  * ISEARCH-2157 — Сохранять в индексацию id celery таски и имя лока
  * ISEARCH-2156 — Кнопка убивания индексации  в админке
  * Выводить общее количество документов в индексе
  * Фикс request\_builders
  * Не нужен сайдбар для просмотра поисков
  * ISEARCH-2159 — Сделать цветовое кодирование окружений в админке
  * ISEARCH-2158 - Больше информации в табличке индексации
  * Сортировка по времени в админке
  * Фикс верстки админки
  * Фикс фэйла индексации
  * ISEARCH-2157 - Переименовала celery\_id в task\_id

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-25 17:48:31

0.450
---

  * Отключил preload для abovemeta

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-24 20:46:53

0.449
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убил обработку формы фидбека

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * get\_text\_content может принимать распаршеный xml
  * ISEARCH-2191 — atsearch: правильно обрабатывать время обновления
    поста от api

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2141 — в пассаже из первых первых слов со страницы не
    отображаются тикеты

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Явный chdir и INFO логи для gunicorn

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-24 18:13:58

0.448
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2172 — Ломается выдача в колдунщике сервисов при сортировке
    по дате
  * ISEARCH-2171 — Дополнительные расширения для фактора isVodstvo
  * Фикс списка факторов
  * Фикс опечатки в настройках

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-24 10:45:52

0.447
---

  * Пишем в sentry только ERROR логи
  * Фикс опечатки
  * Фикс проверки ответа /ping от API
  * AliveMiddleware первая в списке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-23 18:05:17

0.446
---

  * ISEARCH-2193 — Заменить gunicorn-init на ubic
  * ISEARCH-2148 — Добавить правила ProximByAveFreq и Phrase в вызов
    внешнего колдунщика на поиске по Вики
  * Таймаут на запрос в зону 10 секунд
  * exception логи abovemeta
  * Пингуем API
  * Правильно проверяем is\_success

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-23 16:03:25

0.445
---

  * Включаем все поиски через SaaS по-дефолту
  * Revert "ISEARCH-2184 — Переделывать в POST только запросы в
    Я.Сервер"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-22 13:52:44

0.444
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Форматируем урл, только если переданы данные для форматирования
  * fix NameError в надметапоиске
  * ISEARCH-2114 — если в результатах пост с комментарием, то в сниппете
    пишется время последнего комментария к посту

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-21 20:05:46

0.443
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2181 — Обернуть над-мета-поиск в nginx
  * ISEARCH-2184 — Переделывать в POST только запросы в Я.Сервер
  * ISEARCH-2175 — Проверять статус ответа в SearchTrigger

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-21 18:56:18

0.442
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Пофиксил ошибки с пост запросами к api

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-18 20:17:17

0.441
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не правильно считался фактор membersCount
  * Переиндексация этушки каждый час
  * ISEARCH-2131 — Ходить в API через nginx

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поле user обязательно
  * Возвращаем правильные статус-коды в над-мета-поиске
  * Нет больше переиндексаций на Я.Сервере

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2167 — Пустой usercluster ломает индексацию
  * ISEARCH-2166 — Ломается индексация wiki на Я.Сервере
  * ISEARCH-2162 — Мигает расстояние между запросами

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-18 19:28:04

0.440
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс индексатора вики (index\_resource)

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Используем json индексацию для клубов

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Отключить хождение по редиректам в роботе

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2146 — Понизить таймауты в 2 раза

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Для документации разрешить 302, 301

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-16 17:21:22

0.439
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Эскейпим контент в функции get\_text\_content
  * Добавил в треш клуб "Новости личного состава"

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2147 — Убрать правила ExtendNumber и Number из вызова
    внешнего колдунщика в поиске людей
  * ISEARCH-2148 — Добавить правила ProximByAveFreq и Phrase в вызов
    внешнего колдунщика на поиске по Вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-16 13:51:21

0.438
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2112 — дублируется текст в пассаже

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-15 17:19:52

0.437
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Правки индексатора этушки

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Удаление документов из вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-15 17:11:06

0.436
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Количество тредов для отладки

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2129 — Убрать подстановку оригинального запроса через ИЛИ
    (|)
  * SEARCH-2128 — Возможность переопределять правила saas-колдунщика
    через эксперимент
  * Фикс обработки имен на вики-странице
  * ISEARCH-2137 — Не показываются фасеты в просмотре поисков

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-15 16:10:57

0.435
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2119 — Реанимировать индекс по Статистике
  * Фикс опций реиндекса
  * Фикс построения результата запроса в админке
  * ISEARCH-2121 — В вёрстке не работает группировка по doc\_group
  * ISEARCH-2122 — Вернуть информацию про тикеты в генерацию пассажей
  * ISEARCH-2133 — Включить поиск по Вики в Saas по-дефолту
  * Добавлять в документ информацию про индексацию

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс форматирования лога при запуске шел-команд

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Улучшаем производительность индексатора этушки
  * ISEARCH-2132 — Сделать ретраи в над-мета-поиске

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-14 19:41:28

0.434
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Починил сломанный пуш от этушки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-10 18:15:24

0.433
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2103 — Вынести в отдельную зону содержимое wiki-ticket*

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-10 15:41:34

0.432
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Сортировка по дате в стартреке
  * ISEARCH-2081 — не срабатывает сортировка результатов по дате в
    эксперименте

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2098 — Добавить фактор isTrashClub для трешовых клубов и
    всех постов из этих клубов
  * ISEARCH-2093 — Уменьшить сниппеты клубов в поиске по этушке
  * Вернул вырезание тегов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-10-10 14:31:10

0.431
---

  * Фикс работы с тегами вики-страниц

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-09 13:20:22

0.430
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс обертки ./run

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс ошибки об отсутствии ревизии

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Ловим и логируем все ошибки в тасках тредпула

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Если платформа вернула 4хх, то не делаем ретраи
  * Статические мета-факторы для вики
  * Другой запрос факторов в платформе
  * ISEARCH-2085 — Фикс добавления куска страницы в сниппет
  * ISEARCH-2102 — Нормировать количественные факторы в поиске по вики \
    метапоиске
  * Добавить в вики отдельный фактор для последней части тега

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Правильные имена логеров в isearch
  * Возможность переиспользовать пул
  * Слегка причесал индексатор Этушки

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2104 — не отображаются логины в тайтлах и пассажах
  * Не падаем при таймауте

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2061 — Инкрементальная индексация Вики
  * Хранить название параметра для use-ts в настройках

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-10-08 17:36:38

0.429
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс выставления статуса ревизии

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Не ломаться на внешних поисках

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-03 12:53:52

0.428
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Правильное именование фактора для вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-02 13:53:31

0.427
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Revert "Правильный mod\_time"
  * ISEARCH-2085 — Добавлять в сниппет Вики-документа небольшой кусок
    тела страницы
  * Выкинуть остатки meta-study
  * Запрос для мета-поиска платформы
  * ISEARCH-2084 — Cтатические факторы по мета-информации страниц в
    поиске по Вики

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-10-02 12:23:42

0.426
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2082 — в эксперименте сломался поиск по кластеру

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не читаем из базы при инициализации
  * Добавил мемкеш в админку

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-09-30 19:04:17

0.425
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Ошибка индексации если не проиндексировалось 10 документов подряд
  * Правильный mod\_time

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ИНдексация этушки пятничным вечером

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-30 14:25:10

0.424
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Увеличил таймауты лока для индексации вики по крону

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Метафакторы
  * Переименовывать зоны в отдельном методе
  * Генерация конфига с метафакторами
  * Формула для метапоиска
  * Выкинуть meta-study

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-30 10:42:15

0.423
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Неправильная регулярка хоста
  * fix typo
  * ISEARCH-2079 — Починить пуш Этушки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-09-27 18:58:22

0.422
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2078 — Писать логи индексации ещё и в файл

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Пишем в лог сколько документов проиндексировано
  * Body-format теперь передается в функцию emit\_body
  * Включил админку для queriview
  * Неправильно работал триггер All

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс колдунщиков invite, mldescription, study

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-09-27 17:03:25

0.421-1
---

  * Пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-26 18:26:22

0.421
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Считаем None как отключенную фичу

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Убрать буст для вики в платформе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-26 15:34:17

0.420
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Допольнительные проверки чтобы не падать

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс вывода логов индексации для поиска в админке

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Разные правки во вьювере

 * [knopka](https://staff.yandex-team.ru/knopka)

  * check\_only\_before\_reply при добавлении документа

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не парсим хлебные крошки у Документации, если их нет
  * Фикс описания хелперов
  * Избавился от хелпера index
  * ISEARCH-2068 — Сделать возможность выключить эксперимент через get-
    параметр

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-26 13:47:19

0.419
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс приведения к строке триггера внешнего колдунщика

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не падаем если внешний визард недоступен

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Включаем CELERYD\_FORCE\_EXECV

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обернул внешний визард в Optional триггер
  * Фиксы клубов

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс пути fml\_ops2 для дева
  * Использовать данные из метрики
  * ISEARCH-2066 — Мусор в пассаж в сниппетах поиска по Вики
  * ISEARCH-2060 — Вики, зонные факторы по заголовкам

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Выставляем флаг check\_only\_before\_reply
  * Требуем doc\_index при поиске из админке

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил кусок описания в сниппет клуба
  * Многопоточная индексация этушки

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс диспатчинга в индексаторе Этушки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-25 23:51:32

0.418
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Переход по страницам выдачи в админке
  * Мелкие фиксы шаблонов админки

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Пишем логи в celery воркере
  * Возможность задать длину очереди в пуле тредов
  * Можно задавать длину очереди для тредов через параметры
    index/reindex

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-24 15:24:44

0.417
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс админки

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-23 16:02:45

0.416
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Формула для вики
  * Фикс админки: не падать если не работает саас-поиск

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Эскейпим логи в админке
  * Установил дефолтное значение для количества мемберов
  * Лимит на количество людей а не постов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-23 15:35:48

0.415
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Неверно вырезали переводы строк для генерации формулы
  * Баг в админке при поиске по этушке
  * Факторы репостов
  * ISEARCH-2048 — Левые люди в авторах поста

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2018 — Вырезать теги из описания сервисов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-09-19 17:43:11

0.414
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс итерации по ревизиям в генерации конфигов

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Включил клубы в выдачу надметапоиска
  * Общая функция для выделения текста из html
  * Добавил фактор isThread
  * Поддержал limit документов в поиске по этушке
  * Добавил в конфиг индекс по клубам

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-09-18 17:10:41

0.413
---

  * Не кидаем ошибку если можно создать новую ревизию

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-18 13:57:24

0.412
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2004 — Индексировать клубы Этушки

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Дефолтное число тредов индексации 1

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-18 13:29:52

0.411
---

  * Подвинул тредпул в isearch
  * Отправка документов в SaaS в несколько потоков

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-17 18:10:00

0.410
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1989 — Добавить фактор isResolved для стартрека
  * ISEARCH-2033 — Статические факторы по статусам проектов в поиске по
    планеру
  * ISEARCH-2037 — Статические факторы по статусам в поиске по сервисам
  * Фикс генерации конфига

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Баги в индексаторе этушки
  * Добавил факторы в комментарии

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс сохранения формулы
  * Фикс мемориального сотрудника

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил в сниппеты контент поста

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Добавила сервис в fixtures ревизий

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Включил формулу в этушке

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс работы с ревизиями в cleanup

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Лимит ошибок от плафтормы в индексаторе

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-2039 — В фасетах учитывать только треды
  * ISEARCH-2045 — Убрать мусор из пассажей в поиске по этушке
  * ISEARCH-2046 — Разделить фактор по типам постов на несколько

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2032 — Вынести ключевые слова сервисов в отдельную зону в
    поиске людей

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс индексации документации

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2018 — Забирать html вместо вики-разметки в из апи планера

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Поправил спрятанные зоны в этушке

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)


 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-17 15:47:14

0.409
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2020 — Факторы для драфта поиска по Вики

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Приводим id ревизии к строкам
  * Увеличил число потоков у робота Вики
  * Возможность указать id ревизии при переиндексации
  * Фикс формирования общего списка факторов для сервиса
  * Фикс генерации конфига факторов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-13 15:01:49

0.408
---

  * Фикс формирования meta запроса
  * Фикс конфига для meta поиска

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-13 11:08:47

0.407
---

  * Фикс вывода списка поисков в админке
  * ISEARCH-2031 — Мета-поиск для SaaS

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-13 09:35:26

0.406
---

  * ISEARCH-1996 — Фильтровать артефакты по активным ревизиям
  * ISEARCH-1991 — Использовать ревизии для формирования поискового урла

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-12 18:38:42

0.405
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс формирования документа в сервисах

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-12 17:12:58

0.404
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1998 — Имя инстанса SaaS в админке

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Ждать если платформа вернула не 200

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-2030 — Ретраи с задержкой при индексации SaaS

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-12 16:10:27

0.403
---

  * Не инициализируем пустой индекс при установке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-12 14:28:00

0.402
---

  * Специальный кейс для meta при поиске ревизий

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-12 13:27:45

0.401
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс получения title в Документации

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-2008 — Убрать слова «Бывший сотрудник» из поиска для
    мемориальных сотрудников
  * ISEARCH-2024 — Поиск игнорирует формулу для поиска по сервисам

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * обавил фасет про время поста

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1990 — Добавить имя инстанса SaaS в ревизии
  * ISEARCH-1997 — Индексация смотрит на ревизии
  * ISEARCH-2000 — Дополнительные опции для reindex
  * Апдейт RevisionContext
  * Убил ненужный файл

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-12 09:45:49

0.400
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В продакшене ходить в fml\_ops

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Поиск по этушке

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-09-11 16:57:42

0.399
---

  * Фикс получения сервиса для поиска

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-10 21:18:27

0.398
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс json индексации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не коммитим уже закоммиченные ревизии
  * Ходим в отдельные сервисы

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-10 20:59:45

0.397
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс прокидки ревизии

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Использовать разные сервисы платформы
  * Правильно определять, в какой сервис ходить за формулой
  * Индексация вики в платформу
  * Англоязычный индекс вики в платформе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-10 14:32:24

0.396
---

  * ISEARCH-2000 — Дополнительные опции для reindex

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-05 16:02:45

0.395
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Оставляем тройной индекс для Snippet в миграциях

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не забираем пока из базы ревизии для артефактов
  * ISEARCH-2000 — Дополнительные опции для reindex

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-05 15:35:21

0.394
---

  * ISEARCH-1996 — Фильтровать артефакты по активным ревизиям

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-04 15:08:12

0.393
---

  * Оставляем тройной индекс для Snippet

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-04 14:50:17

0.392
---

  * ISEARCH-1994 — Заморозить инкремент ревизий

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-04 13:46:41

0.391
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1972 — По запросу 'рекрутер киев' не находится никто

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1994 — Заморозить инкремент ревизий
  * Фикс 32-ой миграции
  * ISEARCH-1995 — Добавить в артефакты ссылку на ревизию

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-09-04 13:34:41

0.390
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1982 — Добавить правило для вырезания стопслов в вызов saas-
    колдунщика

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1974 — Добавить ключ тикета в зону очереди
  * ISEARCH-1975 — Добавить проекты в индекс по стартреку
  * ISEARCH-1948 — Факторы *\_z\_people\_car\_number всегда нулевые
  * dev- конфиги больше не нужны

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Получение url из запроса, если его нет в ответе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-09-02 19:19:02

0.389
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс шаблонов админки
  * Новые хосты документации
  * Используем отдельный сервис для поиска по стартреку
  * Удалила неактуальные фичи
  * Из дева ходить в престейбл конвертера

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-08-29 16:48:09

0.388
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс настроек

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-08-28 17:44:44

0.387
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1889 — Подключить отдельный инстанс saas для ST
  * ISEARCH-1888 — Добавление факторов в индексаторе
  * ISEARCH-1923 — Добавить фактор isTest для стартека
  * Поправила хэши стартрека + ищем пока в сервисе intrasearch
  * Фича для прокидывания сервиса в стартрек

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-08-28 17:19:18

0.386
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Для документации используем старый индекс

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-08-28 15:12:13

0.385
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Поправил минимальную версию зависимости от opster

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Переименование опции body\_format в reindex
  * Не менять kps для метапоиска
  * Переключаемся для всего на новый kps

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-08-28 12:56:02

0.384
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В fixtures старые ревизии платформы неактивны

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1967 — Плохо ищутся бышие сотрудники (например, f355@)
  * ISEARCH-1969 — Пропадают поисковые атрибуты

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-08-27 11:50:15

0.383
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил описание request\_builders.py

 * [knopka](https://staff.yandex-team.ru/knopka)

  * При поиске использовать kps из базы

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-20 18:53:27

0.382
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Сломалась индексация людей
  * Убил воскресший по непонятной причине файл
  * Вернул на старое поведение генерацию id для DSIndexer
  * ISEARCH-1912 — Теряются ссылки на Вики для сервисов в навигационном
    источнике

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-19 16:59:07

0.381
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Забыл закрыть тег
  * Удалил ненужную менеджмент команду
  * ISEARCH-1928 — Переход на commonjson
  * ISEARCH-1952 — Привести в порядок id документов
  * ISEARCH-1956 — Ломается обработка лога

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-13 15:27:46

0.380
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1953 — Нет значения таймаута для facets\_ids

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Обработка ошибок при обходе страниц с тикетами в API ST

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-08-09 14:11:59

0.379
---

  * Ещё раз обновил хосты для fml\_ops2
  * Не запускаем миграции в postinst

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-08-08 17:15:33

0.378
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1951 — Обрезаются поисковые логи
  * Мелкие правки в сервисном индексаторе

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Хосты для fml\_ops2 в тестинге и продакшене

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-08 16:50:26

0.377
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Fix кронов queryview
  * Баги в парсере

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-08 13:16:04

0.376
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал указание портов старых базовых поисков

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Принудительно создаем симлинку
  * Сразу удаляем старую папку с индексом

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-07 17:30:11

0.375
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Увеличил таймауты
  * Ускорение сниппетов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-07 14:35:51

0.374-2
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Кладем логи таймаутов вместе с логами надметапоиска
  * Неправильное имя mysql-пользователя

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-05 15:35:49

0.374-1
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил в зависимости python-chardet

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-05 14:16:26

0.374
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Таймауты для надметапоиска
  * Добавил время начала запроса в логи
  * Отключил эскейпинг в поисковых логах
  * ISEARCH-1515 — Перенести вьювер в админку поиска

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2013-08-02 19:38:11

0.373
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix dict'а как дефолтного параметра

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В индексаторе людей отделить сервисы от работы
  * Фиксы просмотра поисков в админке

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-07-30 16:27:51

0.372
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс фактора isHead/isDeputyHead в людях

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-07-24 17:38:26

0.371
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1933 — Выкинуть описания сервисов из индекса по людям

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-07-24 14:57:49

0.370
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс сниппета людей
  * Удалила isOutworker из статических факторов людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-07-16 17:39:47

0.368
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Реализация кастомного \_\_deepcopy\_\_ для поискового контекста

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1922 — Обрабатывать фичи приходящие в запросе
  * ISEARCH-1884 — Сделать таблицу для хранения формул
  * ISEARCH-1886 — Триггер с формулой
  * ISEARCH-1887 — Страница в админке для просмотра/редактирования
    формул
  * В просмотре поисков добавила релевантность
  * Название фичи с формулой разное для разных поисков
  * ISEARCH-1871 — Перевести поиски на SaaS
  * ISEARCH-1887 — При компиляции формулы могут быть разные сервисы
  * ISEARCH-1871 — Зонные факторы в конфиге
  * ISEARCH-1922 — Фикс получения фич
  * ISEARCH-1871 — Добавлять факторы при индексации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-07-11 15:29:31

0.367
---

  * Поправила поход в планер из индексатора людей

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-07-08 18:44:29

0.366
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1871 — Убрала зоны-веса из оборудования, рассылок, людей и
    планера

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Все контексты имеют доступ до search\_context

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Из описания рассылок ходить за сервисами

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Используем weakref.proxy
  * Апдейт подавления ворнинга монги

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-07-05 19:14:07

0.365
---

  * ISEARCH-1871 — Перевести поиски на SaaS
  * Фикс индексации этушки

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-07-02 18:16:43

0.364
---

  * Правильный список правил внешнего колдунщика

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-26 09:37:33

0.363
---

  * Фикс шаблона админки
  * Сохраняем исходный запрос при переколдовки внешним колдунщиком

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-25 16:18:47

0.362
---

  * Фикс форматирования запроса в админке
  * Берем в скобки левую часть запроса с бустом

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-20 15:14:26

0.361
---

  * Использование original\_text в уточнениях колдунщика

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-19 17:25:28

0.360
---

  * Фикс генерации конфига мета-поиска
  * Фикс генерации навигационного буста

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-19 02:16:48

0.359
---

  * Правильная инициализация SearchContext в колдунщиках
  * Убил Backend триггер
  * Правильное использование SearchContext в колдунщике
  * Рефакторинг билдеров запроса

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-18 22:54:28

0.358
---

  * Убираем softness из переколдовки
  * Ненужный отладочный принт

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-17 16:16:31

0.357
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не используем синонимы в поиске по рассылкам

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Не показывать в колдунщике закрытые сервисы

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Прокидываем оригинальный текст в обработку фильтров

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-17 13:50:35

0.356
---

  * Использование оригинального текста для поиска по keywords

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-14 18:06:36

0.355
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Chain -> All
  * Подчистка кода триггеров для визарда
  * Перестаём пользоваться колдунщиками Я.Сервера

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В стади у лекции и события может не быть категории
  * Поправила удаление документов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)


 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-06-14 17:03:50

0.354
---

  * ts для даты проведения лекции

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-06-06 19:17:25

0.353
---

  * ISEARCH-1833 — Переписать индексатор стади
  * Включила платформу для стади

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-06-06 18:17:28

0.352
---

  * Фикс джанго конфига продакшена

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-06-04 18:25:07

0.351
---

  * Хэш для индексации в продакшене

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-06-04 16:18:58

0.350
---

  * Один раз коннектимся к планеру
  * Упростила индексатор планнера
  * Постоянный сниппет планера с направлением
  * Обрезаем слишком длинные кейворды для навигационных источников
  * Временно переключаем поиск по стади на яндекс сервер

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-06-03 14:14:21

0.349
---

  * Хэш для тестинга

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-05-30 18:26:12

0.348
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не падаем когда у поиска нет backend

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Фикс хэша для пуша в платформу в тестинге

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-05-30 17:35:31

0.347
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Новый хост для SaaS в продакшене

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1822 — Использовать ids планнера
  * Фиксы индексации сервисов
  * Поправила поход в планер
  * Поправила язык запросов в навигационном триггере
  * Правильный урл для тестинга планера

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-05-30 16:54:27

0.346
---

  * Приводим к unicode все поля фасетов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-05-20 18:20:39

0.345
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс хеша для intrasearch-dev

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Хэш для intrasearch-dev

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Добавил коментариев в конфиг для SaaS
  * Выдаем только ограниченные поля при запросе лейблов фасетов
  * Рисуем ошибки в xml

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-05-20 17:24:01

0.344
---

  * Фикс аргумента функции

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-05-16 19:54:24

0.343
---

  * Обновил настройки хостов SaaS
  * gen.coroutine. совместимость с tornado 3.0
  * Поменял параметр хождения в WaaS

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-05-16 19:34:23

0.342
---

  * Не прокидываем None как параметр
  * Выводим урл и время срабатывания колдунщика
  * Правило с внешним колдунщиком опционально

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-05-07 13:51:22

0.341
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Удалил isearch.backends

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Пишу ворнинг на 500 этушки
  * ISEARCH-1813 — Сниппеты: первая буква имени отрывается от остального
    слова

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Обновил настройки SaaS
  * WaaS доступен в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-05-06 15:53:49

0.340
---

  * ids -> id при запросе лейблов фасетов
  * Таймаут на соединение в прокси поисков
  * Фикс конфигов статики админки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-26 11:36:40

0.339
---

  * Получение Navigation через storage
  * Сниппеты на стораджах
  * Фасеты на стораджах
  * Апдейт тестов api
  * Ходим во внешний колдунщик
  * Поправил \_\_unicode\_\_ у триггеров

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-24 16:19:56

0.337
---

  * Использование nginx upstream для тестинга и keepalive в поисковых
    прокси

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-22 14:56:10

0.336
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Магическое большое число в запросе с группировками для фасетов
  * Проверка поста этушки на пустоту

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс статики админки при девелопменте
  * clear\_params в базовом классе

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-04-19 17:46:36

0.335
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Поправила удаление документа в платформе

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * 24 воркера в индексаторе вики в тестинге

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-18 17:42:16

0.334
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Выкинуть use\_platform
  * При пуше этушки игнорировать пустые посты

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Дефолтный бекэнд как аргумент
  * Редирект на /searches/ с корня

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-18 14:14:34

0.333
---

  * Перенес подгрузку настроек ISEARCH в defaults

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-16 13:34:18

0.332
---

  * Фикс фильтрации лишних параметров при запросе бекэнда
  * Прокидываем backend для формирования правильного запроса к фасетам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-15 18:24:57

0.331
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1811 - Генерация пассажей только из определенных зон

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Особо "большие" запросы выполняем через POST
  * Индексируем вики только в продакшене

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-04-15 17:28:26

0.330
---

  * Убираем лишние параметры в запросах к бекэндам
  * Фикс админки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-10 15:41:28

0.329
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * При пуше этушки ходить за содержанием поста

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Погасил индексацию Планнера
  * Не коммитим индекс если его нет
  * Рефакторинг раскладки проекта. Всё теперь в питонячих пакетах.

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-04-08 19:09:07

0.328
---

  * В просмотре поисков выводить title
  * Таймаут для реиндекса статистики
  * errata в просмотре поисков

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-04-01 15:20:25

0.327
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1738 - Техническая морда поисков
  * Вертикаль статистики
  * Новый тестовый хост планнера
  * Урл админки
  * Правильное название поиска по статистике

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Избавился от хелпера index\_size

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-04-01 12:47:39

0.326
---

  * Переименовал indexers в sources
  * Подвинул backend/indexers.py -> indexers.py
  * В выдаче над-мета-поиска uri запроса

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-03-27 23:46:48

0.325
---

  * Правильная раскладка nginx конфига админки
  * Убил ненужные куски конфигов nginx
  * фикс make package
  * Фикс rules
  * Удалил doc/
  * Удалил tools/loadlog
  * Убил tools/stat
  * Убил параметр yserver\_version
  * Логируем исключеиня в ручке индексации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-03-26 19:25:39

0.324
---

  * Фикс формирования урла для коллекции
  * Ретраи для SearchTrigger

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-03-20 19:00:15

0.323
---

  * Фикс зависимостей isearch

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-03-15 17:18:34

0.322
---

  * Nginx над Я.Сервер'ами
  * Локальный proxy для поисков
  * Правильное хождение в поисковые бекэнды

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-03-14 19:49:25

0.321
---

  * Убил настройку ISEARCH\_PYMORPHY\_DICT\_PATH
  * Ручка /ping в над-мета-поиске
  * Фикс хостов Вики

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-03-14 14:34:07

0.320
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * mod\_time для стартрека
  * SEARCH-1793 - В сервисах правильная ссылка на команду сервиса
  * Сортировочные атрибуты в статистике
  * ISEARCH-1795 - Индексировать посты
  * Переотправляем документ, если платформа вернула не 200
  * ISEARCH-1810 - Изменить дефолт для фичи variable\_search\_filters

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-02-28 15:04:14

0.319
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1792 - Правильный url для сервисов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1800 - не работает поиск по автопереведенному контенту
  * Директории в /etc/yandex для searches пакета
  * Зависимость от yandex-environment-intranet
  * Зависимость api от django\_yauth
  * Для abovemeta убрал preload и выставил maxrequests=100

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-19 18:22:34

0.318
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1779 - Индекс Статистики
  * Сортировка по атрибуту в запросе к бекенду

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-15 15:48:46

0.317
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Наличие фасетов вынесла в настройки
  * ISEARCH-1790 - добавить тег страницы к индексу wiki
  * ISEARCH-1789 - Считать страницы wiki непустыми по умолчанию

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * 8 воркеров над-мета-поиска
  * Ненужный файл

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-12 13:39:29

0.316
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс хоста тестинга ml'я

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Админка открывается на поисках по умолчанию
  * ISEARCH-1778 - Просмотр колдунщиков в админках сломался

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Декоратор csrf\_exempt для ручки индексации
  * Заглушка для индексатора Этушки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-07 19:54:00

0.315
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1787 - Добавить индексы в ревизии

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1781 - Поднимать вверх рассылки с точным совпадением
    названия

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1788 - Привести в порядок id и url документа
  * Поправила контексты в админке

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-02-07 16:53:38

0.314
---

  * Не рассчитывать на присутствие descriptionHtml в st

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-02-06 18:41:14

0.313
---

  * debug=True для над-мета-поиска
  * ISEARCH-1784 - Не работает content=translated

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-06 18:29:26

0.312
---

  * ISEARCH-1783 - Санитайзить описание
  * ISEARCH-1782 - правильный doc\_url для стартрека

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-02-06 18:19:38

0.311
---

  * Убил все таймауты в над-мета-поиске

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-06 11:33:17

0.310
---

  * Формируем окончательный запрос в дефолтном билдере
  * Создаем директорию для indexers логов даже в пакете поисков

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-05 19:33:35

0.309
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Не всегда ходить за id фасетов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Обработка ситуации, когда у таргета нет бекэнда
  * Возврат endpoint у внешнего поиска

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-05 19:05:39

0.308
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Новый контекст
  * Тесты для api
  * Тесты контекстов
  * ERROR логгинг для тестов над-мета-поиска

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Рефакторинг слоггера

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Уменьшила таймауты баз в настройках mysql

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-02-05 18:22:32

0.307
---

  * Фикс id группы

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-31 18:34:50

0.306
---

  * Дефолтная группа пользователя 962

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-31 17:51:49

0.305
---

  * Апдейт таймаутов
  * Поднял до 24-х воркеров над-мета-поиска

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-31 16:52:03

0.304
---

  * Фикс опечатки в обработке holdreq
  * За группами ходим в staff

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-31 15:25:49

0.303
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1775 - Прицеплять сниппеты к дублям документов
  * Один http клиект на хендлер
  * Поднял число воркеров api до 32

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1710 - Не находятся переговорки
  * В ст забирать комментарии по ручке search

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-01-30 17:39:44

0.302
---

  * Фикс конфига для админки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-28 15:56:54

0.301
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1755 - Убрать индексацию направлений и программ
  * Не падать при таймауте апи st
  * ISEARCH-1772 - Вынести логику формирования урла документа
  * ISEARCH-1754 - Починить поиск с кавычками

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал локальную Sentry
  * Шаблоны страниц ошибок для api
  * Собрал логи Я.Сервера в кучу
  * Прописал второй слейв в продакшене

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-01-28 12:38:56

0.300
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В индекс st добавились компоненты и теги
  * ISEARCH-1711 - Ходить за комментариями тикета в апи стартрека
  * Revert "Получение Navigation через storage"
  * Для всех запросов проставлять relev

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Получение Navigation через storage

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-01-23 16:09:26

0.299
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1751 - убрала контакты из индекса сервисов
  * ISEARCH-1746 - Функции превратить в методы
  * ISEARCH-1747 - slogger сделать атрибутом
  * ISEARCH-1748 - Сделать базовый контекст
  * ISEARCH-1742 - Рефакторинг над-мета-поиска

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Новый индекс должен быть минимум 99% от старого
  * Форматируем финальный вид запроса в рамках RequestBuilder'а
  * ISEARCH-1753 - Сломалась ссылка "ещё" на вертикале Документации

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-01-21 15:42:41

0.298
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Тесты надметапоиска

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1739 - Сделать ContentTrigger принимающий несколько
    паттернов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1750 - не срабатывает колдунщик по запросу tools-dev (в

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-15 17:17:58

0.297
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * По дефолту не менять поисковые фильтры
  * Проверка ответа платформы

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2013-01-11 12:40:19

0.296
---

  * Ненужные конфиги в пакете searches
  * Поправил шаблон генерации yandex.cfg

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-10 16:40:06

0.295
---

  * Фикс postinst скриптов для searches и indexers

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-10 15:57:20

0.294
---

  * Вернул statbox-logrotate для поисковых логов
  * Рефакторинг request\_builders
  * request\_builder для таргета ml
  * Вернул SECRET\_KEY в простые базовые настройки

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2013-01-10 13:16:34

0.293
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1583 - Форма фидбека в поиске не работает

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1727 - Перейти на PyStemmer
  * ISEARCH-1733 - Объединить все *-indexer и *-search пакеты

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-12-28 18:56:14

0.292
---

  * Фикс STATIC\_URL для админки
  * Фикс хоста админки для девелопмента
  * Валидация подсвеченных сниппетов
  * Опция --no-restart при сборке

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-25 20:59:25

0.291
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Считаем количество лет сотрудника

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1723 - Индексация сервисов через API Планировщика

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-19 18:57:14

0.290
---

  * ISEARCH-1720 - Поиск по рассылкам стабильно отдаёт 500 по любым
    запросам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-18 17:54:10

0.289
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Подвинула request\_builder st в настройках
  * ISEARCH-1712 - Поиск по стартреку: не находятся тикеты по номеру
  * Правильный запрос для ранжирования

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-17 17:06:45

0.288
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В запросе для фасетов убирать пагинацию

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-12-14 13:00:56

0.287
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Явно задавать backend в настройках

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-13 19:46:05

0.286
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Проваливаемся в backend=yserver при определении урла

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-13 18:50:58

0.285
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Правильно определяем, показывать ли результаты для исправленного
    запроса

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * +x на manage.py
  * Фикс базовых настроек

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1703 - Рефакторинг выбора поискового бекэнда

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * south и mptt в дефолтных настройках
  * Фикс работы с настройками окружения

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-13 16:23:48

0.284
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Брать русский сниппет, если не нашелся английский

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Поправил регулярку для хоста admin в nginx
  * Ненужные симлинки

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В st передаем поисковые атрибуты как строки
  * Пессимизировать закрые тикеты в ст

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-12-11 19:44:17

0.283
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * добавил в зависимости ujson в isearch
  * fix имени хоста

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-12-07 17:49:37

0.282
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * include listen

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-12-07 17:09:52

0.281
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1692 - сниппеты планировщика

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * забыл в зависимости isearch прописать settings
  * Другой формат логов для админок по просьбе Влада

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-12-07 16:13:22

0.280
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс настроек
  * Правильный урл для индексации на Платформе в тестинге
  * Убрал флаг use\_wiki\_groups\_acl

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1701 - Колдунщики в конфиге для Платформы
  * ISEARCH-1700 - Генерировать конфиг для мета-поиска

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-12-07 13:14:54

0.279
---

  * ISEARCH-1699 - Разделить api и admin в бекэнде

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-12-06 15:39:09

0.278
---

  * Убрал явную транзакцию в индексаторе людей
  * Разделил индексатор людей на makeindex и index\_resource
  * Проверяем что есть телефоны у сотрудника

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-12-04 16:21:46

0.277
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Прописываем все параметры в запросе с группировками
  * Добавить тестовый инстанс платформы
  * ISEARCH-1644 - Унифицировать генерацию xml на основе dict
  * Честный токен для стартрека

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-12-03 14:19:25

0.276
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал django\_intranet\_stuff из зависимости пакета mldescription-
    indexer

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1690 - Генерация обобщенных конфигов
  * isearch config ничего не возвращает
  * Отлавливаем ошибку при удалении newindex
  * В фасетах упорядочивать группы по количеству результатов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-11-28 17:27:07

0.275
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Подвинул код удаления старой директории создаваемого индекса
  * Фикс параметра для запроса очистки индекса
  * Обработка ошибки парсинга страниц каталога

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1679 - Права для стартрека

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс аргумента confdir для команды isearch config

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-11-27 16:00:04

0.274
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Новый TargetDispatcher для определения урла поискового бекэнда
  * Индекс для модели Indexation
  * Фикс прокидывания revisions в контекстах колдунщиков
  * Вернул аргумент user в над-мета-поиск
  * Прокидка внешнего $PYTHONPATH в ./run

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1657 - Пессимизировать в выдаче страницы с пустым телом
  * ISEARCH-1657 - Убрала QueryLanguage из подключаемых в метапоиск
    коллекций
  * ISEARCH-1679 - Обновить индексатор st
  * Учитывать в фасетах доступ
  * При удалении коллекции по-другому берем id ревизии

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-11-23 16:49:33

0.273
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Не всегда ходить за группировками
  * Одна группировка в метапоиске

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-11-16 17:32:39

0.272
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Делаем группировачные атрибуты сами без mkgrouping
  * Убрал emit\_category\_to\_parent
  * Группировочные атрибуты сохраняются на лету
  * Фикс создания группировочных атрибутов. Исправлен парсинг выдачи

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Поменяла атрибуты документа в study

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Функция создания очереди в Роботе
  * Логируем начало и конец обхода каталога в роботе
  * Фикс импорта саб-команд isearch
  * Убрал поле status у колдунщиков
  * Подчистил вьюхи админки
  * Больше не нужен dsindexer.cfg
  * Метод open у бекэнда индексации
  * Нунужный параметр yserver\_version
  * Хелпер cleanup для подчистки ревизий и лога индексации
  * Вызов cleanup в конце reindex

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1669 - Обработка параметров запроса через WTForms
  * ISEARCH-1602 - Выгрузка справочника группировочных атрибутов
  * Более одной группировки можно добавить в apply\_grouping
  * ISEARCH-1606 - Формировать зону search\_filters
  * ISEARCH-1605 - Делать запросы в зону search\_results с группировками
  * Убрала проверку из логгера
  * ISEARCH-1607 - Учитывать фильтры фасетов
  * ISEARCH-1680 - Добавить поле value в таблицу атрибутов
  * ISEARCH-1681 - Флаг facet для таблицы атрибутов
  * ISEARCH-1682 - Добавить фасеты в индексатор study
  * В фасетах использовать внешний id
  * Открываем бекэнд для пустого индекса

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-11-16 13:58:45

0.271
---

  * 10 задач для воркера celery
  * distribute поддерживает опция force
  * Навигационный источник зависит от индекса
  * Базовая модель Artefact
  * Сторадж для артефактов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-11-08 09:57:47

0.270
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1657 - Пессимизировать в выдаче страницы с пустым телом
  * В сниппет wiki добавился is\_empty

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фиксированная длина url у навигационной ссылки
  * Хак старой миграции создания Navigation чтобы можно было делать
    тестовую базу
  * Прототип запускателя тестов
  * Убил устаревшее приложение parallels
  * Рефакторинг бекэнда
  * Перенес ручку /run/ в api

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Флаг для сотрудников и внезних спикеров

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * key\_hash может работать с unicode
  * Фикс урлов api в distribute
  * Правильно формируем опции внутри distribute
  * celery при инициализации может бросить ImportError

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-11-07 17:34:01

0.269
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Правильное определение зоны для plan

 * [knopka](https://staff.yandex-team.ru/knopka)

  * В study использовать сессию
  * Правка конфига stud

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Нет больше no\_revision

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-10-31 17:48:51

0.268
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1660 - Фильтр "по дате" сбрасывается при переходе по
    страницам
  * Убрал поддиректорию conf для конфигов Я.Сервера и подвинул в etc

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Синонимы для сервисов

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-10-30 19:46:06

0.267
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1641 - в сниппете стади в action и action\_category всегда
    отдавать name и url
  * ISEARCH-1656 - Включаем синонимы для вики, док и стади
  * Синонимы - ml, планнер, оборудование, сервисы, invite
  * Группировка в конфиге для study
  * Правка крона для стади

 [Nataliya Kryuchkova](https://staff.yandex-team.ru/knopka@yandex-team.ru) 2012-10-30 18:55:18

0.266
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1641 - добавила breadcrumbs к сниппету стади

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Локальный импорт config

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-29 19:51:29

0.265
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Переход на ревизии для задания kps при индексации

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Правила колдунщика стади на вертикали
  * Не заменять запрос в колдунщике стади

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Автогенерация конфигов индексатора
  * Забытая запятая в setup.py

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-29 18:23:33

0.264
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Индексатор study собирает данные обо всех мероприятиях для лекции
  * В колдунщике study не убивать пятьницу

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Забытый postinst для study-search
  * Индексируем study через Платформу

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-26 00:58:38

0.263
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновил хост ml'я
  * update gitignore

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Привел в порядок параметры в create\_document
  * ISEARCH-1560 - Суррогатный id документов
  * ISEARCH-1596 - Подгрузка ревизий в над-мета-поиске
  * ISEARCH-1649 - Индексировать права доступа к тикету
  * ISEARCH-1645 - Формировать запрос в поиск Вики с новым acl
  * ISEARCH-1560 - Суррогатный id документов

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1642 - Свой индексатор для study
  * Исправила опечатку в вызове fetch\_snippet
  * Не вырезать ссылки из тела вики странички

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Апдейт логики формирования первичных параллельных запрос в над-мета-
    поиске
  * Убрал ненужную копию стаба мета-индекса
  * Соединил всё что касается саджеста в одну директорию
  * Саджест теперь в отдельном репозитории
  * Ненужные таргеты в мейкфайле
  * Ненужный etc/fastcgi
  * Мета-поиск смотрит в один индекс

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1655 - Новый мета-поиск с подмешанным study
  * ISEARCH-1654 - Правила колдунщика study на основной выдаче
  * Правки сниппета study

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал acl\_blacklist
  * Использование acl\_users\_whitelist в Документации
  * Проверка на public=1 в новой acl
  * spcctx=doc для study и st
  * Строим запрос к st с учетом acl
  * Статический список экспериментов
  * Фикс форматирования запроса

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-25 18:17:10

0.262
---

  * ISEARCH-1595 - Выгрузка актуальных ревизий в бекэнде
  * Убил *.init.d скрипты
  * ISEARCH-1608 - Обновить bootstrap
  * ISEARCH-1643 - [object Object] в колдунщике переговорок
  * ISEARCH-1418 - 500 на поиске по интранету во время учений в Фольга-A
  * ISEARCH-1636 - Получать группы пользователей
  * ISEARCH-1645 - Формировать запрос в поиск Вики с новым acl
  * ISEARCH-1646 - Обновить индексатор вики для нового acl

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-16 11:43:34

0.261
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Добавила 404 к допустимым кодам ответа
  * ISEARCH-1630 - Убрала вес у description, добавила его в сниппет

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Не нужны больше DocProperty и Groups в конфигах Документации
  * mtime и public не нужны как группировочные атрибуты
  * Убрал документарные атрибуты для doc
  * compile\_data больше не нужен
  * Больше не нужны документарные атрибуты для wiki
  * ISEARCH-1603 - Увеличить число воркеров для бекэнда
  * ISEARCH-1637 - Убрать дополнительные ссылки из навигационного
    источника
  * ISEARCH-1418 - 500 на поиске по интранету во время учений в Фольга-A

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-12 07:27:27

0.260
---

  * Разбиение acl полей по пробелу
  * Убрал группировочный атрибут cluster\_one
  * Фикс мейк-файла

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-09 23:42:22

0.259
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1599 - Обновить индексатор сервисов
  * Удалил проперти в оборуовании
  * Удалил проперти в переговорках
  * ISEARCH-1601 - Обновить индексатор планировщика

 * [knopka](https://staff.yandex-team.ru/knopka)

  * При поиске сниппета брать url из properties

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * убрал проперти из индексатора колдунщика рассылок
  * fix неправильного поля для роли

 * [knopka](https://staff.yandex-team.ru/knopka)

  * При добавлении сниппета брать url из properties
  * ISEARCH-1600 Обновить индексатор документации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Всё-таки атрибут doc\_grou\_grp для группировок нужен

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновление индексатора сервисов
  * забытая ссылка на вики страницу
  * переделал список контактов сервиса
  * Добавил нормализацию данных в контактах

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Правильно санитайзим html
  * unescape для поля description
  * Теперь xnl.cfg у документации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-09 11:41:45

0.258
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс вывода в лог выполненной команды через run
  * Индекс для GroupAttr

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * update .gitignore
  * change request timeout for errata
  * Убрал треды для парсинга xml'я
  * ISEARCH-1597 - Обновить индексатор переговорок
  * ISEARCH-1598 - Обновить индексатор оборудования
  * ISEARCH-1613 - Русские отчества в результатах поиска в англ.
    интерфейсе

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс фильтрации урлов в роботе
  * Чистка конфига индексатора wiki
  * Фикс добавление body вики-страницы в индекс
  * Фикс индексации прав доступа в wiki
  * Фикс поиска по кластеру wiki
  * Базовый санитайзинг страниц вики

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Увеличил таймаут и добавил ретраи для поиска по планировщику
  * Fix индексатора планировщика

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Ненужная обработка параметра backend
  * Индексация Документации на Платформе в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-10-02 16:13:34

0.257
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Вернул проперти в mldescription
  * Создание зон в индексаторе mldescription по-новому

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-09-21 16:40:59

0.256
---

  * Фикс вызова rsync. Эскейпинг символов ':'
  * Закомментировал сохранение группировочных атрибутов в базе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-09-19 14:31:41

0.255
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1594 - Обновить индексатор описания рассылок

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1504 - Инстанс Платформы в продакшене
  * Не нужен finally c return в index. Он скрывает ошибки
  * Определение окружения в ./run
  * Подавил UserWarning в pymongo.connection
  * Рефакторинг запуска консольных утилит через sarge

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-09-19 11:13:44

0.254
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1581 - Инициализировать SearchTrigger именем индекса

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Рефакторинг close() логики бекэнда индексации
  * Фикс наследования моделей
  * Фикс возврата контекста из index
  * Модель и создание ревизии индексов
  * Убрал import settings обратно в функцию
  * Ходим в мастер тестовый вики в девелопменте и тестинге
  * Подкручивает auto increment счетчик ревизий до 1000
  * Прототип индексатора и поиска по StarTrek
  * Таргет deploy-local

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1586 - слишком много данных в логах индексации
  * ISEARCH-1510 - Значения группировочных атрибутов в базе

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1545 - Переформирование документа вики

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не индексируем id подразделения

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Отключение создания ревизий по требованию
  * Апдейт debian/control для >=2.6 питона
  * Отдельный пакеты для конфигов и воркеров celery
  * Убрал зависимость от statbox-logrotate
  * Фикс завивисимости plan-search
  * Конфиг html парсера для wiki не нужен

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-09-18 08:31:03

0.253
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил время ответов сниппетов в логи
  * ISEARCH-1577 - Подгрузка c2n после regroup
  * ISEARCH-1584 - При поиске по номеру автомобиля показываются лишние
    данные
  * Параметр поиска по документу spcctx: doc

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс индексирования группировочных атрибутов в Я.Сервере
  * Параметр backend для разделения Я.Сервер/Платформа в индексации и
    поиске
  * Синхронизируем группы, если есть контекст
  * Help-текст для команд isearch
  * Убил уже ненужную backend команду
  * Отрефакторил импорты
  * Убрал почти все атрибуты из конфига парсера Документации
  * Обработка ситуации когда в c2n нет каких-то значений
  * Стрипинг stdout/stderr при записи в лог
  * Фикс работы с именем группировочного атрибута
  * Отбрасываем пустые атрибуты

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-09-13 11:33:31

0.252
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Убираем служебные символы из запроса

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал временно выдачу metawizard из над-мета-поиска

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-09-05 16:49:00

0.251
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Перевод конфига settings.yaml на confucius
  * Перевел robot.yaml на confucius
  * Единое поле log в Indexation
  * Убрал ненужный echo
  * Использование logging для записи лога команд isearch
  * Интеграция Celery
  * Погасил предупреждение pymongo "must provide a username and password
    to authenticate"
  * Хост planner.tools.yandex.net для продакшена
  * ISEARCH-1576 - Перенести стадию regroup внутрь index
  * Апдейт логинга в commit
  * Переименовал backend в request\_builder

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1568 - В выдаче показывается не тот офис
  * ISEARCH-1562 - Прокидывать выдачу мета-колдунщика во фронтэнд
  * Не правильно выводились имена людей в сниппете

 * [knopka](https://staff.yandex-team.ru/knopka)

  * Поменяла названия новых опций в index/reindex
  * Добавить --force в reindex

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-09-05 15:03:37

0.250
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил роль человека в сниппет сервиса
  * Если текст пустой сразу выдаем ответ
  * ISEARCH-1567 - оставить в лидерах сервиса только одного, остальных в
    команду
  * добавил в сниппет людей office\_id
  * ISEARCH-1566 - Атрибуты в индексаторе people

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1547 - ограничение числа документов при индексации
  * ISEARCH-1569 - Научить robot читать странички с диска

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Новый хост у Планировщика в тестинге

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-31 18:25:56

0.249
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Поправил хост для wiki
  * ISEARCH-1553 - Ограничить одним результатом выдачу колдунщика
    Сервисов
  * Убрал ненужный менеджер у модели Feature
  * Навигационный триггер в новом колдунщике платформ
  * Заменил урлы планировщика

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Подвинул setup\_environ в isearch.utils
  * intrasearch\_wsgi -> wsgi
  * Более хитрый setup\_environ
  * Строгий settings.py

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-30 14:53:38

0.248
---

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1543 - использовать lxml.html или html5lib по выбору

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1559 - Атрибут doc\_url у всех документов

 * [knopka](https://staff.yandex-team.ru/knopka)

  * ISEARCH-1557 - ссылка на оборудование из колдунщика

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал Mapping из конфига
  * Убрал has\_wizard из конфига

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-08-28 12:03:05

0.247
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Обертка над DSDocument

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * unique\_together для ключа и языка в Snippet
  * Ходим в тестинге в реплику вики

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-27 15:02:45

0.246-1
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Непонятное лишнее действие в миграциях

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-27 13:15:47

0.246
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * баг при генерации номеров телефонов для индексации
  * ISEARCH-1524 - Админка редактирования фич
  * ISEARCH-1550 - Дополнительно складывать в индекс названия
    переговорок без цифр
  * ISEARCH-1521 - Ручка выгрузки фич в бекэнде
  * ISEARCH-1522 - Подгрузка фич и их использование в над-мета-поиске
  * ISEARCH-1554 - Включение колдунщика сервисов
  * ISEARCH-1555 - Включение поиска по Платформе
  * Общее время работы надметапоиска

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-27 11:51:38

0.245
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1493 - Сниппет с данными о Сервисах
  * переходим на sha1 от урла в качестве идентификатора сниппета
  * ISEARCH-1461 - Показывать колдунщик проектов, только если есть
    совпадение в названиях проектов
  * ISEARCH-1494 - Подключаем колдунщик Сервисов
  * Не добавляем в сниппет пустые значения если есть данные для другого
    языка

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Дополнительный аргумент при удалении всех документов в Платформе
  * Убрал doc\_source\_grp атрибут
  * Дефолтное значение, если xpath ничего не вернул
  * Индексация Документации на Платформе в тестинге опять включена

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-21 16:18:24

0.244
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Механизм очистки индекса на Платформе - isearch index --clear
  * Убрал вариативность от окружения конфигов doc и wiki

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1512 - сломалась индексация проектов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Конфиги бекэнда в /etc

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * обновил readme

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал индексаю Документации на Платформе в тестинге
  * Подвинул модули в api1

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-08-15 15:34:46

0.243
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * doc\_source указывается глобально

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * fix 500 с mlsearch в надметапоиске
  * Не ходим за сниппетами если нет ни одного ключа
  * добавил в сниппет людей workJabber
  * добавил поисковые атриббуты в язык запросов для людей

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-13 18:20:00

0.242
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * патчим mkgrouping-2010.06
  * обновил control
  * ISEARCH-1495 - Сервис раздачи сниппетов
  * ISEARCH-1500 - Подцепление сниппетов в над-мета-поиске
  * выпилил метапакет

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * doc\_source - дефолтный атрибут
  * Убил пакет samples

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-13 16:28:14

0.241
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1511 - неправильный урл в проксике календаря

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Нет больше кастомной переиндексации
  * Ненужный аргумент --repliaa

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1516 - Url документа как ключ сниппета

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * вызов update\_services\_lite по крону
  * Пробел после оператора |

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-08-09 13:29:46

0.240
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1317 - Избавиться от репортов Я.Сервера
  * Фикс раскладки empty-dsindexer.cfg
  * Использование isearch index для генерации начального пустого индекса
  * Удаление старой директории newindex перед началом индексации
  * Дефолтные атрибуты документов
  * Робот как класс
  * Метод backend.create\_document
  * Запуск reindex в определенных окружениях
  * Подсчет проиндексированных документов самим бекэндом
  * Подключаем модель Group
  * Правильное получение имени индекса в индексаторе Планировщика
  * ISEARCH-1484 - Индексация Документации на Платформе
  * Оператор | вместо ||
  * Общая ссылка на индекс для моделей
  * Убрал WorkDir из конфигов индексаторов
  * Избавился от empty-dsindexer.cfg
  * ISEARCH-1484 - Индексация Документации на Платформе
  * Ловим ошибку при коммите пустого индекса
  * фикс опечатки в postinst
  * Дополнительное doc\_index свойство для всех документов

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1490 - Сериализация сниппетов
  * Починил индексацию людей
  * девелоперский сервер торнады с перезагрузкой сорцов
  * ISEARCH-1293 - Индексация сервисов через django\_services\_lite

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-08-08 13:23:58

0.239
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1471 - неверная логика работы колдунщика по именам рассылок

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1400 - Колдунщик рассылок не срабатывает по запросу вида
    [tools-dev@]

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-07-25 16:51:23

0.238
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не передаем лишние аттрибуты no\_jabber, no\_errata

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Апдейт regroup хелпера
  * Убил команды startindex и finishindex
  * ISEARCH-1470 - Перестало ловиться аварийное завершение индексаций в
    программе isearch

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-07-24 18:31:23

0.237
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1461 - Показывать колдунщик проектов, только если есть
    совпадение в названиях проектов
  * Фикс Endpoint.url()

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1465 - сломался проксик занятости переговорок
  * Баг в генерации саджеста
  * Не ходить за данными по планировщику в балансер

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-07-23 13:00:34

0.236
---

  * Апдейт isearch distribute
  * ISEARCH-1461 - Показывать колдунщик проектов, только если есть
    совпадение в названиях проектов
  * ISEARCH-1464 - Учитывать имена предков (с весом LOW) при поиске
    проектов в планировщике
  * Не индексируем родителя проекта первого уровня

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-19 11:58:02

0.235
---

  * Правильно получаем контент от API ручек в индексаторе Планировщика
  * 80 порт бекэнда поиска по Рассылкам в продакшене

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-17 17:37:53

0.234
---

  * ISEARCH-1450 - Не искать программы и проекты входящие в направление
    [удалённые]

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-17 15:19:46

0.233
---

  * Использование center.prestable в тестинге и девелопменте
  * ISEARCH-1445 - Бывшие сотрудники не группируются в отдельную группу
    на выдаче
  * Кладем в индекс число родителей у проекта
  * Фикс вывода полей уволенных сотрудников
  * ISEARCH-1435 - Показывать домашний номер телефона в сниппете, если в
    нём есть вхождение поискового запроса

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-17 12:34:43

0.232
---

  * Правильный pop у QueryDict

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-12 19:44:59

0.231
---

  * ISEARCH-1439 - Не обновляются данные саджеста по людям
  * ISEARCH-1451 - Генерировать урлы сущностей в зависимости от
    окружения
  * ISEARCH-1446 - Недостаточно данных в выдаче в поиске по проектам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-12 18:09:32

0.230
---

  * robot больше не хелперная команда
  * Убрал index команду из бекэнда
  * Единое место создания бекэнда индексации
  * Правильные эндпоинты Вики и Документации для над-мета-поиска
  * ISEARCH-1446 - Недостаточно данных в выдаче в поиске по проектам
  * убил tools/search\_tools
  * Правильная работа с QueryDict

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-11 15:39:51

0.229
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1441 - Не работает поиск людей в сервисах по ключевым словам
    (тегам)

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Кастомные пути к индексами и конфигам в хелперных скриптах
  * Фикс отметки выполненного задания в роботе
  * Фикс урла до мета-поиска в админке
  * ISEARCH-1425 - Поднять тестовую/разработческую ручку для поиска по
  * Убил приложение tuning
  * doc\_source для индексатора Планировщика

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-07-09 18:51:51

0.228
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * убрал ворнинги в индексаторе людей
  * Неправильно назвал поистинстал :)
  * Ден как синоним денис'а
  * parent\_name в поиске по планировщику
  * Программа и направление
  * Логгирование писем
  * Колдунщик проектов
  * Подключаем планировщик в метаколдунщик
  * Починил поиск по планировщику
  * По новому индексируем номера телефонов
  * Улучшаем качество поиска по описаниям рассылок
  * Убрал лишнего тимсона из файла синонимов
  * Фикс номера авто в поиске по людям
  * Маленький рефакторинг прокси людей
  * Больше не передаем параметры no\_errata и no\_jabber за ненадобностью
  * Баг типизации
  * ISEARCH-1440 - баги с паджинацией

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал ненужный код из прокси людей
  * Абстрактный бекэнд индексации
  * Фикс импорта моделей из индексатора
  * Фикс опечатки
  * Единый конфиг бекэндов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-06-29 17:43:34

0.227
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1420 - "None" вместо номера офисного телефона
  * Улучшаем качество поиска по людям

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-06-21 13:45:23

0.226
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Прокидываем суффикс а так же dry\_run в makeindex
  * ISEARCH-1426 - 500 от прокси людей
  * Неправильный конфиг подсовывался в случае наличия суффикса
  * Баг в скрипте считающем количество проиндексированных документов
  * Правильный каталог для файла группировок
  * ISEARCH-1423 - Поиск по Планировщику
  * ISEARCH-1421 - Не показывается дерево структурных подразделений
  * ISEARCH-1419 - Два мобильных телефона в выдаче склеиваются в один
  * python-dateutil в control
  * Правка крона для планировщика

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-06-20 14:37:56

0.225
---

  * Фикс поддержки JSONP в саджесте

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-06-15 14:49:54

0.224
---

  * Саджест в opensearch

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-06-14 17:33:45

0.223
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Правка словаря расширений
  * Добавил в сниппет людей номера телефонов

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-06-08 18:04:06

0.222
---

  * Рефакторинг бекэнда саджеста

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-06-07 12:04:29

0.221
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Мелкие баги в поиске людей
  * Поддерживаем свойство "бронируемости" переговорки. Фильтруем
    удаленные.
  * Меняем урл переговорки
  * ISEARCH-1393 - Находить переговорки по номеру конференц-связи

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1411 - Переключиться на продакшн-ручку в поиске рассылок
  * ISEARCH-1350 - Портирование бекэнда саджеста на tornado
  * Перенес isearch-* хелперы в пакет isearch
  * Избавился от команды commitindex

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-06-06 16:30:35

0.220
---

  * Фикс владельца каталога с индексами Документации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-29 18:47:48

0.219
---

  * Запуск индексатора Документации от www-data

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-29 18:12:52

0.218
---

  * Убрал ненужные коллекции
  * Выделение абстрактного робота
  * Индексатор документации на базе своего робота

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-29 17:09:45

0.217
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Поиск по номеру авто ищет и с латинскими и с русскими буквами
  * ISEARCH-1394 - Добавить в индекс поиска людей поля "рассылки" и
    "вики" для подразделения
  * ISEARCH-1397 - 500 от поиска людей
  * Добавил в поисковые логи количество найденных документов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Число воркеров роботов в продакшене поднял до 12
  * Прокидка кода возврата индексатора Вики
  * Правильные урлы базовых поисков с автопереведенным контентом
  * Фикс шаблона админки поисков

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-29 12:27:57

0.216-1
---

  * Пересборка

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-23 17:56:42

0.216
---

  * Правильно указываем коллекцию автопереведенной вики
  * Апдейт шаблона дашборда поисков
  * Отключил колдунщики для en коллекции вики

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-23 16:36:46

0.215
---

  * Включение wiki-en в cron'е
  * Включение en коллекции в meta поиске

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-22 11:04:50

0.214
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1391 - 500-ки по некоторым запросам

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1391 - 500-ки по некоторым запросам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-22 08:21:06

0.213
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1388 - Включить колдунщик переговорок на запросы без слова
    "переговорка"
  * Fix поиска по переговоркам

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Статус new для нового лога индексации
  * Отключаем из мета-поиска колдунщик Syntax2
  * Убрал ненужнаые зависимости индексатора людей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-21 17:34:17

0.212
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Универсальный Run обработчик
  * Расширенный формат задания таймаута лока для isearch-reindex
  * Помечаем тасты сделанными внутри робота

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Использовать сислог вместо файлхендлера, для поисковых логов

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Проверка что основная выдача тоже получина над-мета-поиском
  * ISEARCH-1385 - Новая поисковая ручка для поиска по рассылкам
  * Поднял число воркеров для робота в продакшене до 6
  * Правильно считаем число документов в новом индексе

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-17 15:51:13

0.211
---

  * Учет суффикса в API ручки commit
  * Правильный индекс для archive коллекции документации
  * Правильное выставление exit code в trap блоке
  * Фикс конфига архивных коллекций
  * Обстракция ответов от поисковых бекэндов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-11 17:06:15

0.210
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Больше не пытаемся получить данные из удаленного индекса
  * ISEARCH-1237 - Переделать индексацию Документации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Для плохого индекса число документов 0
  * Фикс distribute скрипта
  * Использование trap для удаления ременных директорий

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-03 16:36:38

0.209
---

  * Берем число документов у newindex

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-02 21:51:12

0.208
---

  * Индексатор services для 2.6 питона
  * Переиндексируем оборудование каждые 15 минут
  * Фикс isearch-distribute

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-02 21:25:21

0.207
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Правки в скрипте переиндексации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Настройка директорий индексов и логов для индексаторов
  * Маленький фикс isearch-reindex

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-02 20:09:15

0.206
---

  * Использование pytils вместо uniconv в индексаторе людей
  * ISEARCH-1235 - Зависимости yandex-tools-intrasearch-suggest-indexer

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-02 17:42:02

0.205
---

  * Убрал работу с /var/cache

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-02 16:49:33

0.204
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убрал код фронтэнда

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Удалил лишнее из gitignore
  * Отрефакторил запускалку перенидексаций. Теперь с количеством
    документов!
  * Не считать количество проиндексированных документов при неудачной
    индексации

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * dh\_auto\_install/clean для сборки isearch
  * ISEARCH-1315 - Переписать isearch-* команды на python
  * Убрал зависимость от yandex-init у индексаторов
  * ISEARCH-1321 - Конфиг для демона rsync
  * ISEARCH-1322 - Скрипт isearch-distribute
  * ISEARCH-1324 - Обновить инфраструктуру для индексации на генераторах

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-05-02 14:54:23

0.203-1
---

  * Hotfix сборки статики

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-04-25 13:42:21

0.203
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Сохраним реферер в логгере
  * ADMIN-4407 - Выносить поисковые логи в отдельное место

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1150 - Придумать решение по сборке js и css на лету для
    разработки

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-04-24 12:58:30

0.202
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Добавил хостнейм в админочку просмотра логов индексации
  * если нет имени переговорки пытаемся записать в заголовок
    альтернативное имя

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1088 - Поиск по кластеру только внутри вертикали Вики

 * [Rustem Halilov](https://staff.yandex-team.ru/Rustem%20Halilov)

  * Двойной ключик у сниппета вики

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Удаляем папку оставшуюся от неудачной индексации
  * ISEARCH-1379 - Неправильное исправление опечатки и
  * Считаем время ответа

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * Поправил исполнение bemhtml.js в node.js рантайме
  * ISEARCH-1375 - Неправильная ссылка на рассылку из сниппета сервиса
  * ISEARCH-1380 - Деградация фронтенда в случае большого количества
    ошибок от поисков
  * Убрал wikisearch и docsearch из pages-desktop

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1278 - Поменять url для забора данных из Танкера

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1183 - Статическая вёрстка блоков /mlsearch? в БЭМ

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-04-20 15:14:40

0.201
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Обновил в зависимостях npm-request
  * ISEARCH-1108 - Синонимы на метапоиске

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-04-06 15:57:33

0.200
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Таймаут на получение данных от опечаточника
  * Админка для просмотра логов индексации
  * ISEARCH-1371 - Бывшие сотрудники не группируются в отдельную группу
    на выдаче
  * Правильная ссылка на стафф для бывших сотрудников
  * Вернул колдунщики в поиске людей

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * баг в колдунщике переговорок, из-за которого для некоторых
    переговорок отображалось Вместимость: None

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-04-05 17:45:55

0.199
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Не индексируем переговорки не зарегистрированные в exchange'е
  * Права на создание логов у бэкенда

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-04-02 16:59:04

0.198-1
---

  * hotfix индексации людей

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-03-31 12:09:02

0.198
---

 * [Rustem Halilov](https://staff.yandex-team.ru/Rustem%20Halilov)

  * ISEARCH-1351 - Битые ссылки на документацию из выдачи
  * ISEARCH-735 - Фича: сделать название источника в крошках кликабельным и вести с
    него на сервис
  * ISEARCH-1352 - Показывать в верстке wiki как отдельную вертикаль
  * Удалил b-ico, заменил его на b-icon. Заморозил лего на ревизии 30250

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1362 - Использовать библиотеку request для хождения по http
  * увеличил таймаут до 20 сек при запросу в над-мета-поиск
  * небольшой рефакторинг doRequestSearch
  * ISEARCH-1367 - Ломается вёрстка на 404-й странице
  * ISEARCH-1368 - Перейти на новый формат ссылок на подразделения
    стаффа
  * ISEARCH-1214 - Написать priv.js для блока b-wizard-meeting-rooms
    (колдунщик переговорок)
  * ISEARCH-1195 - Динамическое получение информации о занятости
    переговорок (колдунщик переговорок)

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Зависимость пакета www2 от npm-request

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1364 - Поддержать mlsearch в мета-колдунщике
  * Добавил в вывод яндекс сервера количество стульев в переговорке
  * Убрал лишний QueryLanguage
  * Проксируем в nginx'е ручку проксирования для календаря *\_*
  * ISEARCH-1361 - Подробный лог запросов над-мета-поиска
  * ISEARCH-1360 - Находить людей в подраделении по айдишнику
    подразделения.

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-03-30 23:53:59

0.197
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Правильная TimeZone'а в Sentry

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс обработки пустого запроса
  * Вызов updatecenter с опцией --noplock
  * Таймаут в 20 секунд у getHttp

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-21 15:22:01

0.196
---

  * Единообразная проверка результата запросов в над-мета-поиске
  * Заменил пару write/finish на просто finish при отдаче ответа
  * Рефакторинг работы с бекэндом в над-мета-поиске

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-21 10:42:54

0.195
---

  * Корневые шаблоны попадают в пакет
  * Зависимость от npm-async
  * Проверяем статус код ответа опечаточника

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-20 19:39:32

0.194
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1353 - ложное срабатывание колдунщика рассылок
  * Hotfix временно закомментировал, англоязычную коллекцию метапоиска

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * рефакторинг добавления дополнительных параметров во views

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-03-20 14:22:14

0.193
---

 * [Rustem Halilov](https://staff.yandex-team.ru/Rustem%20Halilov)

  * ISEARCH-1334 - Не совсем правильно работает поиск людей из Вики.
  * ISEARCH-1341 - Увеличить ширину блока с колдунщиком людей
  * ISEARCH-1342 - Сообщения об исправлении неправильной раскладки в запросе

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1323 - Ручка в бекэнде, которая делает commit и restart
  * Отключаем дебаг на продакшене
  * ISEARCH-1087 - Выделить wiki в отдельную вертикаль
  * Fix неправильно поставленной скобочки в ручке для календаря

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1331 - Перейти на библиотеку async.js
  * Рефакторинг controller.js

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1342 - Сообщения об исправлении неправильной раскладки в запросе
  * Апдейт isearch-* скриптов. Больше логики на откуп isearch-reindex
  * Почистил код репорта документации
  * Текстовые логи фронтенда
  * Убрал кеш запросов на мета-поиске

 [Nikita Zubkov (Hello World!)](https://staff.yandex-team.ru/zubchick@yandex-team.ru) 2012-03-19 17:24:48

0.192
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Маленькое улучшение в логировании надметапоиска
  * Не слать письма об ошибках от sentry в инбокс
  * ISEARCH-53 - Научиться находить рассылки с префисом ya*
  * Разные емейлы сентри в тестинге и продакшене

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1335 - Вернуть счетчик метрики на страницы поиска
  * Настроил отдачу лего с yandex.st
  * ISEARCH-1333 - Перевести плейсхолдер в строке поиска
  * ISEARCH-1338 - Разобраться с lego.init
  * ISEARCH-1336 - Сделать возможным использование общих блоков на всех
    страницах

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1344 - Прокси-ручка с данными о занятости переговорок

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1346 - Не падать когда мета-поиск не вернул ответ

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-15 17:24:52

0.191
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Убил папку quality
  * Переключение не search домен

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1330 - Рефакторинг page.js для более гибкого использования

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-13 19:12:40

0.190
---

 * [Rustem Halilov](https://staff.yandex-team.ru/Rustem%20Halilov)

  * ISEARCH-1306 - Непереведённые сообщения о редиректах
  * ISEARCH-1316 - Пустые строки в выдаче
  * ISEARCH-1307 - Не делать серым контрол включения поиска по
    переведённому контенту
  * ISEARCH-1325 - Сломалась страница ошибок
  * ISEARCH-1328 - Закрасить переключалку поиска по автопереведенному
    контенту
  * ISEARCH-1327 - Использовать поле языка интерфейса из ЧЯ

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * закомментировал индексацию автопереведенной вики

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-12 20:55:50

0.189
---

  * 8 воркеров только в тестинге и деве у робота Вики. В продакшене 4
  * Настройка логинга для робота Вики
  * Подвинул время начала индексации автопереведенной Вики на 2 часа
  * Закомментировал все FieldTrigger в правилах колдунщиков
  * Ретраи в прокси поиска людей

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-11 19:41:16

0.188
---

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1294 - Не работает звонилка на странице поиска

 * [Rustem Halilov](https://staff.yandex-team.ru/Rustem%20Halilov)

  * ISEARCH-1310 - Передача get параметров с ссылки 'Назад'

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Интеграция централизованного логинга через winston
  * Убил bem-proxy
  * Отключил валидацию моделей в некоторых командах
  * Ненужный код в репортах
  * Ретраи при заборе урлов индексатором Вики
  * ISEARCH-1278 - Поменять url для забора данных из Танкера

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-11 01:01:46

0.187
---

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1312 - Ошибка 500 при запросе [3516]
  * Добавил к логам запрос, чтобы потом было понятно, на каких запросах
    падаем
  * убрал ненужную функцию objToString

 * [Rustem Halilov](https://staff.yandex-team.ru/Rustem%20Halilov)

  * ISEARCH-1304 - Непереведённый блок ещё в селекторе вертикалей

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Fix индексации телефонов

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-07 15:57:12

0.186
---

  * Фикс opensearch.xml
  * Не удаляем корные txt файлы из www при сборке
  * ISEARCH-1313 - В продакшне ссылки на вики ведут на
    wiki01d.tools.yandex.net
  * ISEARCH-1314 - Уменьшить число воркеров индексатора Вики в
    продакшене
  * ISEARCH-1311 - Не работает поиск по номеру телефона
  * Ненужная директива конфига
  * Правильная логика остановки робота индексатора Wiki

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-07 02:06:35

0.185
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1052 - Поиск телефонов без разделителей

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * ISEARCH-1309 - http статусы страниц ошибок

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Фикс nginx конфига
  * ISEARCH-1283 - Колдунщик рассылок срабатывает по совпадению в
    описаниирассылки и без ключевого слова
  * Увеличил время оживания очередей до 10 в роботе Вики

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-06 18:39:09

0.184
---

 * [maxcold](https://staff.yandex-team.ru/maxcold)

  * закоментил css с несуществующими картинками

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Правильная обработка пустого запроса
  * Фикс регулярки хоста search2 для nginx
  * ISEARCH-1283 - Колдунщик рассылок срабатывает по совпадению в
    описании рассылки и без ключевого слова
  * Индексация обычной Вики каждые 4 часа
  * Sentry раздаёт свою статику сама
  * Фикс зависимости от python-yserver

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-06 15:54:17

0.183
---

  * ISEARCH-1140 - Новый фронтенд внутреннего поиска

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-05 17:04:03

0.182
---

  * Энкодим дополнительные параметры в utf-8
  * ISEARCH-1298 - Базовый робот для вики
  * ISEARCH-1295 - Нерелевантные результаты поиска по запросу "что-то там"

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-03-05 03:33:28

0.181
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * убрал www/i18n из git'а

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Fix настроек sentry
  * Fix отображения статуса индексации в админке

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Использование flock вместо dlock для индексатора вики
  * Явная зависимость от python-raven

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-29 18:32:16

0.180
---

  * Фикс использования dlock

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-29 14:29:55

0.179
---

  * Выставление владельца на /var/run/ для sentry
  * Использование dlock для индексатора wiki

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-29 14:23:22

0.178
---

  * Фикс настроек Sentry в тестинге и продакшене
  * Включение хендлеров sentry по-дефолту
  * Более мягкий фильтр следования для автопереведенного индексатора

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-28 20:46:33

0.177
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Избавился от Zabbix

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1284 - Слишком "мягкий" поиск рассылок
  * ISEARCH-1287 - Добавить названия сервисов в поиск рассылок

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * Апдейт правил индексирования Wiki
  * Настройка уровня логирования индексатора Wiki и Doc в зависимости от
    окружения
  * ISEARCH-1276 - Колдунщик оборудования срабатывает по совпадению
    вописании единицы оборудования и без ключевого слова
  * ISEARCH-1283 - Колдунщик рассылок срабатывает по совпадению в
    описаниирассылки и без ключевого слова
  * ISEARCH-1164 - Подключить колдунщик рассылок на всех вертикалях
  * ISEARCH-1282 - Если нет английского имени и фамилии - выводится
    пустой сниппет
  * Не забираем Jabber статусы в бекэнде
  * Правильные имена индексов при диагностики коммита
  * Апдейт скриптов идексирования. Раздельное индексирование разных
    типов Вики

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-28 11:40:47

0.176.bemhtml
---

  * Сборка нового bemhtml бранча

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-24 11:50:59

0.176
---

  * Вывод времени выполнения запроса для каждой зоны и content-type'а
  * Проверка в проксике людей что джаббер-статусы отдались с 200
  * Дефолтные шаблоны 500 и 404 для бекэнда
  * ISEARCH-1246 - Поднимаем Sentry
  * ISEARCH-1216 - priv.js для колдуншика по рассылкам

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-24 11:36:35

0.175.bemhtml
---

  * Сборка нового bemhtml бранча

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-21 16:33:05

0.175
---

  * Использоварние MergeDict для настроек урлов поиска
  * ISEARCH-871 - Поиск по автопереведённой Вики
  * ISEARCH-1233 - id и from\_stuff\_id класть в атрибуты документов
  * ISEARCH-1244 - Запретить Яндекс.Серверу ходить по вики-страницам
    садресом, заканчивающимся на /.edit
  * Поменял девелоперский хост документации на teux.doc01.dev

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-21 10:40:03

0.174.bemhtml
---

  * Сборка нового bemhtml

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-17 22:12:06

0.174
---

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * Фикс верстки админки отображения поисков
  * Добавил новые зависимости в метапакет

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1246 - Поднимаем Sentry

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-17 21:47:26

0.173.bemhtml
---

  * Cборка нового bemhtml фронтэнда

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-15 18:58:52

0.173
---

  * Фикс создания лога индексации

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-15 19:47:08

0.172
---

 * [Alex Koshelev](https://staff.yandex-team.ru/Alex%20Koshelev)

  * ISEARCH-1243 - Добавить проверку на пустой индекс

 * [Nikita Zubkov](https://staff.yandex-team.ru/Nikita%20Zubkov)

  * ISEARCH-1186 - Лог индексации
  * Вебморда для просмотра данных об индексациях

 [Alex Koshelev](https://staff.yandex-team.ru/alexkoshelev@yandex-team.ru) 2012-02-15 18:44:15

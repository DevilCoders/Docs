2.11
----

* [max-tyulin](http://staff/max-tyulin)

 * WIKI-15898: Не энкодим + в хеше урл

Заодно обновил образ ubuntu до 20,04  [ https://a.yandex-team.ru/arc/commit/9478960 ]

* [maratik](http://staff/maratik)

 * ARCANUM-5496: WIKI migration  [ https://a.yandex-team.ru/arc/commit/9281158 ]

* [dsamuylov](http://staff/dsamuylov)

 * ARCANUM-5510 prepare migration from .devexp.json to a.yaml (intranet)  [ https://a.yandex-team.ru/arc/commit/9231012 ]

[max-tyulin](http://staff/max-tyulin) 2022-05-20 12:01:34+03:00

2.10
----

 * Пересборка

[elisei](http://staff/elisei) 2021-09-02 23:29:50+03:00

2.9
---

* [elisei](http://staff/elisei)

 * WIKI-15282: добавил в исключения символы ! и /  [ https://a.yandex-team.ru/arc/commit/8576216 ]

* [exprmntr](http://staff/exprmntr)

 * DEVTOOLS-7781 - remove NO_LINT()

[elisei](http://staff/elisei) 2021-08-31 14:15:55+03:00

2.8
---

* [max-tyulin](http://staff/max-tyulin)

 * WIKI-14755: Не энкодим "=" в параметрах  [ https://a.yandex-team.ru/arc/commit/7635262 ]

* [elisei](http://staff/elisei)

 * Удалил устаревшую настройку про кулауд                                             [ https://a.yandex-team.ru/arc/commit/7571174 ]
 * PR from branch users/elisei/readme_change

changed deploy target: Qloud -> Deploy  [ https://a.yandex-team.ru/arc/commit/7123234 ]

[max-tyulin](http://staff/max-tyulin) 2020-12-01 18:40:35+03:00

2.7
---

* [shadchin](http://staff/shadchin)

 * Fix build hidereferer with Python 3.8  [ https://a.yandex-team.ru/arc/commit/7028886 ]

[elisei](http://staff/elisei) 2020-07-17 18:33:10+03:00

2.6
---

* [max-tyulin](http://staff/max-tyulin)

 * Улучшение логирования  [ https://a.yandex-team.ru/arc/commit/6920966 ]

* [neofelis](http://staff/neofelis)

 * PR from branch users/neofelis/feature/WIKI-13954

Исправляем Response Splitting (WIKI-13954) которая могла быть эксплуатирована через netloc (в примере - через ya.ru:13 ... ) а также добавил через схему и фрагмент  [ https://a.yandex-team.ru/arc/commit/6920400 ]

[max-tyulin](http://staff/max-tyulin) 2020-06-10 14:39:30+03:00

2.5
---
 * WIKI-13881: Улучшение логов, доп. обработка исключений  [ https://a.yandex-team.ru/arc/commit/6916481 ]

[max-tyulin](http://staff/max-tyulin) 2020-06-09 11:40:03+03:00

2.4
---
 * WIKI-13960 Правка проверки кук  [ https://a.yandex-team.ru/arc/commit/6908212 ]

[smosker](http://staff/smosker) 2020-06-05 17:14:44+03:00

2.3
---
 * WIKI-11646: чиню кодировку на error page + эскейплю dist_url  [ https://a.yandex-team.ru/arc/commit/6904020 ]

[elisei](http://staff/elisei) 2020-06-04 15:29:12+03:00

2.2
---

* [elisei](http://staff/elisei)

 * WIKI-11646: html encoding спец. символов в теле error page  [ https://a.yandex-team.ru/arc/commit/6902976 ]

* [smosker](http://staff/smosker)

 * Change README.md

Note: mandatory check (NEED_CHECK) was skipped  [ https://a.yandex-team.ru/arc/commit/6896386 ]

[elisei](http://staff/elisei) 2020-06-04 13:16:37+03:00

2.1
---
 * TOOLS-2643 fix redirect

<!-- DEVEXP BEGIN -->
![review](https://codereview.common-int.yandex-team.ru/badges/review-complete-green.svg) [![elisei](https://codereview.common-int.yandex-team.ru/badges/elisei-ok-green.svg)](https://staff.yandex-team.ru/elisei) [![uruz](https://codereview.common-int.yandex-team.ru/badges/uruz-ok-green.svg)](https://staff.yandex-team.ru/uruz)
<!-- DEVEXP END -->  [ https://a.yandex-team.ru/arc/commit/6896288 ]

[smosker](http://staff/smosker) 2020-06-02 14:48:07+03:00

2.0
----

* [nslus](http://staff/nslus)

 * ARCADIA-2198 [migration] github/tools/hidereferer  [ https://a.yandex-team.ru/arc/commit/6886897 ]

* [smosker](http://staff/smosker)

 * убрал лишнее                                           [ https://a.yandex-team.ru/arc/commit/6886840 ]
 * TOOLS-2643 Подготовка к переносу в Аркадию + python 3  [ https://a.yandex-team.ru/arc/commit/6886839 ]

[smosker](http://staff/smosker) 2020-06-01 12:44:36+03:00

1.11
----
 * COMPUTERPROBLEM-247: удаляю пробелы из урла  [ https://github.yandex-team.ru/tools/hidereferer/commit/bd873ae ]
 * WIKI-11485: добавил конфиг ревьюшницы        [ https://github.yandex-team.ru/tools/hidereferer/commit/81b8b58 ]

[Alexey Mikerin](http://staff/elisei@yandex-team.ru) 2019-09-02 19:32:44+03:00

1.10
---
 * WIKI-11224: Hidereferer – открывать safety вместо infected для зараженных ссылок  [ https://github.yandex-team.ru/tools/hidereferer/commit/ad6d37c ]

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2018-08-21 18:14:00+03:00

1.9
---
 * WIKI-10638: добавить zen.yandex.ru в список исключений                            [ https://github.yandex-team.ru/tools/hidereferer/commit/e95c8e6 ]

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2018-08-21 18:14:00+03:00

1.8
---
 * WIKI-10472: редиректить на https://yandex.ru/search/infected/?url=%url% для зараженных ссылок  [ https://github.yandex-team.ru/tools/hidereferer/commit/9d1d78f ]

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2017-12-27 18:48:41+03:00

1.7
---
 * Не отдаем 500 при некорректных ответах от Редиректора  [ https://github.yandex-team.ru/tools/hidereferer/commit/bb1c3c5 ]

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2017-11-10 13:40:43+03:00

1.6
---
 * WIKI-10472: Отказ от файлов с информацией о зараженных сайтах  [ https://github.yandex-team.ru/tools/hidereferer/commit/e693885 ]

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2017-10-25 13:35:52+03:00

1.5
---

* [Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru)

 * Добавляем yadi\.sk в список доверенных доменов

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2016-11-16 14:43:26

1.4
---

* [Sergey Kryzhanovsky](http://staff/another@yandex-team.ru)

 * pytz==2016.6.1

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2016-08-10 13:13:55

1.3
---

* [Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru)

 * TOOLS-1898: Перейти на новое апи для подновления авторизационных кук в статусе NEED_RESET

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2016-07-22 13:06:12

1.2
---

* [Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru)

 * TOOLSUP-5794: Корректно работаем с transfer-encoding: chunked

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2016-07-22 09:23:38

1.1
---

* [Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru)

 * Удалил ненужное про /etc/yandex из uwsgi.ini
 * Переезд из registry.ape.yandex.net в registry.yandex.net
 * 302 Redirect h.yandex.net -> h.yandex-team.ru
 * blackbox.yandex-team.ru now have ipv6 address
 * Исправил README.md

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2016-07-19 17:24:40

1.0
---

* [Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru)

 * TOOLS-1907: Перевезти хайдреферер в облако

[Oleg Gulyaev](http://staff/o-gulyaev@yandex-team.ru) 2016-07-07 09:58:48

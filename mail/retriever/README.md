# retriever (webattach)
Сервис **retriever** (*webattach*) отвечает за получение вложений письма.

## HTTP API
* **/ping** - pong (тест доступности сервиса)
* **/message_part_real** - содержимое вложения письма

см. [API retriever](https://wiki.yandex-team.ru/users/elsid/retriever/)

У сервиса фактически одна ручка, однако по причине того, что сервис торчит наружу, иногда прилетают запросы на случайные ручки. Вот пример распределения запросов по ручкам за день для одного из узлов:
<pre style="overflow-x: auto; word-break: none">
 480609 request=/message_part_real/
  75836 request=/ping
     39 request=/message_part_real
     17 request=
      4 request=/apple-touch-icon.png
      4 request=/
      2 request=/robots.txt
      2 request=/apple-touch-icon-120x120-precomposed.png
      2 request=/apple-touch-icon-120x120.png
      1 request=/https://webattach.mail.yandex.net/
      1 request=/apple-touch-icon120x120.png
</pre>

## Архитектура
* qloud: https://platform.yandex-team.ru/projects/mail/retriever

| группа                             | суффикс           | число узлов |
| :--------------------------------- | :---------------- | ----------: |
| mail_retriever_production          |                   |     **244** |
|                                    | _retriever        |         230 |
|                                    | _retriever-canary |           3 |
|                                    | _retriever-old    |           3 |
|                                    | _retriever-ua1    |           4 |
|                                    | _retriever-ua2    |           4 |
| mail_retriever_intranet-production |                   |       **7** |
|                                    | _retriever        |           6 |
|                                    | _retriever-canary |           1 |

\* Число узлов по состоянию на октябрь 2019

#### Структура контейнера
<img src="https://jing.yandex-team.ru/files/bmichail/RetrieverArchitecture.png"/>

Сервис **retriever** живёт в отдельном контейнере. Кроме самого сервиса в контейнере располагаются другие вспомогательные сервисы: **nginx** (проксирует запросы извне, ограничивает? rps), **supervisord** (следит за процессом сервиса, перезапускает сервисы), **unistat** (собирает статистику для yasm, отвечает на запрос */unistat*).

#### Цикл работы
<img src="https://jing.yandex-team.ru/files/bmichail/RetrieverFlow.png"/>

* Потребитель приходит в сервис с запросом, содержащим *sid* (attach_sid, защищенный идентификатор аттача).
    * *retriever* расшифровывает *sid* и извлекает из него *uid* (идентификатор пользователя) и *mid* (идентификатор письма).
    * *retriever* обращается с полученными *uid* и *mid* к сервису *hound* за метаинформацией о письме, которая, кроме прочего, содержит *stid* (ключ для доступа к содержимому письма в MDS), информацию о количестве и типах аттачей, их размерах и расположении (смещении).
    * *retriever* отправляет запросы в *storage* (MDS) и получает содержимое аттачей; в зависимости от их типа и/или размера, сервис может выполнять несколько (на практике до нескольких десятков) обращений к MDS, выкачивая содержимое частями.
    * если аттач это картинка, то (в зависимости от параметров запроса */message_part_real*) возможен поход в *resizer* для формирования пиктограммы

## Logs

* **nginx**:
    * **access** (/var/log/nginx/retriever/access.tskv)
* **retriever**:
    * **http_client** (/app/log/http_client.tskv)
    * **access** (/app/log/access.tskv)
    * **retriever** (/app/log/retriever.tskv)
* **прочие**:
    * yplatform.log (/app/log/yplatform.log)
    * unistat (/app/log/unistat.stdout, .../unistat.stderr)
    * profiler.log (/app/log/profiler.log)
    * supervisord (/var/log/supervisor/supervisord.log)

#### Что в логах
* в *nginx* *access* регистрируются поступившие в proxy-сервис запросы и статусы их выполнения.
* в *retriever* *access* регистрируются запросы, которые дошли до сервиса.
* в *http_client* регистрируются http-обращения к внешним сервисам: hound, mds, resizer.
* в *retriever* попадает более детальная информация о работе сервиса: причины ошибок и ретраев обращений к hound, MDS, ошибки расшифровки *sid*'ов.

## Dashboards
* [production](https://yasm.yandex-team.ru/template/panel/retriever_panel/env=production/)
* [corp](https://yasm.yandex-team.ru/template/panel/retriever_panel/env=intranet-production/)

Примерное распределение запросов по времени в течение суток (будни) по всему кластеру

![График распределения запросов за сутки по кластеру](https://yasm.yandex-team.ru/img/9408ef931d5b450b1165f1cbe12625dd.png)
Для примера взят график входящих запросов за 3 октября 2019 года (вторник):

* общее число запросов: ~115 млн.
* среднее число запросов в секунду: ~1,3 тыс.
* min число запросов в секунду: ~0,3 тыс.
* max число запросов в секунду: ~2,6 тыс.
* распределение rps по времени:
    * 00:00 - 06:00 - ~0,4 тыс.
    * 06:00 - 10:00 - рост до ~2,4 тыс.
    * 10:00 - 16:00 - сохранаяется на уровне ~2,2-2,6 тыс.
    * 16:00 - 00:00 - плавное снижение
* max число запросов в секунду для одного узла: до ~60 (как такового ограничения сверху нет)

### Ссылки
* [API retriever](https://wiki.yandex-team.ru/users/elsid/retriever/)
* [Про resizer](https://wiki.yandex-team.ru/mds/resizer/)

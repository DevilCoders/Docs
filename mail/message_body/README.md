# MBODY (message_body)
 Сервис **mbody** (*message_body*) отвечает за получение тела письма.

## HTTP API
* **/ping** - pong (тест доступности сервиса)
* **/message** - тело письма
* **/headers** - список хедеров писем
* **/message_source** - исходник письма
* **/pumpkin/enable, /pumpkin/disable** - включение и выключение тыквы

см. [API message-body](https://wiki.yandex-team.ru/pochta/backend/message-body/)

Если не учитывать запросы */ping*, то на ручку */message* приходится около 99,8-99,9% запросов, 0,1-0,2% - */headers* и */message_source*, - менее 0,001%.

## Архитектура
* qloud: https://platform.yandex-team.ru/projects/mail/mbody

| группа                | суффикс       | число узлов |
| :---------------------| :------------ | ----------: |
| mail_mbody_production |               |     **180** |
|                       | _mbody        |         177 |
|                       | _mbody-canary |           3 |
| mail_mbody_corp       |               |       **9** |
|                       | _mbody        |           8 |
|                       | _mbody-canary |           1 |

\* Число узлов по состоянию на февраль 2020


#### Структура контейнера
<img src="https://jing.yandex-team.ru/files/bmichail/MBodyArchitecture.png"/>

Сервис **mbody** живёт в отдельном контейнере. Кроме самого сервиса в контейнере располагаются другие вспомогательные сервисы: **nginx** (проксирует запросы извне, ограничивает rps), **supervisord** (следит за процессом сервиса, перезапускает сервисы), **unistat** (собирает статистику для yasm, отвечает на запрос */unistat*).

#### Цикл работы
<img src="https://jing.yandex-team.ru/files/bmichail/MBodyFlow.png"/>

* Потребитель приходит в сервис с запросом, содержащим *uid* (идентификатор пользователя) и *mid* (идентификатор письма).
    * *mbody* идет в *sharpei* за информацией о том на каком шарде хранится метаинформация для пользователя с заданным *uid*.
    * *mbody* обращается к метабазе (*mdb*) за информацией о письме с указанным *mid* и, кроме прочего, получает *stid* - ключ для доступа к содержимому письма в MDS.
    * *mbody* отправляет запрос в *storage* (MDS) и получает содержимое письма (обращение по ручке */message* обычно приводит к выполнению двух запросов в MDS).
    * полученное содержимое отдается на обработку в *sanitizer* для удаления опасного содержимого
        * если *sanitizer* недоступен, производится санитайзинг собственными силами (так называемой *тыквой*): html превращается в plain-text, что приводит к потере форматирования.
    * письмо (его идентификатор) отдается в *factextractor* для извлечения (поиска) *фактов*
        * если *factextractor* недуступен, факты игнорируются
* Потребителю отдается сформированный ответ содержащий тело письма, обработанное санитайзером, факты и другая информация


## Logs

* **nginx**:
    * **access** (/var/log/nginx/application/access.tskv)
* **mbody**:
    * **yplatform** (/app/log/yplatform.log)
    * **http_client** (/app/log/http_client.tskv)
    * **access** (/app/log/access.tskv)
    * **mbody** (/app/log/mbody.log)
    * **profiler** (/app/log/profiler.log)
* **прочие**:
    * user_journal (/app/log/user_journal.tskv)
    * unistat (/app/log/unistat/stdout ... stderr)
    * phishing (/app/log/phishing.tskv)

#### Что в логах
* в *nginx* *access* регистрируются поступившие в proxy-сервис запросы и статусы их выполнения (или отклонения, если например превышен рейт).
* в *mbody* *access* регистрируются запросы, которые прошли проверку nginx'ом (лимиты rps, наличие ticket'а). Этот лог может содержать более специфичную информацию о запросе, например, хедеры.
* в *http_client* (*yplatform*) регистрируются http-обращения к внешним сервисам: sharpei, mds и др.
* в *mbody* попадает более детальная информация о работе сервиса: причины ошибок и ретраев обращений к MDS, факты отказа sanitizer'а и fallback'а на тыкву.


## Dashboards
* [production](https://yasm.yandex-team.ru/template/panel/mbody_panel/env=production/)
* [corp](https://yasm.yandex-team.ru/template/panel/mbody_panel/env=corp/)


Примерное распределение запросов по времени в течение суток (будни) по всему кластеру

![График распределения запросов за сутки по кластеру](https://yasm.yandex-team.ru/img/15d88c3c14a8c2ab1b1da071ca846702.png)

Для примера взят график входящих запросов за 16 июля 2019 года (вторник):

* общее число запросов: ~280 млн.
* среднее число запросов в секунду: ~3,2 тыс.
* min число запросов в секунду: ~0,45 тыс.
* max число запросов в секунду: ~7 тыс.
* распределение rps по времени:
    * 00:00 - 06:00 - ~1 тыс.
    * 06:00 - 09:00 - рост до ~7 тыс.
    * 09:00 - 15:00 - сохранаяется на уровне ~6-7 тыс.
    * 15:00 - 00:00 - плавное снижение
* max число запросов в секунду для одного узла: до 55

Для каждой машины на продакшене в nginx'е установлен лимит в 100 rps. Т.е. запас по прочности примерно двукратный.

---

## Тыква / tykva / pumpkin
POST-методы для включения и выключения режима тыквы *sanitizer*'a.

```bash
$ curl -X POST 'host:port/pumpkin/enable'
{} # sanitizer is set to 'tykva'
$ curl -X POST 'host:port/pumpkin/disable'
{} # sanitizer is set to it's original value
```
*Note: режим тыквы сбрасывается при рестарте сервиса.*

### Ссылки
* [API message-body](https://wiki.yandex-team.ru/pochta/backend/message-body/)
* [Про sharpei](https://wiki.yandex-team.ru/mail/pg/sharpei/)
* [Про factextractor](https://wiki.yandex-team.ru/aleksandrbulatov/tomita/)

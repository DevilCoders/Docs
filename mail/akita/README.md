# AKITA
 Сервис **akita** отвечает за получение информации о пользователе по куке или oauth-токену

## HTTP API
* **/ping** - pong (тест доступности сервиса)
* **/auth|ninja_auth** - проверка кук для фронтенда почты. Ручка всегда отвечает 200 OK, в случае ошибки будет специальгый json
* **/check_cookies** - проверка кук для xiva. Ручка отвечает 200 ОК в случае успеха, 400 в случае ошибки клиента и 500 если ошибка сервера

см. [API akita](https://wiki.yandex-team.ru/users/jkennedy/ywmiapi/#bezopasnostiavtorizacija)


## Архитектура
* qloud: https://platform.yandex-team.ru/projects/mail/akita

| группа                         | суффикс       | число узлов |
| :----------------------------- | :------------ | ----------: |
| mail_akita_production          |               |     **440** |
|                                | _akita        |         431 |
|                                | _akita-canary |           9 |
| mail_akita_intranet-production |               |      **11** |
|                                | _akita        |          10 |
|                                | _akita-canary |           1 |

\* Число узлов по состоянию на август 2019


#### Структура контейнера

Сервис **akita** живёт в отдельном контейнере. Кроме самого сервиса в контейнере располагаются другие вспомогательные сервисы: **nginx** (проксирует запросы извне, ограничивает rps), **supervisord** (следит за процессом сервиса, перезапускает сервисы). **unistat** в процессе добавления.

#### Цикл работы

* Потребитель приходит в сервис с запросом, содержащим набор кук или oauth-токен
* *akita* идет в *blackbox* за информацией о пользователе
* Потребителю отдается сформированный ответ с информацией о пользователях


## Logs

* **nginx**:
    * **access** (/var/log/nginx/akita/access.tskv)
* **akita**:
    * **yplatform** (/var/log/akita/yplatform.log)
    * **access** (/var/log/akita/access.log)
    * **akita** (/var/log/akita/akita.tskv)
    * **profiler** (/var/log/akita/profiler.log)
* **прочие**:
    * supervisord (/var/log/supervisor/supervisord.log)

#### Что в логах
* в *nginx* *access* регистрируются поступившие в proxy-сервис запросы и статусы их выполнения (или отклонения, если например превышен рейт).
* в *akita* *access* регистрируются запросы, которые прошли проверку nginx'ом (лимиты rps, наличие ticket'а). Этот лог может содержать более специфичную информацию о запросе, например, хедеры.
* в *yplatform* регистрируются http-обращения к внешним сервисам: blackbox, tvmapi.
* в *akita* пишутся причины почему ответили ошибкой


## Dashboards
* [production](https://gr-mg.yandex-team.ru/dashboard#mail_akita)
* [corp](https://gr-mg.yandex-team.ru/dashboard#mail_akita_corp)


![График распределения запросов за сутки по кластеру]( https://yasm.yandex-team.ru/img/1ba0f8742324c1b8d4dd710952918ba2.png 
)

Для примера взят график входящих запросов за 19 августа 2019 года:

* min число запросов в секунду: ~4 тыс.
* max число запросов в секунду: ~51 тыс.
* max число запросов в секунду для одного узла: около 150рпс в пике
* один инстанс держит около 1000 рпс

Для каждой машины на продакшене в nginx'е установлен лимит в 900 rps и burst 200



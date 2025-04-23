# Сервисы кроме Директа, которые поддерживаем

## Wordstat { #wordstat }

<https://wordstat.yandex.ru/> , веб-мордочка к ADVQ.

Статус: заморожен. Выключить не можем, вкладываться в развитие не хотим, для клиентов сервис важен.

### Где живёт
Код расположен в [аркадии](https://a.yandex-team.ru/arc/trunk/arcadia/direct/wordstat), инструкция по сборке: https://a.yandex-team.ru/arc/trunk/arcadia/direct/wordstat#build-release-and-deploy
{% note alert "Внимание" %}

В результате сборки остаются файлы и директории созданные под root'ом

{% endnote %}

Сервис живет в [Деплое](https://deploy.yandex-team.ru/stages/advq-wordstat-production) и под [аваксом](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/wordstat.yandex.ru/show/) 

### Как выкладывать
После сборки остаётся docker-образ, тегированный временем сборки. Пример имени образа: `registry.yandex.net/wordstat/frontend_deploy_build`, тег `202104302033`.

Нужно запушить его в regsitry:
`docker push registry.yandex.net/wordstat/frontend_deploy_build:YYYYMMDDHHMM`

и в [конфиге бокса](https://deploy.yandex-team.ru/stages/advq-wordstat-production/edit/du-wordstat/box-box) прописать нужный тег в Base layer.

### Логи
- Логи l7 балансеров в [логвьювере](https://direct.yandex.ru/logviewer/short/TQhLurXd3uUGjb)
- access-логи nginx: сейчас только на файловой системе в `/opt/advq-logs/access.log`
- логи ошибок perl-приложения: ошибки со стектрейсами, отрендеренными в HTML, лежат в `/opt/wordstat_errors`

### Подводные камни
- время в логах в UTC
- docker-образ собирается от "чистого" образа Ubuntu Precise, так что каких-то диагностических вещей может там не быть, например, portoctl. То, что выкладывается пакетами, можно добавлять в Dockerfile


## Custom Solutions { #custom-solutions }

Статус: загадочный.

Про эксплуатацию: <https://wiki.yandex-team.ru/jeri/#gorynych>
Старая таблица востребованности компонент: <https://wiki.yandex-team.ru/jeri/catalogue/2017-q4/gorynych/>

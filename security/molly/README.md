======
Molly
======

This project provides web interface and REST API for Web Application Security scanner (e.g. Burp Suite Pro)

Main components:

1. molly-webui - django application

Balancer: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/molly-balancer/show/
Deploy: https://deploy.yandex-team.ru/stages/molly-www

2. molly-celery - Celery task scheduler + Report parser

Deploy: https://deploy.yandex-team.ru/stages/molly-celery

3. molly-agent - Celery workers + BurpSuitePro + Phantomjs + tools

Deploy: https://deploy.yandex-team.ru/stages/molly-agents-stable

3. molly-logcollector - HTTP request collector

Balancer: https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/molly-logcollector-balancer/show/
Deploy: https://deploy.yandex-team.ru/stages/molly-logcollector

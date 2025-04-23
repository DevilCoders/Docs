# Асессорский стенд

-   [Балансер](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-crowdtest-balancer/show/)
-   [Апстрим балансера](https://nanny.yandex-team.ru/ui/#/awacs/namespaces/list/travel-frontend-crowdtest-balancer/domains/list/rasp-crowdtest/show/)
-   [Стэйдж прокси](https://deploy.yandex-team.ru/stages/travel-frontend-rasp-crowdtest-testing)
-   [Репозиторий прокси](https://a.yandex-team.ru/arcadia/travel/rasp/crowdtest_proxy)
-   [Стэйдж стенда](https://deploy.yandex-team.ru/stages/travel-frontend-rasp-assessors)
-   Домены:
    -   rasp.crowdtest.yandex.by
    -   rasp.crowdtest.yandex.kz
    -   rasp.crowdtest.yandex.ua
    -   rasp.crowdtest.yandex.uz
    -   t.rasp.crowdtest.yandex.by
    -   t.rasp.crowdtest.yandex.kz
    -   t.rasp.crowdtest.yandex.ua
    -   t.rasp.crowdtest.yandex.uz

## Как выкатить задачу на асессорский стенд

При создании пулл-реквеста в master будет собран образ, о чем робот напишет в задачу (подробнее об этом написано в разделе [Процесс разработки](/docs/developmentProcess.md)). Сообщение выглядит примерно так: "Собран образ `pr-4609.TRAVELFRONT-5619.2021-10-06_17-56-23`" вот как раз этот образ (`pr-4609.TRAVELFRONT-5619.2021-10-06_17-56-23`) и нужно выкатить в ручную на [стэйдж стенда](https://deploy.yandex-team.ru/stages/travel-frontend-rasp-assessors), как это описано в разделе [Релизный процесс](/docs/releaseProcess.md) (выкатка релиза вручную).

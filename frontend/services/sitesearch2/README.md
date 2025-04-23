Sitesearch2
===========
Stub package sitesearch2 is used to install BEM locally to build debian package yandex-sitesearch2-www.

The package is reqired as far as SERP machines do not provide global BEM and package yandex-sitesearch2-www uses LEGO 2.8,
which doesn't provide local BEM.

It should be removed after migration to LEGO 2.10.

## Разработка

Для сборки проекта нужен [ycssjs](https://wiki.yandex-team.ru/verstka/tools/ycssjs/). Его можно установить как на Ubuntu, так и на macOS.

После клонирования репозитория поднять проект можно так:

```
make -B build
nvm use 12
npm run start:public # Поднимет домен
```

На машинках из группы [wmc-dev-front](https://c.yandex-team.ru/groups/wmc-dev-front) уже установлен ycssjs. Если вы подняли на этой машине бету через `npm start`, бета будет поднята на указанном вами порту (в примере 3001), до которого у вас, скорее всего, нет дырок. Чтобы не делать дырки для всех портов удалённой машины, поднимите SSH-туннель с вашего ноутбука до удалённой машины:

```
npm run start:public # Поднимет публичный домен
```

## Статика

Статика деплоится в S3 MDS: бакеты serp-static-testing для тестинга, sitesearch2 для продакшена.

 * [Cборка релиза](https://a.yandex-team.ru/projects/frontend/ci/releases/timeline?dir=frontend%2Fservices%2Fsitesearch2&id=release)

## Links

  * [Production](https://yandex.ru/search/site/?searchid=2205041&web=1&text=трамп)
  * [Dev](https://login-1-ws1.tunneler-si.yandex.ru/search/site/?searchid=234354&web=1&text=трамп)
  * [HTML&CSS](https://sitesearch.common.yandex.net/yandex.ru/search/site/htmlcss.html?searchid=2205041&text=трамп)
  * [Iframe](https://sitesearch.common.yandex.net/yandex.ru/search/site/iframe.html?searchid=1486269&text=трамп&web=0)

## Тестирование выдачи ПДС при релизах частей Поиска

При релизах репорта, апхостового графа и других частей Поиска нужно убедиться, что выдача ПДС не поломалась. Для этого в Sandbox нужно запустить таску SITESEARCH_INTEGRATION_TEST, которая прогонит тесты ПДС на заданной выдаче.

- Код тестов: [hermione](hermione)
- Таска в сандбоксе: [SITESEARCH_INTEGRATION_TEST](https://sandbox.yandex-team.ru/tasks?type=SITESEARCH_INTEGRATION_TEST&page=1&pageCapacity=20&forPage=tasks)
- Шедулер для ее запуска: [10638](https://sandbox.yandex-team.ru/scheduler/10638/view)
- Код беты для тестов htmlcss и iframe выдачи: [sitesearch-serp-test](https://github.yandex-team.ru/isqua/sitesearch-serp-test)
- Релевантная задача: [SITESEARCH-3448: Тесты на поисковую часть ПДС](https://st.yandex-team.ru/SITESEARCH-3448)

# repo-coupling

Скрипт строит зависимости между репозиториями. Для него нужны данные: список пакетов в репозитории мы возьмём из склонированных репозиторев. Список зависимостей придётся скачать из OKO. Для этого вам нужно будет сохранить ответ ручки OKO — только дёргать придётся из браузера, т.к. она залогиновая.

Для визуализации установите [Graphviz](https://graphviz.gitlab.io/about/):

```
brew install graphviz
```

Вам нужно сохранить ответы ручки для искомых репозиториев в файлы с расширением `.json`. Примеры:

- Сохраняем https://oko.yandex-team.ru/api/getRepoDependecyList?repoName=search-interfaces/frontend в `frontend.json`
- Сохраняем https://oko.yandex-team.ru/api/getRepoDependecyList?repoName=search-interfaces/infratest в `infratest.json`
- Сохраняем https://oko.yandex-team.ru/api/getRepoDependecyList?repoName=search-interfaces/ci в `ci.json`
- Сохраняем https://oko.yandex-team.ru/api/getRepoDependecyList?repoName=search-interfaces/trendbox-ci в `trendbox-ci.json`
- Сохраняем https://oko.yandex-team.ru/api/getRepoDependecyList?repoName=search-interfaces/microservices в `microservices.json`

Вам нужно иметь скачанные репозитории локально.

Чтобы построить граф, нужно скормить скрипту список папок-репозиториев и список файлов-json’ов. Аргументы интерпретируются очень просто: все аргументы с расширением `.json` считаются файлами OKO, всё остальное считается папками-репозиториями. Вот как можно построить граф для репозиториев:

```
npm_config_registry=https://npm.yandex-team.ru npx @yandex-int/repo-coupling \
    ../frontend \
    ../infratest \
    ../ci \
    ../trendbox-ci \
    ../microservices \
    frontend.json \
    infratest.json \
    ci.json \
    trendbox-ci.json \
    microservices.json
```

В результате работы тулзы получатся четыре файла:

- packages.dot — граф в формате Graphviz с зависимости репозиториев от пакетов
- packages.png — отрисованный граф
- repos.dot — граф в формате Graphviz с зависимости репозиториев от репозиториев
- repos.png — отрисованный граф

# Metrics launch manager frontend

* [production](https://mlm.yandex-team.ru)
* [testing](https://metrics-launch-manager-dev.qloud.yandex-team.ru)

### Релиз в Qloud
* вмёрджить и собрать [новую версию](https://teamcity.yandex-team.ru/viewType.html?buildTypeId=search_evaluation_MetricsLaunchManagerFrontend_MergeAndReleaseToProduction), результатом сборки будет артефакт с версией
* обновить ее в [qloud](https://qloud.yandex-team.ru/projects/quality/metrics-launch-manager/development?component=frontend&update=yes)

### Установка
* [установить nodejs и npm](http://nodejs.org/)

#### Забираем из репозитория
```
user:~/ $ git clone ssh://git@git.qe-infra.yandex-team.ru/search-evaluation/metrics-launch-manager-frontend.git mlmf
user:~/ $ cd mlmf
user:~/mlmf $ npm install
```


### Сборка и локальный запуск

* в /etc/hosts добавляем строчку
```
127.0.0.1       mlm.qe-local.yandex-team.ru
```
* `npm start` запускает сервер webpack
* открываем [страницу](https://mlm.qe-local.yandex-team.ru:8080) в браузере
* для тестирования на продакшн данных
```
npm start -- --backend production`
```
* если надо собрать проект в `/target` без запуска локального сервера
```
npm run build
```
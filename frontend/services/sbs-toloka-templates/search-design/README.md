[![N|Solid](https://jing.yandex-team.ru/files/excel/2016-11-28_21.20.17.png)](https://nodesource.com/products/nsolid)

# samadhi-toloka
Данный проект помогает разрабатывать шаблоны **samadhi** для Яндекс.Толока.
Включает в себя два инструмента:

  - Локальный запуск шаблона на задании из выброного проекта -> пула
  - Деплой шаблона на указаный проект

# Запуск и использование
Для запуска проект необходимо выполнить команду:
```sh
$ npm run search-design:init
$ open ./samadhi.secret.json
```

В открывшемся файле необходимо указать токены для интересующего окружения (обязательно только для необходимого окружения)
  - **sandbox** - [sandbox.toloka.yandex.ru](https://sandbox.toloka.yandex.ru/)
  - **prod** - [toloka.yandex.ru](https://toloka.yandex.ru/)
  - **yang-sbox** - [sandbox.yang.yandex-team.ru](https://sandbox.yang.yandex-team.ru/)
  - **yang-prod** - [yang.yandex-team.ru](https://yang.yandex-team.ru)

#### Получение токена
Получить токен можно в личном кабинете, как это сделано описано [на странице документации Яндекс.Толока](https://tech.yandex.ru/toloka/doc/concepts/access-docpage/). Этот токен нужно указать в файле выше.
Также токены можно посмотреть [здесь](https://yav.yandex-team.ru/secret/sec-01cn53b0mcf16njk1haxjrzp3n/explore/versions)

#### Использование
```sh
$ npm run search-design:go
```
При запуске программа попросит ввести окружение (`sandbox`, `prod`, `yang-sbox`, `yang-prod`) и ввести id нужного проекта.

#### Доступные команды
  - **init** - переключение между проектами и окружениями
  - **write_proj_cfg** - обновляет файл конфигурации `samadhi.project.json` записывая в него настройки текущего проекта
  - **deploy** - обновляет удаленный проект. Обновляются входные параметры, выходные параметры и файлы проекта с разметкой, стилями и скриптами. (информация подтягивается из файла `samadhi.project.json`)
  - **deploy_batch** - запускает серию деплоев указанных в файле `samadhi.deploy.batch.json`
  - **update_specs** – обновляет спецификацию входны/выходных данных текущего проекта (берется из файла
  `io-specs.js`)
  - **run** - запускает локальный сервер разработки на основе информации в `samadhi.project.json`. Предлагает выбрать один из доступных пулов в проекте.
  - **stop** - останавливает сервер.
  - **exit** - выход из программы.
  - **help** - список доступных команд.
  
  
#### Пример деплоя настроек проекта
  - `$ npm run search-design:go`
  - `init` Ввести название окружения и id проекта
  - `write_proj_cfg` Обновить текущие параметры проекта
  - В файле `samadhi.project_update.json` указать новые настройки проекта
  - `deploy` для деплоя в текущий проект или `deploy_batch` для обновления нескольких проектов до текущий настроек

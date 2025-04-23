# HOWTO

## Подготовка

### устававливаем yc - cli к Яндекс.Cloud
https://cloud.yandex.ru/docs/cli/quickstart#install

нужны 2 федерации

для baseimage: `ajesnqgjakesl1dvjh47`

для supportai: `aje4atja7u8h3iaetofn`

убеждаемся что в https://console.cloud.yandex.ru/federations/<federation_id>
нас пускает
авторизация через <login>@yandex-team.ru

### настраиваем yc

`yc init --federation-id=<federation_id`

называем профили понятно, чтобы можно было переключаться между ними

для выкатки в тестинг достаточно 1 профиля, выбираем folder testing

если нужна выкатка в продакшен, то настраиваем 2й профиль, соответственно с folder production

список профилей

`yc config profile list`

переключиться на профиль

`yc config profile activate <profile_name>
`
### скачиваем baseimage
для этого переключаем yc на baseimage и далее

`IAM_TOKEN=$(yc iam create-token)`

где-то тут будет отсылка в браузер, где нужно ввести `<login>@yandex-team.ru`

`docker login --username iam --password $IAM_TOKEN cr.yandex`

`docker pull cr.yandex/crpjnf40unocamomb3i5/taxi-base-kube-xenial`

### настраиваем kubernetes
устанавливаем консольный клиент
https://kubernetes.io/docs/tasks/tools/install-kubectl/

переключаем yc на supportai
смотрим id kubernetes кластера

`yc managed-kubernetes cluster list`

настраиваем конфиг kubectl

`yc managed-kubernetes cluster get-credentials <cluster_id> --external`

убеждаемся, что kubernetes сконфигурировался

`kubectl config view`

`kubectl get po`


## Выкатка в testing

переключаем yc на supportai

получить токен

`IAM_TOKEN=$(yc iam create-token)`

`docker login --username iam --password $IAM_TOKEN cr.yandex`

обновить версию front в гите в файле `kubernetes/testing/front.deployment.yaml`

собрать новый образ

`REGISTRY_ID=crpri850lhmnh8hn3449`

`docker build . --build-arg YANDEX_ENVIRONMENT=testing -t cr.yandex/${REGISTRY_ID}/front:<new_version>`

`docker push cr.yandex/${REGISTRY_ID}/front:<new_version>`

запустить deploy

`kubectl apply -f kubernetes/testing/front.deployment.yaml`

смотрим за переключением

`kubectl get po`

можно зайти в pod, посмотреть что да как

`kubectl exec -it <pod_id> bash`


## Выкатка в production

Аналогична выкатке в тестинг, но

`PRODUCTION_REGISTRY_ID=crpnq1h4legv4n8hqcgt`

Не забыть пересобрать с `--build-arg YANDEX_ENVIRONMENT=stable`

`docker build . --build-arg YANDEX_ENVIRONMENT=stable -t cr.yandex/${PRODUCTION_REGISTRY_ID}/front:<new_version>`

`docker push cr.yandex/${PRODUCTION_REGISTRY_ID}/front:<new_version>`

Обновить версию front в гите в файле `kubernetes/stable/front.deployment.yaml`

`kubectl apply -f kubernetes/stable/front.deployment.yaml`

Переключение между конфигурациями kubectl через

`kubectl config use-context yc-taxisupportai-testing`

`kubectl config use-context yc-supportai-production-kubernets-claster`

## Запуск проекта (фронт)

Сначала устанавливаем необходимое окружение:
- Node.js - v14.15.3
- npm - v6.14.9
- Python - v3.9.1

Приложение состоит из 3-х частей: клиентская часть на React.js, сервер-прослойка Node.js и закрытый сервер.

Клиент React.js ⟷ Прослойка Node.js ⟷ Сервер

Сначала устанавливаем зависимости Клиента. Переходим в папку src
`npm install`

Дальше зависимости Прослойки. Переходим в папку src/server
`npm install`

Для локального запуска на машине нужно запустить свой экземпляр Клиента и Прослойки.
Запуск Клиента: в папке src: `npm run start`
Запуск Прослойки: в папке src/server: `node index.js`

## Список поддерживаемых capability:
- `personal_account` - доступ к странице "Метрики"
- `dialogs_history` - доступ к странице "История диалогов"
- `topics` - доступ к странице "Создание тематик"
- `thresholds` - доступ к странице "Настройка модели"
- `features` - доступ к странице "Признаки"
- `scenarios` - доступ к странице "Сценарии"
- `scenario_modify_actions` - Расширенный редактор сценариев. Добавляет возможность просматривать/добавлять/редактировать действия
                              "Специальное действие" и "Изменить признак". Действие "Ответ пользователю" доступно по умолчанию и не управляется этой capability.
                              Также добавляет просмотр/редактирование поля "Дополнительно" у сценариев и страницу "Advanced настройки" для редактирования конфигов проекта.
- `tasks` - доступ к странице "Выгрузки настроек"
- `live_dialog` - доступ к странице "Online-тестирование" а также возможность отображения кнопки "Продолжить диалог" на странице истории диалогов
- `voice` - Доступ к странице "Голос"
- `quality_control` - доступ к странице "Разметка диалогов"
- `validation` - Возможность начать валидацию проекта
- `demo` - Возможность загрузить диалоги и статистику для демо проектов
- `update_records` - Возможность обновить записи на странице "Голос"
- `testing` - Доступ к странице "Тестирование"
- `history_changes` - Доступ к странице "История изменений"
- `manage_versions` - Доступ к странице "Управление версиями"
- `access` - Доступ к странице "Доступы"
- `graph_editor` - Доступ к странице "Сценарии 2.0" (граф)
- `hide_internal_errors` - Скрывает сообщения о серверных ошибках (код ответа которых начинается с 5)
- `manage_capabilities` - Доступ к странице "Дополнительные возможности"
- `deploy` - Возможность опубликовать версию на странице "Выгрузки настроек"
- `change_model` - Возможность менять модель проекта на странице "Настройка модели"
- `projects_list` - Доступ к странице "Список проектов"
- `messages_milliseconds` - Отображение миллисекунд в датах сообщений
- `superusers` - Доступ к странице "Суперпользователи"
- `learn_models` - Доступ к странице "Обучение моделей"
- `integrations` - Доступ к странице "Интеграции"
- `dialogs_history_filter_version` - Возможность на странице "История диалогов" фильтровать сообщения по версии
- `export_import_graph` - Возможность загружать и выгружать граф в формате JSON
- `upload_external_phone_ids` - Возможность загружать файл для обновления идентификаторов телефонных номеров
- `clustering` - Возможность получать тексты диалогов по проекту и добавлять их в опорные фразы
- `clustering_launch` - Возможность запускать группировку текстов диалогов по проекту
- `force_enable_online_testing` - Выключить заглушку на странице "Онлайн-тестирование". Временная капабилитис, нужна на время улучшения подхода к Онлайн-тестированию.
- `calls_metrics` - Доступ к статистике по звонкам
- `scenarios_page` - Доступ к странице выбора сценария
- `new_scenario_editor` - Доступ к новому редактору настроек сценария на графе при клике на первую ноду
- `incoming_integrations` - Доступ к странице входящих интеграций

Стандарты и практики на фронте

Вёрстка:
  1. В основном вся вёрстка построена на следующих компонентах:
  - `Row, Column` - Обёртки над flex-div'ами. В пропсах можно указать justifyContent, alignItems и т.д. для управления дочерними элементами
  - `Container` - Обёртка над div'ом, служит для выделения области определенных размеров. Обычно в пропсах передаётся широта/высота

Взаимодействие с сервером:
  1. Сервер использует snake_case для именования полей объектов, на фронте используется camelCase, поэтому перед сохранением данных от сервера в стор нужно прогнать данные через функции-преобразователи. Они хранятся в `types/parsers`. Также в этих функциях можно помими переименования полей делать ещё какие-нибудь преобразования, валидации и т.п.
  2. Типы запросов на сервер описаны в `types/requests`
  3. Авторизация. Существует 2 способа авторизоваться: через Яндекс.oAuth и собственная авторизация через логин/пароль. `Задача авторизации - получить токен, user_id и provider (флаг, который указывает, каким из способов была проведена авторизация - 'yandex.passport' или 'supportai')`. Эти три сущности сохраняются в localStorage, после чего используются при отправке запросов
    3.1. Авторизация через Яндекс.Паспорт. После нажатия на кнопку "Авторизоваться через Яндекс" пользователя перебрасывает на страницу авторизации Яндекс.oAuth, где он даёт разрешение авторизовать его аккаунт. После этого Яндекс.oAuth перебрасывает пользователя обратно в наше приложение на страницу /auth с хеш-параметром access_token в строке запроса. Этот токен отправляется на Node.js прослойку. Node.js прослойка отправляет токен Яндекс.Паспорту, получает пользователя и возвращает в react приложение. Такми образом есть token (полученный от oAuth), user_id (полученный от Яндекс.Паспорта) и provider (устанавливается на фронте как 'yandex.passport')
    3.2. Собственная авторизация через логин/пароль. Доступна по пути /supportai. Вводим логин, пароль, отправляем на Node.js прослойку, оттуда на сервер. Сервер возвращает токен и пользователя. Таким образом, фронт получает token и user_id от сервера и provider устанавливается как 'supportai'

Redux
  1. Для централизованной обработки ошибок используется middleware, перехватывающий все action'ы, у которых в payload есть поле error `(errors.ts в redux/middlewares))`. Для удобной обёртки можно использовать класс ErrorAction, при создании объекта которого нужно передать ошибку, перевод сообщения ошибки и параметры, если нужно как-то обработать ошибку в reducer'e.
  2. Для сохранения данных между сессиями и кеширования можно использовать `cache middleware (cache.ts в redux/middlewares))`. Как с ним работать:
    в cacheConfig нужно создать новое поле, где ключом будет являться тип action'а, а в значение передать объект со следующими полями:
      - cacheItem - ключ (произвольная строка), по которому будет кешироваться значение.
      - stateCallback (опционально) - callback-функция, возвращающая значение, которое нужно закешировать. Если не указывать, то будет закеширован payload action'a. Если указывать - то закешируется значение, которое вернула функция stateCallback

## Table of Contents
1. [Установить зависимость](#install-deps)
2. [Линтер на версии пакетов](#depslint)
3. [Дедупликация](#dedupe)
4. [dependencies vs devDependencies](#deps-vs-devdeps)
5. [Базовый контейнер для Sandbox](#base-sandbox-container)
6. [Ресурсы](#sandbox-resources)
7. [service.yaml](#service-yaml)

### Установить зависимость <a name="install-deps"></a>
В npm workspaces используется один `package-lock` - в корне монорепы

`package.json` есть в каждом 'листе'
```bash
# во всех листьях
npm i --save react -ws

# в конкретном
npm i --save react -w projects/website

# нескольких конкретных
npm i --save react -w projects/website -w projects/webview
```

Если возникает ошибка `Unable to resolve dependency tree`, то добавить флаг `--legacy-peer-deps`.

### Линтер на версии пакетов <a name="depslint"></a>

Настроен линтер на одинаковые версии зависимостей во всех листьях. Посмотреть его реализацию можно в `packages/lint/deps.js`

Исключения можно сконфигурировать в файле `.depslint.js` в корне монорепы:
```js
module.exports = {
  skipFor: ['react-router-dom'],
}
```

Теперь можно иметь разную версию `react-router-dom` в листьях.

### Дедупликация <a name="dedupe"></a>
При условии одинаковых версий зависимостей все пакеты должны быть установлены в корневом node_modules

Однако бывает так, что при установке/обновлении зависимость оседает в конкретных листьях, например:
```bash
- lavka/
  - node_modules/
    - babel-loader@7 # зависимость от зависимости
  - projects/
    - webview/
      - node_modules/
        - babel-loader@8 # прямая зависимость у webview
    - website/
      - node_modules/
        - babel-loader@8 # прямая зависимость у website
```

В идеальном мире в корневом `node_modules` должен быть `babel-loader@8`, а `babel-loader@7` должен лежать у своего родительского пакета

Это можно попробовать полечить с помощью команды:
```bash
npm dedupe -ws
```

Если не помогло, то:
```bash
# 1. удаляем все node_modules и корневой package-lock
# 2. перегенерируем package-lock.json
# 3. устанавливаем зависимости

npm run reinstall-deps
```

### dependencies vs devDependencies <a name="deps-vs-devdeps"></a>
Флоу сборки приложения:
1) Установка всех зависимостей
2) Сборка приложения
3) Удаление `devDependencies`

Если пакет нужен на этапе рантайма и без него сервер не запустится, то его нужно добавить в `dependencies`. Например - `express`.

Если пакет нужен только для сборки, то в `devDependencies` - например `webpack` или `prettier`.

Удаление `devDependencies` позволяет немного сэкономить на размере итогового образа.

### Базовый контейнер для Sandbox <a name="base-sandbox-container"></a>

В Sandbox можно создать LXC контейнер с предустановленными зависимостями, например nodejs и npm:
https://ui.yandex-team.ru/arcadia/ci/sandbox#lxc-kontejnery

Затем указать идентификатор "сваренного" контейнера в задачах — контейнер будет там использоваться

Для создания нового контейнера с NodeJS можно использовать команду:

```bash
env NODE_VERSION=16.13.1 npm run dev:images
```

Либо можно клонировать последнюю задачу из списка:
https://sandbox.yandex-team.ru/tasks?children=false&hidden=true&owner=LAVKASERVICES&tags=NODEJS%2CLAVKA-FRONTEND&type=SANDBOX_LXC_IMAGE&all_tags=true&limit=20&offset=0
и подправить секцию `custom_script`

После успешного завершения нужно зайти на вкладку `Resources`, перейти в ресурс `LXC_CONTAINER` и нажать на
кнопку `Important` (иконка флажка)
Это увеличит время жизни ресурса до "бесконечно"

Затем идентификатор ресурса нужно прописать в файл `a.yaml` в
секцию `shared.sandbox_requirements.requirements.sandbox.container_resource`

### Ресурсы <a name="sandbox-resources"></a>

Типы ресурсов можно посмотреть в
модуле https://a.yandex-team.ru/arc_vcs/sandbox/projects/lavka/frontend/utils/resource_types

LAVKA_FRONTEND_PROJECT_BUILD — ресурс с исходниками приложения:
https://sandbox.yandex-team.ru/resources?type=LAVKA_FRONTEND_PROJECT_BUILD&limit=20

### service.yaml <a name="service-yaml"></a>

TODO: описать `lavka-frontend` велосипеды

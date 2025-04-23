# Скрипт docker-autorelease

## Описание
Для облегчения сборки docker-образов в вертикалях есть скрипты autorelease, их исходники можно [найти тут](https://a.yandex-team.ru/arcadia/classifieds/infra/vertis-packages/yandex-vertis-autorelease/data/usr/bin).

Все скрипты доступны на teamcity-агентах и их можно использовать в качестве шага сборки `Command Line`

{% cut "Подробнее" %}

![docker-autorelease-teamcity.png](docker-autorelease-teamcity.png)

{% endcut %}

Скрипты `docker-debian-autorelease` и `autorelease` **deprecated** и находятся на поддержке - новые фичи в них не добавляются.

## docker-autorelease
**docker-autorelease** позволяет собирать docker-образы из исходников и запускать деплой

{% cut "Доступные опции" %}

- `-h --help`          - вызвать help.
- `--docker-name=`     - с каким именем собрать docker-образ.
- `--docker-version=`  - с какой версией собрать docker-образ.
- `--release-message=` - сообщение в релизе(deprecated).
- `--dry-run`          - запретить деплой после сборки контейнера.
- `--env-build-time=`  - при сборке пробрасывает в контейнер переменную окружения `BUILD_TIME`.
- `--env-revision=`    - при сборке пробрасывает в контейнер переменную окружения `REVISION`.
- `--branch=`          - бранч в деплое, в который выкатится приложение.
- `--project-workdir=` - директория с приложением, где лежит Dockerfile.
- `--shiva`            - после сборки запустить деплой в shiva.
- `--issues`            - <span style="color:green">(only shiva)</span> номера задача в трекере для связи с деплоем (в виде комментария после успешной выкладки), разделенные запятыми
- `--user=`             - <span style="color:green">(only shiva)</span> staff логин инициатора only shiva
- `--comment`          - <span style="color:green">(only shiva)</span> комментарий к деплою. Будет выведен как markdown и не имеет ограничений на длину (deprecated)
- `--raw-comment` - <span style="color:green">(only shiva)</span> комментарий к деплою в оригинальном виде (будет сделан escape). Будет выведен как markdown и не имеет ограничений на длину
- `--metadata` - <span style="color:green">(only shiva)</span> произвольная строка с метаданными для деплоя (передаётся вместе с событиями деплоя в хуках, используется для интеграций). Ограничение по длине 64Кб
- `--service-name=`            - имя сервиса, для деплоя(используется если имя docker-образа отличается от имени сервиса в карте сервисов).
- `--skip-vcs`                 - не пушить в git tag с собранной сервией.
- `--transient=<true|false>`   - пишет в release-message сообщение из последнего коммита и использует его хеш как версию для docker-образа
- `--use-git-tag=<true|false>` - берет последний git tag и использует его в качестве версии docker-образа.
- `--verify-image-exists`      - не собирает образ, а только проверяет нет ли его еще в registry.
- `--dev`                      - выкатить в dev-бранч(доступно только для jenkins).
- `--deploy-without-branch`   - принудительно выкатывать без бранча в деплой.
- `--deploy-if-image-exists`  - пропустить сборку и сразу запустить деплой, если такая версия образа уже есть в registry. По умолчанию деплой не будет запущен.
- `--use-arc` - использовать команды arc вместо git.

{% endcut %}

## Примеры использования:
Сборка образа hub-api с версией 0.1-test. После сборки проставится git tag в репозиторий проекта и будет запущена выкладка в testing через jenkins.

```bash
/usr/bin/docker-autorelease --docker-name=hub-api --docker-version=0.1-test
```

Сборка hub-api с версией по хешу последнего коммита из директории hub без записи тега в git.

```bash
/usr/bin/docker-autorelease hub --docker-name=hub-api --transient=true --skip-vcs
```

Сборка docker-образа с именем hub-api, версией по хешу последнего коммита и запуск деплоя сервиса hub в shiva.

```bash
/usr/bin/docker-autorelease --docker-name=hub-api --transient=true --service-name=hub --shiva
```

Сборка docker-образа с именем hub-api, версией по хешу последнего коммита и запуск деплоя сервиса hub в shiva в бранч test1.

```bash
/usr/bin/docker-autorelease --docker-name=hub-api --transient=true --service-name=hub --shiva --nomad-branch=test1
```

## Особенности работы:
* После сборки спулить docker-образ можно будет по имени `registry.yandex.net/vertis/<имяобраза>:<версия>`. Например `registry.yandex.net/vertis/hub-api:0.1-test`.
* Сборка запустится только если docker-образа с заданной версией нет в registry. При наличии образа сборка не падает, а выходит с кодом 0.
* Если сборка запустилась в git branch, то и выкладка в деплой запустится в branch. Но можно принудительно изменить это поведение опцией `--deploy-without-branch`, с ней после сборки приложение выкатится не в бранч.
* Если не указан `skip-vcs`, скрипт запушит git tag с собранной версией в git в формате <имясервиса_версия> (например hub-api_191).
* При сборке в docker build всегда передается [аргумент](https://docs.docker.com/engine/reference/builder/#arg) `--build-arg VERSION=<версия>`

# Contributing

На основе шаблонов генерирует Dockerfile и конфиги для базовых образов с nodejs определенной версии и соответствующих им образов с логированием и мониторингами.

**ВНИМАНИЕ** Имя и актуальную версию образов нужно брать из [versions.json](./versions.json).
Резюме изменении в образах можно найти в файлах папки [changelogs](./changelogs).

## Требования

Для работы с образами локально должны быть установлены:

```
make, arc, findutils, node.js >= 6, sed, docker
```

Докер-клиент должен быть [залогинен в registry.yandex.net](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#cli)
и переменная окружения `REGISTRY_TOKEN` должна содержать [OAuth токен для работы с registry.yandex.net](https://wiki.yandex-team.ru/cocaine/docker-registry-distribution/#avtorizacija).

## Использование

Образы на основе Ubuntu с node.js имеют несколько характеристик:

- Версия Ubuntu (`OS` в make-командах) - напр. `trusty`, `xenial`.
- Версия node.js (`NODE`) - напр. `6`, `8`.
- Дополнительные параметры для сборки образов (`make build`) можно передать через `DOCKER_BUILD_OPTS`.

### Сборка новой версии

1. Устанавливаем зависимости:

    ```sh
    npm install
    ```

1. Делаем правки в папке образа `/src`.
1. Коммитим изменения.
1. Вливаем изменения в `trunk` через PR.

1. Смотрим на список изменений, чтобы выбрать тип увеличения версии. Образы `ubuntu-node` версионированы по [semver](https://semver.org/):

    ```sh
    make show-current-changelog OS=xenial NODE=10
    ```
1. Отводим новую ветку и поднимаем версию у образа:

    ```sh
    make (major|minor|patch)
    ```

1. Создаем PR, где подхватит CI и соберет образы:

    ```sh
    arc pr create --push --publish -M
    ```

1. Не забываем замержить, когда всё собралось.

Чтобы посмотреть статус сборки, необходимо перейти в PR и дождаться `success` статуса у `RELEASE_*`.

> Если вместо `success` вы видите `fail`, то нажмите на него, чтобы увидеть сломавшийся шаг. При нажатии на __Details__ можно увидеть логи и понять причину поломки.

Если в процессе вы понимаете, что необходимы дополнительные изменения, то делаем их и выполняем `make patch`. Пушим в тот же PR и ждем.

> **Важно**: весь процесс построен на обычных пользовательских ветках, в такие ветки могут пушить только авторы. Поэтому если вам необходимо пересобрать образ с чужими изменениями, то необходимо забрать нужные фиксы и повторить шаги от своего имени.

### Локальная сборка новой версии

Если хотим собрать и запушить образ локально, то необходимо выполнить следующую команду с такими же параметрами, с какими поднимали версию:

```sh
make clean release OS=xenial NODE=10
```

### Как пометить минимальную обязательную версию образа

```sh
make enforce OS=<ubuntu_name> NODE=<node_version>
```

### Как проверить работу образа локально

1. Сделайте фиктивное изменение в `versions.js` для интересующего вас образа
2. `make build REGISTRY_TOKEN=$QTOOLS_TOKEN SKIP_TAG_CHECK=1 OS= NODE=` (выбери свой `OS` и `NODE`)
3. `WORKDIR="/usr/local/app" docker run -w $WORKDIR -v $(pwd)/tests/app:$WORKDIR -e "MAPS_NODEJS_APP=$WORKDIR/app.js" -p 8080:80  -it registry.yandex.net/maps/ubuntu_xenial-node_14:$VERSION /start.sh` — `$VERSION` поменять на свою.

Чтобы зайти в поднятый контейнер:

```sh
# В соседнем терминале
docker ps
docker exec -ti <container_id> /bin/bash
```

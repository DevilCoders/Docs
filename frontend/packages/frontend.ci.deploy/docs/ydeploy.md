# Deploy в YDeploy

## Переменные окружения
- `DCTL_YP_TOKEN` - Токен авторизации для работы консольной утилиты `dctl`
- `AWACS_OAUTH_TOKEN` - Токен для авторизации awacs клиента для обновления балансера
- `DOCKER_IMAGE_TAG` - Тег для докер-контейнера (он должен уникальным для любого изменения стейджа. YDeploy не обновляет стейдж если повторно попытатся выложить один и тот же тег)
- `BETA_SLUG` - (Необязательный) Суффикс для беты (по умолчанию `pr-<номер пр>`)

Также вы можете указать любую переменную окружения, которую необходимо подставить в ваш конфиг и пакет будет искать её в `process.env`.

## Подготовка к деплою пулл-реквестных бет
Для пулл-реквестных бет нужно один раз создать в Ydeploy шаблонный stage. Далее в конфиге в поле `templateStageId` id этого stage'а. После этого для любой выкладки пулл-рекквестных бет будет использоваться конфиг этого stage. Если вы удалите шаблонный stage, то сломается выкладка бет. При изменении шаблонного stage'а изменения подтянутся только при создании новой беты. При обновлении беты будет использоваться конфиг стейджа ранее созданной беты. Это позволит настраивать стейдж беты через UI и не перезатирать его при каждой выкладке беты.

Также, если вам необходимо обновлять балансер, нужно добавить в конфиг шаблон для backend'а и upstream'а в поле `awacs`.

Пакет умеет создавать/обновлять/удалять stage(ydeploy), backend(awacs), upstream(awacs) если они указаны в конфиге.
 
### Файл с конфигом
#### Конфиг для YDeploy
Файл с конфигом для удобства может быть в YAML формате. Конфиг можно брать из dctl в yaml. При этом целиком в vcs хранить нельзя из-за delegation токенов. https://wiki.yandex-team.ru/deploy/#storestage.yaml

Конфиг выглядит следующим образом:
```yaml
type: 'ydeploy'
beta:
    templateStageId: <stage-id>
    stage:
        spec:
            ...
```
После получения шаблона stage, в него будут внесены все изменения из beta.stage. То есть будут перезаписаны все значения в шаблоне в соответствии с конфигом.

#### Конфиг для Awacs
Также в конфиг можно добавить информацию для создания/обновления backend, upstream в awacs.
В отличие от конфига стейджа, конфиги бекэндов и апрстимов мы можем хранить в vcs, поэтому их мы указываем полностью.

Тонкости хранения конфига для upstream:
* Конфиг для апстрима можно скопировать из интерфейса awacs в yaml, и положить к себе в конфиг.
Для более сложных конфигов, к примеру для FULL_MODE настоятельно рекомендуется использовать именно yaml (ключи в camelCase не будет работать).
Конфиг из ключа yaml будет передан как текст (как если бы вы его вставили в интерфейсе редактирования в awacs).
* (не рекомендуется) Для совместимости с предыдущими версиями можно класть конфиг апстрима в поле upstream.spec.config, в нем в ключах можно использовать как camelCase, так и snake_case. Но нет гарантии, что для сложного конфига это будет работать.

```yaml
type: 'ydeploy'
beta:
  ydeploy:
    <здесь может быть конфиг stage>
  awacs:
    namespace: <namespace-id>
    backends:
      - <здесь backend конфиг № 1>
      - <здесь backend конфиг № N>
    upstreams:
      - meta:
          auth:
            type: STAFF
            staff:
              owners:
                logins:
                  - <user-staff-login>
                  - <robot-login>
                groupIds:
                  - <abc-id>
          namespaceId: <namespace-id>
          id: <upstream-id>
        spec:
          labels:
            order: <order-number-text>
          type: YANDEX_BALANCER
          yandex_balancer:
              mode: <EASY_MODE2-или-FULL_MODE>
              yaml:
                  <сюда-и-далее-копируем-конфиг-из-awacs>
      - meta:
          auth:
            type: STAFF
            staff:
              owners:
                logins:
                  - <user-staff-login>
                  - <robot-login>
                groupIds:
                  - <abc-id>
          namespaceId: <namespace-id>
          id: <upstream-id>
        spec:
          labels:
            order: <order-number-text>
          type: YANDEX_BALANCER
          yandex_balancer:
              mode: <EASY_MODE2-или-FULL_MODE>
              yaml:
                  <сюда-и-далее-копируем-конфиг-из-awacs>
```

Для backend таких тонкостей не выявлено, поэтому их храним так (пример для бет Я.Командировок):
```yaml
type: 'ydeploy'
beta:
  ydeploy:
    <здесь может быть конфиг stage>
  awacs:
    namespace: trip.test.yandex-team.ru
    upstreams:
      - <здесь может быть upstream конфиг № 1>
      - <здесь может быть upstream конфиг № N>
    backends:
      - meta:
          auth:
            type: STAFF
            staff:
              owners:
                logins:
                  - <user-staff-login>
                  - <robot-login>
                groupIds:
                  - <abc-id>
          namespaceId: trip.test.yandex-team.ru
          id: ${BETA_SLUG}
        spec:
          selector:
            balancers: []
            gencfgGroups: []
            ypEndpointSets:
              - cluster: sas
                endpointSetId: tools_trip_stand-${BETA_SLUG}.front
              - cluster: vla
                endpointSetId: tools_trip_stand-${BETA_SLUG}.front
            nannySnapshots: []
            type: YP_ENDPOINT_SETS
            allowEmptyYpEndpointSets: false
```

### Как работает выкладка бет
1. Получаем id шаблонного stage для создания нового stage для пулл-реквеста
2. Создаем новый stage с указанием тега для докера из переменной окружения
3. Создаем (или обновляем ранее созданный) backend в Awacs с указанием stage пулл-реквеста
4. Создаем (или обновляем ранее созданный) upstream в Awacs. В нем указывем маску по которой будет доступна бета

### Как работает удаление беты
1. Удаляем upstream в Awacs
2. Удаляем backend в awacs
3. Удаляем stage в YDeploy

### Как работает выкладка тестинга
1. Создаем (или обновляем ранее созданный) stage в YDeploy в соответствии с конфигом
2. Создаем (или обновляем ранее созданный) backend в Awacs в соответствии с конфигом
3. Создаем (или обновляем ранее созданный) upstream в Awacs в соответствии с конфигом

### Примеры

* [Конфиг для беток и релиза](./examples/ydeploy/config.json)
* [Конфиг с билдом](./examples/ydeploy/with-build.json)
* [Конфиг для awacs](./examples/ydeploy/with-awacs.json)

### Полезные ссылки
https://wiki.yandex-team.ru/deploy/docs/
https://wiki.yandex-team.ru/deploy/docs/dctl/

### Build и push docker-образа

Если вам необходимо перед деплоем собирать и загружать docker-образ, то этот процесс можно автоматизировать. Для этого нужно добавить следующие секции в конфиг:
* секция описания вашего box'а в нужном окружении:
```json
    "name": "${DOCKER_IMAGE_NAME}",
    "registry_host": "${DOCKER_REGISTRY}",
    "tag": "${DOCKER_IMAGE_TAG}"
```
* секцию `build` в корне конфига ([пример](./examples/ydeploy/with-build.json)):
```json
    "build": {
        "dockerImageName": string; // путь в docker registry
        "dockerRegistry"?: string; // (default = "registry.yandex.net")
        "contextFiles"?: string[]; // список файлов и директорий, которые попадут в docker-образ, без опции попадут все
        "buildArgs"?: string[]; // список дополнительных аргументов для вызова `docker build`
    }
```

После добавления этих секций в конфиг необходимо добавить флаг `--build` к вызову команды `deploy` в ваших скриптах. Ваша команда будет выглядеть примерно так: `YENV=testing frontend-deploy deploy --config=.config/deploy/config.json --build`.

### Еще полезное
Для deploy units, которые хотим оставить без изменений, надо в конфиге указать
```
deploy_units:
    <deploy_unit_name>: {}
```

## <span style="color: red">Внимание</span>
Если не указать в конфиге существующие deploy units, то они будут потерты. Критично указать пустой конфиг для deploy units, изменение которых быть не должно

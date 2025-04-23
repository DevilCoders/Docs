# Stapler Deploy Tasklet

Тасклет для CI Arcadia.

Тасклет опубликован в registry
- [Registry](https://a.yandex-team.ru/arc/trunk/arcadia/ci/registry/projects/stapler)


##### Про CI в аркадии
- https://a.yandex-team.ru/arc/trunk/arcadia/ci

##### Основная документация по CI в аркадии
- https://a.yandex-team.ru/arc/trunk/arcadia/ci/docs

##### Quick-start по CI в аркадии
- https://a.yandex-team.ru/arc/trunk/arcadia/ci/docs/quick-start.md

##### Про тасклеты
- https://wiki.yandex-team.ru/sandbox/tasklets/

## Почему
Результатом работы приложений граф-генераторов является сам граф (`instance`) который должен быть опубликован в Nirvana.
Соответственно требуется исполнить собранный бинарник `graph_generator` с определенными параметрами и секретами, указать основное приложение `calculator`, секрет-токен, пулы и квоты, а так же определенный `mode` исполнения графа.

    Примечание: реализация граф-модов это ответственность разработчиков проектов граф-генераторов.
    В каких-то проектах их может вообще не быть.
    Мы рекомендуем закладывать возможность запуска графа в разных режимах для удобства тестирования и отладки.

Для таких действий не предусмотрен tasklet, поэтому нужно разработать собственный

## Тест
Для удобства тестирования тасклета в корне создан отладочный скрипт `run.sh` и `test_input.json`

> sh run.sh

```
echo 'YA MAKE'
ya make --yt-store -r

echo 'RUN TASKLET ON SANDBOX'
./deploy_tasklet run StaplerDeploy --input="$(cat test_input.json)" --sandbox-tasklet

```

## Публикация

После внесения изменений в код тасклета, необходимо его собрать и опубликовать новую версию

    ya make
    ./deploy_tasklet sb-upload --sb-schema

Дождать завершения публикации и полученный ID заменить в файле `~/arc/arcadia/ci/registry/projects/stapler/stapler_deploy.yaml`

> cat ~/arc/arcadia/ci/registry/projects/stapler/stapler_deploy.yaml
```
title: Stapler Deploy
description: Получает ресурс с собранным stapler приложением и запускает граф-генератор
maintainers: arakhmatulin

sources: market/monetize/stapler/infra/tasklets/deploy_tasklet
tasklet:
  implementation: StaplerDeploy

versions:
  stable: 1941128489
```

## Входные параметры

```
message ConfigVar {
    string name = 1;
    string value = 2;
    bool is_resource = 3;
    bool is_secret = 4;
    string secret_key = 5;
}

message Config {
    string resource_type = 1;
    repeated ConfigVar vars = 2;
    string kwargs_template = 3;
}

message Input {
    ci.TaskletContext ctx = 1;

    Config config = 2;
    repeated ci.SandboxResource sb_resources = 3;
}
```

Основную смысловую нагрузку несет массив `vars` объектов `ConfigVar` в объекте `input.config`

Из vars формируется словарь аргументов для шаблона команды `kwargs_template`

`is_resource` означает что в значении будет передаваться полное имя распакованноо файла из полученого архива ресурса `input.config.resource_type`

Парные аргументы `is_secret` и `secret_key` распаковывает значение секрета по ключу и подставляет в значение аргумента

## Выходные ресурсы

Объект Result со следующими полями

```
message Result {
    string status = 1;
    string message = 2;
    string link = 4;
    string workflow = 5;
}
```

## Пример использования

- [Stapler Example a.yaml](../../../example/a.yaml)


```
  input:
    config:
      resource_type: RESOURCE_TYPE_NAME
      kwargs_template: "{graph_generator} \
                    --calculator={calculator} \
                    --secret_name={secret_name} \
                    --yt_token={yt_token} \
                    --workflow_guid={workflow_guid} \
                    --quota=market-replenishment \
                    --pool=market-replenishment \
                    --proxy=hahn \
                    --log_level=INFO"
      vars:
        - name: graph_generator
          value: graph_generator
          is_resource: True
        - name: calculator
          value: calculator
          is_resource: True
        - name: yt_token
          value: sec-00002x1x2gksp0ayq2ayna0000
          is_secret: True
          secret_key: nirvana
        - name: secret_name
          value: some_nirvana_secret_name_token
        - name: workflow_guid
          value: e9ed8700-0000-47d5-0000-e57484e6090b
```


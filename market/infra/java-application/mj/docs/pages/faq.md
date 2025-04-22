# FAQ
## Как опробовать фреймворк?
Чтобы быстро создать папку с сервисом на MJ, достаточно воспользоваться командой [ya project create MJ](ya_project.md#ya-project-create-mj).

## Проблемы с oneOf в генераторе
На данный момент openapi-generator не [поддерживает inline oneOf](https://github.com/OpenAPITools/openapi-generator/issues/11932#issuecomment-1079621784). 
Поэтому чтобы воспользоваться oneOf, его необходимо объявить отдельно. Например, у вас была такая спека:
```yaml
CredentialOptions:
      type: object
      properties:
        secret:
          type: object
          additionalProperties: true
          oneOf:
            - $ref: '#/components/schemas/MiradoreCredentialFields'
            - $ref: '#/components/schemas/AWSCredentialFields'
            - $ref: '#/components/schemas/AzureClientSecretCredentialFields'
            - $ref: '#/components/schemas/AzureUsernamePasswordCredentialFields'
            - $ref: '#/components/schemas/CrowdstrikeCredentialFields'
            - $ref: '#/components/schemas/CensysCredentialFields'
            - $ref: '#/components/schemas/SNMPv2CommunitiesCredentialFields'
            - $ref: '#/components/schemas/SNMPv3CredentialFields'
            - $ref: '#/components/schemas/VMwareCredentialFields'
        [other properties omitted]
```
Она не сработает, так как oneOf объявлен внутри объекта, то есть inline. Вместо такой спеки можно написать следующее:
```yaml
CredentialFields:
      oneOf:
        - $ref: '#/components/schemas/MiradoreCredentialFields'
        - $ref: '#/components/schemas/AWSCredentialFields'
        - $ref: '#/components/schemas/AzureClientSecretCredentialFields'
        - $ref: '#/components/schemas/AzureUsernamePasswordCredentialFields'
        - $ref: '#/components/schemas/CrowdstrikeCredentialFields'
        - $ref: '#/components/schemas/CensysCredentialFields'
        - $ref: '#/components/schemas/SNMPv2CommunitiesCredentialFields'
        - $ref: '#/components/schemas/SNMPv3CredentialFields'
        - $ref: '#/components/schemas/VMwareCredentialFields'

    CredentialOptions:
      type: object
      properties:
        secret:
          $ref: '#/components/schemas/CredentialFields'
        [other properties omitted]
```

## Когда пытаюсь сделать наследование в openapi спецификации, то в сгенерированном коде получаю просто класс со всеми полями родителя, а хочу получить нормальное Java-наследование через extends
В openapi генераторе присутствует такая [проблема](https://github.com/OpenAPITools/openapi-generator/issues/8495) начиная с 5-й версии. Решение описано [там же](https://github.com/OpenAPITools/openapi-generator/issues/8495#issuecomment-797381399).
Нужно добавить в базовый класс `discriminator`
```yaml
discriminator:
  propertyName: className
  properties:
    className:
      type: string
```
Cамо поле заполнять необязательно.

## В какую папку в YD класть секреты?
`/app/datasources/properties.d`

## Трассировки в YD
В nanny файлы логов из `src/main/external/push-client.conf` парсятся и добавляются в конфиг пуш клиента `conf/push-client/market_health.yaml`
В деплое так не работает автоматически.
Есть хак:
добавить в переменную `PUSH_CLIENT_LOG_FILES` имена фалов с логами.
```
- env:
    - name: "PUSH_CLIENT_LOG_FILES"
      value:
        literal_env:
          value: "nginx/сервис-access-tskv.log,сервис/сервис.log,сервис/сервис-trace.log"
```
Пример: https://yd.yandex-team.ru/stages/testing_market_mbi-partner-registration/history/39/diff/40

## При локальном запуске тестов с рецептом через ya make -t падает с [ошибкой](https://paste.yandex-team.ru/5830306): _InvalidCommandError: Target program is not a file: <project_path>/src/test/test-results/src-test/pgsql/bin/pg_ctl (exists: False stat: None)_.
Удалить папку `~/.ya/build` и пересобрать проект

## Как убрать авторизацию\проверку TVM для конкретной ручки?
Необходимо реализовать [интерфейс](https://a.yandex-team.ru/arc_vcs/market/infra/java-application/mj/v1/mj-security/src/main/java/configurer/FrameworkWebSecurityConfigurer.java)
`web.ignoring(<path>)`

## Получаю ошибку java.lang.NoClassDefFoundError: ...
Перегенерировать проект и перезапустить идею

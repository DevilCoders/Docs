# HTTP API для управления джобами

## TeamCity
![Build Status](https://teamcity.yandex-team.ru/app/rest/builds/buildType:Market_Tools_TmsCoreQuartz2release/statusIcon)

## Публикация

Публикация либы производится после коммита в мастер автоматически через релизную машину:
https://tsum.yandex-team.ru/pipe/projects/jlibrary/delivery-dashboard/tms-core-quartz2-java-library

## Для пользователей библиотеки

### Подключение необходимой конфигурации к Spring контексту
для регистрации контроллера необходимо добавить импорт ru.yandex.market.tms.quartz2.config.TmsControllerConfig в Configuration class

```java
@Import(ru.yandex.market.tms.quartz2.config.TmsControllerConfig.class)
@Configuration
public class AppConfig{
}
```
По адресу `/tms/jobs` будут доступны следующие операции:

### Описание ручек

`GET /tms/jobs/ping` - возвращает `200 OK`

`GET /tms/jobs` - возвращает краткое описание джоб   

`GET /tms/jobs/full-info` - возвращает полное описание джоб (с JobDataMap)   

`GET /tms/jobs/running` - возвращает краткое описание запущенных в данный момент джоб   

`POST /tms/jobs/run` - незамедлительно запускает джобу   
jobGroup - optional   
```json
{
  "jobName": "simpleTrigger",
  "jobGroup": "DEFAULT"
}

```
`DELETE /tms/jobs` удаляет джобу   
jobGroup - optional   
```json
{
  "jobName": "simpleTrigger",
  "jobGroup": "DEFAULT"
}

```
`PUT /tms/jobs` - меняет cron expression джобы   
jobGroup - optional   
```json
{
  "jobName": "simpleTrigger",
  "jobGroup": "DEFAULT",
  "cronExpression": "0/1 * * * * ?"
}
```
### Unified Enrich Entry API

[UEE Wiki](https://wiki.yandex-team.ru/users/gavrilov-mi/uee/)

### Environment Properties to override for local run

```properties
UEE_YT_TOKEN=<your_yt_oauth_token>
UEE_STAFF_TOKEN=<your_staff_oauth_token>
```

Token stored in yav

### UEE API Specification

You can see spec [here](../uee-common/api.yaml) or swagger
ui [here](https://ir-ui.tst.market.yandex-team.ru/swagger-ui/index.html#/)

### UEE API Client Generation

If you want to generate api client, you need:

1. Add Inclusion file in your project.
   [Example for Java client](../../ir-ui/src/main/openapi-client-gen.inc)
2. Add INCLUDE operator in your ya.make file
   `INCLUDE(${ARCADIA_ROOT}/<path_to_your_project>/openapi-gen.inc)`
3. Rebuild project and reload IDE

Standard configuration of Java client

```json
{
    "library": "resttemplate",
    "dateLibrary": "java8",
    "hideGenerationTimestamp": "false"
}
```

Generator configuration options can be
found [here](https://github.com/OpenAPITools/openapi-generator/tree/master/docs/generators) for different languages. For
example, [Java client options](https://github.com/OpenAPITools/openapi-generator/blob/master/docs/generators/java.md)



### Поддерживается OAuth авторизация

Токен получать тут 
https://oauth.yandex-team.ru/authorize?response_type=token&client_id=1d8711512ae2492896b8437885875c94

При походе в сервис надо добавлять заголовок с полученными токеном
пример запроса
curl https://uee-api.vs.market.yandex.net/uee/api/users -H "Authorization: OAuth %%TOKEN%%"
 

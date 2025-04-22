Swagger support for akka-http (sort of fork of [swagger-akka-http](https://github.com/swagger-akka-http/swagger-akka-http))

## How to use

### Serve swagger-ui static content
Add `ru.yandex.vertis.akka.http.swagger.SwaggerHandler` to your routes (usually as `/swagger`)

```
private val swaggerHandler = new SwaggerHandler
val route = {
        *your root routes*
    } ~ pathPrefix("swagger") {
      swaggerHandler.route
    }
```

### Serve swagger json api description
Implement `ru.yandex.vertis.akka.http.swagger.SwaggerApiInfoHandler` and add it's `route` to your akka-http routes

```
class ApiInfoHandler extends SwaggerApiInfoHandler {

  val apiTypes: Seq[Type] = Seq(
    typeOf[ApiInfo],
    typeOf[SessionsHandlerDoc],
    typeOf[UsersHandlerDoc]
  )

}
```
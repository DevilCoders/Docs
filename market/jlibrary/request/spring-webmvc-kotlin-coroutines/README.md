Реализация ServletInvocableHandlerMethod, которая для всех запросов, для всех suspend методов-обработчиков запроса создает корутину с трассировочным контекстом

Подключать примерно так:
```kotlin
@Configuration
class WebMvcContextConfig : WebMvcRegistrations {

    override fun getRequestMappingHandlerAdapter(): RequestMappingHandlerAdapter {
        return object : RequestMappingHandlerAdapter() {
            override fun createInvocableHandlerMethod(handlerMethod: HandlerMethod): ServletInvocableHandlerMethod =
                CoroutineServletInvocableHandlerMethod(handlerMethod)
        }
    }
}
```

### Новый способ проверять запросы из браузера

#### Запуск DevTools и запись запросов

Появились два новых модуля - [DesktopDevToolsTestsModule](../desktop-web-client/src/main/java/ru/auto/tests/desktop/module/DesktopDevToolsTestsModule.java)
и [MobileDevToolsTestsModule](../desktop-web-client/src/main/java/ru/auto/tests/desktop/module/MobileDevToolsTestsModule.java)  
Внутри них подключена рула [DevToolsResource](../desktop-web-client/src/main/java/ru/auto/tests/desktop/rule/DevToolsResource.java)
и [DevToolsManager](../desktop-web-client/src/main/java/ru/auto/tests/desktop/managers/DevToolsManager.java)

Рула стартует DevTools и начинает записывать все запросы через `DevToolsManager`, внутри которого и хранится экземпляр самих DevTools и список всех запросов  
Если в тестах или степах нужны запросы или сами DevTools, то нужно инжектить `DevToolsManager` и вызывать там методы `getDevTools()` и `getAllRequests()`

```java
@Inject
private DevToolsManager devToolsManager;

DevTools devTools = devToolsManager.getDevTools();
List<Request> requests = devToolsManager.getAllRequests();
```

Запросы пишутся в список в отдельном потоке, который активен до тех пор, пока тест не закончится или не будет вызван метод `devToolsManager.stopRecordRequests()`  
Т.к. это отдельный поток и те или иные запросы постоянно отправляются, то рекомендую использовать awaitility :)

Так же есть [SeleniumMockSteps](../desktop-web-client/src/main/java/ru/auto/tests/desktop/step/SeleniumMockSteps.java),
в котором вспомогательные методы. Например, там есть метод `assertWithWaiting()`, который как раз оборачивает ассерт в awaitility

#### Проверка, что среди запросов есть нужный

Появилось 3 новых матчера - [RequestsMatcher](../desktop-web-client/src/main/java/ru/auto/tests/desktop/matchers/RequestsMatcher.java), 
[RequestHasBodyMatcher](../desktop-web-client/src/main/java/ru/auto/tests/desktop/matchers/RequestHasBodyMatcher.java)
и [RequestHasQueryItemsMatcher](../desktop-web-client/src/main/java/ru/auto/tests/desktop/matchers/RequestHasQueryItemsMatcher.java)  
Первый, `RequestsMatcher`, основной. Он применяется к списку запросов и принимает в себя другие матчеры, который работают с конкретным запросом.  
В простом виде это выглядит вот так
```java 
assertThat(devToolsManager.getAllRequests(), onlyOneMetricsRequest(hasSiteInfo("click=button")))
```
Тут написано, что в списке всех запросов должен быть только один запрос в метрику, у которого есть site-info click=button (проверится containsString)  

В этом `RequestsMatcher` есть метод как для общей метрики, так и для метрики кабинета. И метод, который принимает произвольный URL

#### Хорош теории, давай рассказывай как тесты писать?

Тут есть несколько простых шагов:
1. Подключаешь модуль `DesktopDevToolsTestsModule` или `MobileDevToolsTestsModule`
2. Инжектишь `SeleniumMockSteps`
3. Делаешь все нужные для теста действия
4. Вызываешь в конце 
```java
seleniumMockSteps.assertWithWaiting(onlyOneMetricsRequest(
        hasSiteInfo("{\"garage\":{\"banner\":{\"yandex_market\":{\"popup\":{\"show\":{}}}}}}")
))
```

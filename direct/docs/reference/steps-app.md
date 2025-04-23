## Приложение steps
#### Полезные ссылки
[Репозиторий](https://a.yandex-team.ru/arcadia/direct/apps/test-steps)
[Steps на ТС](http://direct-steps-test.in.yandex.net/docs/swagger-ui.html#!)
[Steps на Devtest](http://direct-steps-devtest.in.yandex.net/docs/swagger-ui.html#!)
[Steps на Dev7](http://direct-steps-dev7.in.yandex.net/docs/swagger-ui.html#!)

### Для чего нужно приложение
У нас есть фронтовые тесты, которые должны проверять какую-то функциональность кусочков Директа.
Для этого им необходимо, чтобы у клиента был определенный набор данных, например, полностью запущенные кампании определенных типов.
Создавать это все в тестах через интерфейс — долго, дорого и плохо (если будет ошибка, например, на этапе создания кампаний, все тесты просто упадут на ней, хотя могли бы на уже созданных кампаниях проверять сценарии не связанные с созданием).
Таким образом родилось это приложение — набор REST-ручек для подготовки тестов данных.
Кроме того, благодаря swagger-интерфейсу, можно пользоваться степами и при ручном тестировании

### Концепция
Раньше уже было аналогичное приложение со схожей функциональностью — [direct-steps-proxy](https://wiki.yandex-team.ru/users/ssdmitriev/direct-steps-proxy/)
Оно предоставляло доступ к “старым”, времен автоматизаторов, степам. Но с ними большая проблема — их надо поддерживать и расширять, а про это и забыть могут, да и дополнительные  нетривиальные действия приходится делать.
Новое приложение, по идее, самоподдерживающееся.
Основная идея — давать доступ к тем степам, которые бекендеры используют в своих CI тестах.
Эти степы активно используются, если в них требуется что-то поправить, это будет происходить вместе с правками кода.
Так как все в рамках единого IDEA-проекта, сломать test-steps незаметно, не так-то просто.

Фактически, test-steps это обертка над бекендными [степами](https://a.yandex-team.ru/arc_vcs/direct/core/src/test/java/ru/yandex/direct/core/testing/steps/Steps.java)

### Как запустить локально
Чтобы запустить приложение steps локально надо
1. Выкачать проект Директа (см. https://wiki.yandex-team.ru/Direct/Development/Java/QuickStart/#dljaarc)
2. Настроить окружение (см. https://docs.yandex-team.ru/direct-dev/guide/dev/back-first-steps)
3. Запустить основной класс приложения [TestStepsApp](https://a.yandex-team.ru/arcadia/direct/apps/test-steps/src/main/java/ru/yandex/direct/teststeps/TestStepsApp.java)

Если все настроено и запущено верно, то можно посмотреть и потыкать [swagger локально запущенного приложения](https://local-direct.yandex.ru:8443/docs/swagger-ui.html#!).

### Релизы
Отдельных релизов “по расписанию” нет.
Если требуется довезти новые или обновленные степы до разработческих и тестовых сред, достаточно воспользоваться [NewCI для test-steps](https://a.yandex-team.ru/projects/direct/ci/releases/timeline?dir=direct%2Fapps%2Ftest-steps&id=deploy-layer-release)
[Инструкция по работе с NewCI в Директе](https://docs.yandex-team.ru/direct-dev/guide/releases/release-newci)

### Пример добавление степа
[Коммит с добавлением степа, который уже используется в тестах бекенда](https://a.yandex-team.ru/arcadia/commit/r9759526)
Примерный план действия для добавления степа, коорый уже используется в тестах бекенда
0. Проверить, нет ли уже подходящего степа(без комментариев)
0. Найти подходящий степ
0. Сделать или найти сервис в приложении steps, который будет вызывать этот степ
0. Написать или добавить контроллер, который будет дергаться фронтовыми тестами или через swagger

Далее расписано, что надо было сделать, чтобы добавить степ для добавления в базу нового еком-домена

#### Найти подходящий степ
Искать существующие степы надо начинать с класса [Steps](https://a.yandex-team.ru/arcadia/direct/core/src/test/java/ru/yandex/direct/core/testing/steps/Steps.java)
Найти подкласс типа "Фича"Steps.[java|kt]
И в нем поискать подходящий степ
В примере мне подошел [EcomDomainsSteps.java](https://a.yandex-team.ru/arcadia/direct/core/src/test/java/ru/yandex/direct/core/testing/steps/EcomDomainsSteps.java)
А степ/метод — addEcomDomain

#### Сделать или найти сервис в приложении steps, который будет вызывать этот степ
Так как раньше не было в приложении степов с еком-доменами, мне нужно было создать сервис — [EcomStepsService.kt](https://a.yandex-team.ru/svn/trunk/arcadia/direct/apps/test-steps/src/main/java/ru/yandex/direct/teststeps/service/EcomStepsService.kt)
Простой класс, который умеет пользоваться EcomDomainsSteps из ядровых степов и помечен аннотацией `@Service`.
В нем я добавил метод addEcomDomain, который буду вызывать из контроллера с передачей парметров, а сам он дергает ядровый степ.
Кроме того, я добавил этот сервис в [TestStepsService.java](https://a.yandex-team.ru/arcadia/direct/apps/test-steps/src/main/java/ru/yandex/direct/teststeps/service/TestStepsService.java) для единообразия вызова степов из контроллеров — в них не надо подключать сервисы по отдельности, достаточно подключить этот "метасервис", и из него доставать необходимые.

#### Написать или добавить контроллер, который будет дергаться фронтовыми тестами или через swagger
Осталось добавить контроллер, который непосредственно будет дергаться через swagger
Я добавил [EcomStepsController.kt](https://a.yandex-team.ru/arcadia/direct/apps/test-steps/src/main/java/ru/yandex/direct/teststeps/controller/EcomStepsController.kt)

Выглядит страшно, но большая часть — это служебный код. По большому счету все аннотации — копипаста, на что надо обратить внимание:
1. `@RequestMapping("/ecom")` — путь до контроллера
1. `@Api(value = "Контроллер для еком сущностей")` — человекопонятное описание того, за что контроллер отвечает
1. `@ApiOperation` — аннотация описывающая непосредственно метод контроллера, там есть человекопонятное описание метода(`value`), и имя метода (`nickName`)
1. `@PostMapping.path` — путь метода, по которому он будет доступен внутри контроллера
1. Собственно метод, который может делать какую-то валидацию и вызывать степ из сервиса написанного ранее

Когда все готово, можно запустить локально, как описано [выше](#kak-zapustit-lokalno)

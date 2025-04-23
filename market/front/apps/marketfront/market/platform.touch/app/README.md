<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
Страницы и виджеты

- [Pages](#pages)
  - [BasePage](#basepage)
    - [JsonPage](#jsonpage)
      - [JsonApiPage](#jsonapipage)
    - [HtmlPage](#htmlpage)
  - [RedirectPage](#redirectpage)
  - [StaticPage](#staticpage)
- [Widgets](#widgets)
  - [BaseWidget](#basewidget)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Pages

### BasePage

Расширяет: [stout.Page](https://github.yandex-team.ru/market/stout/blob/master/lib/node_modules/Page.js).

Предоставляет api:
* `<BasePage> checkSecretKey({String} sk)` — проксирующий вызов `user.checkSecretKey` + обработка ошибок;
* `<Response> resource({String} id, {Object} [params], {Boolean} [isMandatory=true])` — возвращает результат вызова ресурса с переданными и контекстными (debug-объект, contextId);
* `<Response> getWidget({String} name, {Object} [params])` — возвращает результат работы виджета через вызов ресурса `widgets.get`;
* `<Response> renderWidget({String} name, {Object} [params], {String} path)` — возвращает результат работы виджета + наложения шаблона через вызов ресурса `widgets.{name}View` (должен быть определён для переданного виджета);
* `<BasePage> log({String} message, {String} [level])` — проксирующий вызов `stout.log` + добавление контекстного префикса к сообщению (`this.getLogPrefix()`).

Методы, доступные для переопределения / расширения:
* `processError({Terror} error)` — обработка различных типов ошибок (рекомендуется только расширять);
* `<BasePage> debugError({Terror} error)` — отладка ошибки при включенном в конфиге режиме `debug`;
* `<String> getLogPrefix()` — контекстный префикс, который добавляется к логируемым сообщениям.

Добавляемые в `request` данные (доступны через `this.request.getData(param)`):
* `user` — инстанс класса `User`, проинициализированный для текущего запроса (также доступен через `this.user`);
* `domainZone` — домен первого уровня запрошенного хоста;
* `id` — уникальный id запроса (результат работы виджета `RequestId`).

Общая функциональность:
* установка общих заголовков ответа (`X-Content-Type-Options`);
* парсинг тела запроса с помощью `bodyParser` и актуализация объекта `request`;
* инициализация уникального id запроса;
* проверка на dump-режим работы (аналог 8080 в XScript, [см. dumper](/market/MarketNode/tree/master/app/modules/dumper.js));
* инициализация пользователя (авторизация + гео-информация);
* проверка авторизации, если установлен `pageData.authOnly`;
* запуск таймеров обработки запроса, логирование.

#### JsonPage

Расширяет: [BasePage](#basepage).

Переопределенные методы:
* `write({*} chunk)` — вызывает родительский `write` со значением `JSON.stringify(chunk)`.

Общая функциональность:
* установка заголовка (`Content-Type: application/json`);
* вызов родительского метода `checkSecretKey`.

##### JsonApiPage

Расширяет: [JsonPage](#jsonpage).

Тесты: `spec/pages/JsonApiPage`.

Является заменой xscript'ового роутера аяксовых запросов.
Вызывает метод страницы, переданный в `<Response> pageData.method` и обрабатывает результат его выполнения (формирует ответ согласно протоколу).

Методы, доступные для переопределения:
* `writeResult({*} data)` — проксирующий вызов `write` с предварительным формированием согласно протоколу успешной операции;
* `writeError({Error} error, {*} data)` — проксирующий вызов `write` с предварительным формированием согласно протоколу ошибки. При включенном в конфиге режиме `debug` добавляет в ответ информацию из `error`.

Переопределенные методы:
* `_finish` — анализирует результат работы вызванного метода страницы и передаёт его в `writeResult` или `writeError`;
* `processError` — для обратной совместимости со старым роутером устанавливается код ответа 200 для `BAD_REQUEST`;
* `getLogPrefix` — добавляет `pageData.method` к префиксу логирования.

Общая функциональность:
* добавление в очередь вызова метода, переданного в `pageData.method`;
* обработка результата его работы и формирование ответа.

#### HtmlPage

Расширяет: [BasePage](#basepage).

Тесты: `spec/pages/HtmlPage`.

Родительская страница для всех конечных страниц приложения с вёрсткой.
Требует передачи в `pageData` параметра `template`, содержащего путь к шаблону.

Предоставляет api:
* `<String> renderHtml(data, mode, args)` — возвращает результат шаблонизации, замеряет время.

Методы, доступные для переопределения / расширения:
* `<Object> getTemplateData()` — возвращает итоговые данные для передачи в шаблон (`this.registry` + `{tasks: this.getTasksResults()}`).

Переопределенные методы:
* `_finish` — отправить результат шаблонизации шаблона `pageData.template` и данных, полученных от `this.getTemplateData()`;
* `processError` — обрабатывает код `AUTH_REQUIRED` редиректом на страницу авторизации (хост берется из свойства `authHost` объекта `user`);
* `debugError` — при указанном в свойстве конфига `templates.error` пути к шаблону, осуществляет его рендер с переданными данными ошибки и отдаёт в ответе (dev only).

Общая функциональность:
* установка заголовков (`Content-Type: text/html`, `X-Frame-Options': SAMEORIGIN`);
* инициализация информации о браузере в объекте `user`;
* добавление в очередь виджетов, общих для всех страниц с вёрсткой (`CookieWprid`, `CookieClid`, `CookieUtm`);
* инициализация свойства `registry` для агрегации данных, которые будут переданы в шаблон;
* при включенном в конфиге режиме `debug` и наличия в запросе параметра `dd` добавить в шаблон `{errors: this.getTasksErrors()}` и флаг `page.dump`;
* после завершения работы очереди произвести шаблонизацию и отправить результат.

### RedirectPage

Расширяет: [stout.Page](/market/stout/blob/master/lib/node_modules/Page.js).

Тесты: `spec/pages/RedirectPage`.

Осуществляет внутренние редиректы.

Требует передачи в `pageData`:
* `{String} redirectTo` — имя страницы для редиректа;
* `{Object} redirectParams` — необязательно, дополнительные параметры для построения url. Примиксовываются к query-параметрам запроса.
* `{Object} redirectRule` — необязательно, дополнительные параметры для построения url. Для замены query параметра в path.
* `{string} redirectRule.key` — query параметры для замены.
* `{string} redirectRule.value` — path параметры для замены.

По умолчанию происходит редирект с кодом `301`.
В случае, если не переданы обязательные параметры или роутер не смог построить по ним url, осуществляется логирование ошибки с уровнем `error` и редирект на главную  с кодом `302`.

### StaticPage

Расширяет: [stout.Page](/market/stout/blob/master/lib/node_modules/Page.js).

Отдаёт статику (должен быть установлен route в конфиге).

Только для использования при разработке.

## Widgets

### BaseWidget

Расширяет: [stout.Widget](https://github.yandex-team.ru/market/stout/blob/master/lib/node_modules/Widget.js).

Предоставляет api:
* `<Response> resource({String} id, {Object} [params], {Boolean} [isMandatory=true])` — ссылка на `BasePage.prototype.resource`;
* `<Response> getWidget({String} name, {Object} [params])` — ссылка на `BasePage.prototype.getWidget`;
* `<BaseWidget> log({String} message, {String} [level])` — ссылка на `BasePage.prototype.log`.

Методы, доступные для переопределения / расширения:
* `processError({Terror} error)` — обработка различных типов ошибок (рекомендуется только расширять);
* `<String> getLogPrefix()` — ссылка на `BasePage.prototype.getLogPrefix`.

Общая функциональность:
* расширение `contextId` (добавляется `contextId` управляющей страницы или виджета);
* запуск таймеров работы виджета, логирование.

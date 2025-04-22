# Тестирование в fiji

В систему тестов сервиса входят:

* [unit-тесты для TypeScript кода](#unit-typescript)
* [unit-тесты для клиентского i-bem кода](#unit-ibemjs) **(legacy)**
* [unit-тесты для серверного priv.js кода](#unit-privjs) **(legacy)**
* [unit-тесты на bemhtml.js шаблоны](#unit-templates) **(legacy)**
* [hermione-тесты](#hermione-tests) для интеграционного тестирования.
* [hermione-команды](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/runner/hermione/commands/README.md) проектные команды для файлов `*.hermione.js`. Список не полный см https://st.yandex-team.ru/SAKHALIN-2740
* [e2e-тесты](#e2e-tests) для интеграционного тестирования на реальных данных.
* [e2e-команды](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/runner/hermione/commands-e2e/README.md) проектные команды для файлов `*.hermione.e2e.js`.
* [yaml сценарии](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/docs/yaml.md) для TestPalm.

## Запуск тестов

**Внимание:** Перед локальным запуском тестов нужно выполнить [Настройку среды](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/docs/common/settings).

Запуск каждого вида тестов выполняется отдельными командами:

```bash
fiji spec --help          # Запуск unit-тестов для TypeScript кода
fiji unit --help          # Запуск unit-тестов для серверных priv.js
fiji test --help          # Запуск unit-тестов для клиентского i-bem кода
fiji tmpl --help          # Запуск unit-тестов для шаблонов bemhtml.js
npm run hermione:local -- --help      # Запуск hermione-тестов (по умолчанию запускаются в локальном Selenium Grid)
fiji e2e --help           # Запуск e2e-тестов
```

Каждое изменение кода, отправленное в репозиторий сервиса в виде [Pull Request](https://github.yandex-team.ru/mm-interfaces/fiji/blob/dev/docs/pull-request.md) проходит цикл проверок автоматическими тестами при выполнении сборки проекта. Сборка упадет, если хотя бы один тест не прошел.

<a name="unit-typescript"></a>

## Запуск unit-тестов на TypeScript код

<a name="unit-typescript-jest"></a>

### Jest

Все новые тесты на typescript код в обязательном порядке должны писаться с использованием [Jest](https://jestjs.io/).

Jest тесты делятся на 2 вида:
1) тесты на серверный (nodejs) код, хранятся в файлах `*.server.jest.ts(x)`;
2) тесты на клиентский или полиморфный код, хранятся в файлах `*.jest.ts(x)`.

### Mocha (legacy)

**Пожалуйста, пишите тесты на [Jest](#unit-typescript-jest)!**

Данный вид тестов временно оставлен в проекте и со временем будет переписан на Jest, а mocha раннер будет удалён.

До появления тестов на Jest для тестирования typescript кода исполозовалась mocha + ts-node.

В данном случае тесты хранятся в файлах с расширением `*.spec.js` в директориях компонентов, рядом с соответствующими `*.ts(x)` файлами.

### Способы локального запуска

```bash
# Запуск всех тестов
fiji spec [options] [path...] # `path` — путь к тесту;  `options` — параметры запуска

# Доступные параметры
fiji spec --help

# Точечный запуск одного или нескольких тестов, выполняется указанием пути к файлу или директории с тестами
fiji spec <путь к тесту>

# Точечный запуск тестов для сервиса:
fiji spec images

# Точечный запуск тестов для платформы:
fiji spec images/desktop
```

<a name="unit-ibemjs"></a>

## Запуск клиентских i-bem unit-тестов (legacy)

Тесты представляют собой HTML-страницу, в которую добавлены нужный блок, тест и библиотеки тестирования. Файлы тестов имеют расширение `*.test.js` и хранятся в директориях блоков (БЭМ-сущностей), рядом с соответствующими `*.js`-файлами (например, `images/blocks-touch-phone/cbir-controller/cbir-controller.test.js`).

Способы локального запуска:

**Внимание** Перед запуском тестов необходимо установить [mocha-phantomjs](https://www.npmjs.com/package/mocha-phantomjs) `sudo npm install -g mocha-phantomjs`.

**QYP** Для работы phantomjs в QYP необходимо добавить строку ```export QT_QPA_PLATFORM=offscreen``` в ```~/.bashrc```

```bash
# Запуск всех тестов
fiji test [options] [path]  # `path` — путь к тесту;  `options` — параметры запуска

# Доступные параметры
fiji test --help

# Точечный запуск одного или нескольких тестов, выполняется указанием пути к файлу или директории с тестами
fiji test <путь к тесту>
```

Отчет с результатами тестирования отображается непосредственно в консоли или его можно просмотреть с помощью GUI, выполнив следующую команду:

```bash
open <images|video>/<touch-phone|desktop|...>/pages/common/common.test.html
```

См. также:
* [Общий гайд по unit-тестированию](https://wiki.yandex-team.ru/search-interfaces/testing/unit-test-guidelines)
* [FAQ по unit-тестированию и ошибки PhantomJS](https://wiki.yandex-team.ru/search-interfaces/testing/client)

<a name="unit-privjs"></a>

## Запуск серверных priv.js unit-тестов (legacy)

Тесты для серверных `priv.js`-шаблонов хранятся в файлах с расширением `*.test-priv.js` в директориях блоков (БЭМ-сущностей), рядом с соответствующими `*.priv.js` (например, `video/blocks-deskpad/head-stripe/head-stripe.test-priv.js`).

Способы локального запуска:

```bash
# Запуск всех тестов
fiji unit [options] [path...]  # `path` — путь к тесту;  `options` — параметры запуска

# Доступные параметры
fiji unit --help

# Точечный запуск одного или нескольких тестов, выполняется указанием пути к файлу или директории с тестами
fiji unit <путь к тесту>

# Запуск тестов commonjs модулей(*.test-common.js)
fiji unit <путь к тесту> --modules
```

Отчеты с результатами тестирования отображаются непосредственно в консоли.

См. также:
* [Гайд для разработки тестов](https://wiki.yandex-team.ru/search-interfaces/testing/priv-js/#kaknachat)
* [Полезные ссылки](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/unit-priv/intro)

<a name="unit-templates"></a>

## Запуск unit-тестов на шаблоны bemhtml.js (legacy)

Тесты для шаблонов хранятся в директории `block.tmpl-specs`, например `video/blocks-touch-phone/b-page/b-page.tmpl-specs`.

Способы запуска:
```bash
# Сборка и запуск всех тестов
fiji tmpl

# Сборка и запуск всех тестов в картинках
fiji tmpl -b images

# Сборка и запуск тестов на b-page в video/touch-phone
fiji tmpl b-page -b video/touch-phone

# Доступные параметры
fiji tmpl --help
```

Чтобы создать новый тест необходимо:
* создать директорию `block.tmpl-specs`;
* создать внутри директории файлы `10-testname.bemjson.js` с необходимым BEMJSON;
* запустить `fiji tmpl block --save`.

Особенность технологии сохранения эталонов заключается в том, что первый прогон с опцией `--save` приведёт к падению тестов в случае, если вы создаёте или обновляете эталон. Не стоит этого пугаться. Последующий запуск `fiji tmpl block` отработает без ошибок.

См.также:
* [wiki SERPa](https://wiki.yandex-team.ru/search-interfaces/testing/templates/)
* [технология ENB](https://github.com/enb/enb-bem-tmpl-specs/)

<a name="hermione-tests"></a>

## Запуск hermione-тестов

Интеграционные тесты используются для проверки работы бизнес-логики сервиса и взаимодействия между блоками. Выполняются путем эмуляции действий пользователя в браузере.

[TestCop](https://testcop.si.yandex-team.ru/skips/hermione/fiji)

Тесты хранятся в корне репозитория fiji в папке с фичами [features](https://github.yandex-team.ru/mm-interfaces/fiji/tree/dev/features) в файлах с раcширением `*.hermione.js`. Например, `features/images/desktop/cbir/cbir.hermione.js`.

Метод assertView делает и складывает скриншоты в папку с вашей фичей. Наример, `features/images/desktop/<название блока>/screens/<хеш тест-кейса>/<браузер>/<состояние>.png`.

**Поскольку название папки конкретного тест-кейса генерируется из его названия, необходимо переснимать скриншоты каждый раз после его изменения!**
Например, `it('Что-то там')` изменился на `it('Что-то там еще')`. Хеш, расчитываемый из названия тест-кейса тоже изменился, так что теперь скриншоты должны лежать в другой папке. Необходимо их переснять.

Способы запуска:

**Внимание** Перед запуском тестов в локальном Selenium Grid необходимо запустить в отдельной вкладке [Selenium-сервер](#selenium-set). По умолчанию тесты запускаются в удалённом Selenium Grid.

```bash
# Запуск всех тестов (локальный)
npm run hermione:local -- [options] [test]  # `tests` — путь к тесту;  `options` — параметры запуска

# Доступные параметры
npm run hermione:local -- --help

# Запуск всех тестов для определенного сервиса и платформы с воспроизведением дампов
npm run hermione:local -- --service=images --platform=desktop --play

# Запуск теста с созданием новых дампов
npm run hermione:local -- --service=video --platform=touch-phone --create

# Запуск теста с перезаписью дампов
npm run hermione:local -- --service=video --platform=touch-phone --save

# Точечный запуск одного или нескольких тестов, выполняется указанием пути к файлу или директории с тестами
npm run hermione:local -- --browser=desktop-chrome --play features/images/desktop/cbir/cbir.hermione.js

# Запуск тестов в локальном Selenium Grid, выполняется с использованием опции `--local-grid`
npm run hermione:local -- features/images/desktop --play --browser=desktop-chrome --local-grid --base-url yandex.ru
```

Так же при запуске `hermione` тестов можно задать/изменить [экспериментальные флаги](https://wiki.yandex-team.ru/search-interfaces/experiments/).

[Установка экспериментальных флагов локально](https://github.com/gemini-testing/url-decorator)
[Установка экспериментальных флагов в TeamCity](https://github.yandex-team.ru/search-interfaces/docs/blob/master/testing/hermione/nightly_serp.md#Установка-дополнительных-флагов)

После запуска тестов автоматически будет поднят SSH-тоннель в грид и запустится выполнение тестов в нужном браузере.

Отчет о результатах тестирования отобразится непосредственно в консоли.

См. также:
* [Документация Hermione](https://github.com/gemini-testing/hermione)
* [Пост в Этушке о снятии скриншотов в Hermione](https://clubs.at.yandex-team.ru/search-interfaces-serp/1635)
* [Гайд по разработке hermione-тестов](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/e2e-wd#lokalnyjjzapusk)
* [Практики разработки hermione-тестов](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/reliabletests)
* [Функциональное тестирование интерфейсов](https://wiki.yandex-team.ru/search-interfaces/testing/hermione/)
* [Общий гайд по unit-тестированию](https://wiki.yandex-team.ru/search-interfaces/testing/unit-test-guidelines/)

### **Запуск теста с возможностью подключения по VNC к машине в гриде**

С помощью плагина `@yandex-int/hermione-debug` появилась возможность подключаться к удаленным машинам, но поддерживаются не все браузеры

Подробнее https://clubs.at.yandex-team.ru/search-interfaces/3142

Для запуска теста с возомжностью удаленного управления браузером, в конце команды `npm run hermione:local` нужно просто добавить через два дефиса, чтобы пробросить параметры в hermione, следующие парамеры:
```bash
-- --debug --debug-vnc-before-test true
```
После запуска теста на выполнение в консоли появится урл на VNC сессию.

Если в браузере недоступен VNC может быть доступна запись видео:

```bash
-- --debug --debug-record-video 1
```
После того как тест выполнится в консоли появится урл на видео.

Также не забыть отфильтровать запуск только одного теста в одном браузере, иначе поднимется одновременно несколько сессий.
Это следует добавлять до двух дефисов.
```bash
--grep '...' --browser touch-phone-chrome
```

Пример запуска:

```bash

npm run hermione:gui -- path/to/test.hermione.js --platform ... --grep '...' --browser ...  -- --debug --debug-vnc-before-test true
```

Полный список возможностей смотрите в `npx hermione -h`

<a name="e2e-tests"></a>

### Особенности использования команда webdriver после переезда на Hermione v4 (wdio v7)
Рекомендуется к прочтению пост [hermione + wdio@7](https://clubs.at.yandex-team.ru/devtools-frontend/182/)

Основные отличия:
* Тесты больше не поддерживают написание chaining-ом, они будут работать только в async/await синтаксисе.
* При получении результатов команд вместо объекта с ключем value приезжает реальный результат.
* Старые wdio4-команды все еще работают за счет [hermione-wdio-migrator](https://github.com/gemini-testing/hermione-wdio-migrator)

"Подводные камни" для тех кто привык работать со старыми командами:
* Во многих командах мигратора дефолтный таймаут 500мс, в некоторых тестах этого может быть недостаточно.
* Команды: getText , getAttribute , getCssProperty (и другие начинающиеся на get ) теперь ищут только первое вхождение переданного селектора, а не все.
  * Например: selectorExecute, getAttribute - команды ищут только первый элемент по селектору
  * Если все же нужно вызвать команду на нескольких элементах можно использовать хелперы: yaGetAttributes, yaGetTexts (можно написать или перетащить из web4 подходящие)
* **leftClick** - умела не принимать селектор, в миграторе селектор обязателен
* **chooseFile** - В новом API - только в хроме (который запущен в гриде)
* **execute** - не может принимать null в доп аргументы
  * Ожидаемые аргументы `(string|object|number|boolean|undefined)[]`
  * команда проверяет аргументы и выкинет ошибку, например если забыли [вызывать pageObject](https://jing.yandex-team.ru/files/ekurtaliev/2021-12-21_10.52.11-5dwCi.png) то [получите ошибку](https://jing.yandex-team.ru/files/ekurtaliev/2021-12-21_10.52.38-GT4h4.png)
* **orientation** - команды больше нет, но есть **setOrientation**, **getOrientation**
  * getter теперь возвращает текущую ориентацию капсом {LANDSCAPE|PORTRAIT}, учитывайте это при составлении условий
* **url** - работает не во всех браузерах, используйте **getUrl**
* Полезно заглядывать в код команд [hermione-wdio-migrator](https://github.com/gemini-testing/hermione-wdio-migrator) чтобы понять как они реализованы

## Запуск e2e-тестов

Помимо интеграционных тестов на дампах, существуют интеграционные тесты на реальных данных.

[TestCop](https://testcop.si.yandex-team.ru/skips/hermione-e2e/fiji)

Тесты хранятся в корне репозитория fiji в папке с фичами [features](https://github.yandex-team.ru/mm-interfaces/fiji/tree/dev/features) в файлах с форматом `*.hermione.e2e.js`.

Пример запуска:

```bash
# Запуск всех тестов для определенного сервиса и платформы
fiji e2e --service=images --platform=desktop

# Точечный запуск одного или нескольких тестов, выполняется указанием пути к файлу или директории с тестами
fiji e2e features/sakhalin/common/header/header.hermione.e2e.js
```

По умолчанию тесты запускаются на хосте: https://renderer-fiji-dev.hamster.yandex.ru.
Данный хост можно изменить с помощью использования параметра url, например:

```bash
fiji e2e --url=https://hamster.yandex.ru
```

Если ваша фича отсутствует в деве, и беты с этой фичей еще нет, то можно запустить тесты локально на темпларе, указав переменную среды окружения `templar_runner_enabled=true`:

```bash
 templar_runner_enabled=true fiji e2e
```

<a name="e2e-commands"></a>

## Запуск тестов в sandbox

Зачастую запустить большое количество тестов локально не получается либо их прогон слишко долог, можно запустить тесты в sandbox.

[Castle](https://github.yandex-team.ru/search-interfaces/infratest/tree/master/packages/castle)

Пример запуска:

```bash
$ npm run castle -- features/images/desktop/footer/footer.hermione.js --platform desktop touch-phone --service images --type hermione blockstat
Build 303746653 created, waiting subtasks creation: https://sandbox.yandex-team.ru/task/303746653
Started hermione platform:touch-phone, service:images https://sandbox.yandex-team.ru/task/303749514
Started hermione platform:desktop, service:images https://sandbox.yandex-team.ru/task/303749471
```

Тестируется **последний коммит**. Незакоммиченные изменения не отправляются в sandbox.

## Как удалить неиспользуемые скриншоты или переименовать папку со скриншотами после переименования тест-кейса

Гермиона сохраняет скриншоты для тестов в папке с названием, равным первым 7 символам md5-суммы от полного названия тест-кейса в кодировке ASCII. Чтобы легко узнать о всех тест-кейсах и соответствующих им хешах в hermione-файле, можно запустить гермиону с опцией `--hash-stats 1`.

Например,

`fiji hermione --hash-stats 1 --service video --platform desktop features/video/desktop/promo-tooltip/exp/promo-tooltip-collections.hermione.js`

Пример вывода:

```
...
75d34ad Промо-залогин / на кнопке "добавить в коллекцию" В карточке сериала
963cfe8 Промо-залогин / на кнопке "добавить в коллекцию" В карточке фильма Внешний вид
28ad54d Промо-залогин / на кнопке "добавить в коллекцию" В карточке фильма Кнопка регистрации
...
```

Эту команду удобно использовать при изменении названия тест-кейса (например, при раскатке эксп. флагов, когда название эксперимента удаляется из названия тест-кейса).

Получив список хешей до и после изменения названия, можно переименовать соответствующие папки со скриншотами, лежащие рядом с hermione-файлом в папке screens

Если же нужно очистить все неактуальные скриншоты в какой-либо папке (например, при отрыве тестов), можно запустить команду `fiji validate-hashes --delete`.

Запуск без параметра `--delete` произведет только вывод неактуальных папок


## Другое

Для локального запуска hermione тестов —  [selenium grid](#selenium-set).
Для локального запуска клиентских unit-тестов — [mocha-phantomjs](https://www.npmjs.com/package/mocha-phantomjs).

<a name="templar-set"></a>

### Selenium Grid

[selenium grid](https://wiki.yandex-team.ru/selenium/) — кластер, узлы которого предоставляют различные версии браузеров под различными операционными системами. Применяется для запуска тестов и других задач, требующих автоматической симуляции работы пользователя с браузером.

Для использования selenium grid необходимо установить локальный [Selenium Standalone Server](https://www.npmjs.com/package/selenium-standalone) (из любого места файловой системы):

**Внимание:** Убедитесь, что у вас установлена последняя версия [Java](https://www.java.com/ru/download/mac_download.jsp).

```bash
npm i -g selenium-standalone
selenium-standalone install
```

Запуск Selenium-сервера:

```bash
selenium-standalone start
```

Тесты можно выполнять как в локальном, так и удаленном selenium grid. Запуск тестов в локальном selenium grid позволяет «вживую» видеть выполнение тестов: открытие страниц, клики на элементы и т. п.

Браузеры доступные в [локальном](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/e2e-wd/use-cases/.edit?section=2&goanchor=h-2) и [удаленном](https://selenium.yandex-team.ru/) selenium grid.

Обратите внимание, что по умолчанию hermione-тесты запускаются в удаленном selenium grid. Чтобы выполнить hermione-тесты в [удаленном Selenium Grid](https://selenium.yandex-team.ru/#quota/all), используйте опцию `--local-grid`.

Cм. также:
* [Документация Selenium](http://selenium2.ru/docs.html)
* [Установка и подключение Selenium-сервера](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/installselenium)
* [Известные проблемы](https://wiki.yandex-team.ru/search-interfaces/multimedia/test/e2e-wd/seleniumexception)

<a name="node-config-set"></a>

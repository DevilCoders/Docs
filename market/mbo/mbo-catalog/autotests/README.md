## Запуск ui тестов ##

UI тесты лежат в `autotests/src/integration-test/java/`.

Выполнить их можно:
1. из консоли командой `./gradlew autotests:integrationTest`
2. из IDEA выбрав для нужного теста команду `Run` в контекстном меню

По умолчанию тесты будут выполняться в яндексовском selenium grid (будет использоваться Firefox)
и будут проверять фронт `https://mbo-testing.market.yandex-team.ru`.

### Настройка url фронта который нужно тестировать ###

1. Создайте файл `autotests/src/main/resources/properties/99_anyname.local.properties` или используйте существующий.
2. В этом файле задайте в свойствах `mbo.view-x5.url` и `mbo.gwt.url` url-ы на тестируемый фронт
(соответственно верстка и gwt).

Пример `99_anyname.local.properties`:
> ```
> mbo.view-x5.url=https://mbo.ayratgdl.user.derkoat.yandex.ru
> mbo.gwt.url=http://mbo-gwt-ayratgdl-braavos-36530.user.derkoat.yandex.ru
> ```

### Запуск тестов в локальном браузере ###

1. Скачайте `webdriver` соответствующий браузеру в котором вы хотите выполнять тесты. При необходимости распакуйте файл.
    * Firefox: [скачать WebDriver](https://github.com/mozilla/geckodriver/releases)
    * Opera: [скачать WebDriver](https://github.com/operasoftware/operachromiumdriver/releases)
    * Safari: в Mac OS лежит в `/usr/bin/safaridriver`
    * Yandex: используйте тот же WebDriver что и для Opera
2. Создайте файл `autotests/src/main/resources/properties/99_anyname.local.properties` или используйте существующий.
3. В этом файле задайте свойство `mbo.uitest.browsertype`. Допустимые значения:
    * `remote_firefox` - выполнение тестов в Firefox на яндексовском selenium grid (значение по умолчанию)
    * `local_firefox` - выполнение тестов в локальном Firefox
    * `local_yandex` - выполнение тестов в локальном Яндекс.Браузере
    * `local_safari` - выполнение тестов в локальном Safari
    * `local_opera` - выполнение тестов в локальной Opera

4. Если `webdriver` лежит в одной из директории переменной среды `${PATH}` то он будет найден автоматически.
Иначе нужно указать полный путь до него в свойстве `mbo.uitest.webdriver.path`
5. Если тесты запускаются для выполнения в Яндекс.Браузере и при этом браузер установлен
в директорию не по умолчанию, или тесты не видят браузер, то нужно явно указать путь
до браузера в свойстве `mbo.uitest.browser.path`
6. Если тесты запускаются для выполнения в Safari, то нужно в браузере разрешить удаленную автоматизацию.
Для этого в Safari активируйте пункт меню "Разработка" -> "Разрешить удаленную автоматизацию".



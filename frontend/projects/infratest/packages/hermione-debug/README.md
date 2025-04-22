# hermione-debug

Плагин для [hermione](https://github.com/gemini-testing/hermione), позволяющий дебажить тесты с использованием возможности [enableVNC](https://aerokube.com/selenoid/latest/#_live_browser_screen_enablevnc) и записывать видео прогона тестов с использованием возможности [enableVideo](https://aerokube.com/selenoid/latest/#_video_recording_enablevideo_videoname_videoscreensize_videoframerate_videocodec).
Подробнее почитать о плагинах можно в [документации](https://github.com/gemini-testing/hermione#plugins).

## Установка

```bash
$ npm install @yandex-int/hermione-debug --registry=http://npm.yandex-team.ru
```

## Использование

Необходимо подключить плагин в конфиге `hermione`:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-debug': {
            enabled: false, // Не нужно запускать debug по умолчанию

            // Перечислены значения по умолчанию, эти опции не обязательно указывать
            noTimeouts: false, // Выключить таймауты сессии и времени работы теста
            retryOnSuccess: false, // Перезапускать тест, если он завершился успешно
            vncOnFail: false, // Открывать VNC-клиент при падении теста
            vncBeforeTest: false, // Открывать VNC-клиент перед стартом теста
            pauseOnVnc: false, // Останавливать прогон теста после открытия VNC-клиента (enter для продолжения)
            recordVideo: false, // Записать видео прогона теста (ссылка будет выведена в лог)
            assignedCapabilities: { // Эти capabilities будут подмешаны к desiredCapabilities браузера
                'chrome-phone': {
                    version: 'phone-67.0-vnc',
                }
            },
            localVncProxy: { // Список браузеров, для которых VNC работает через проксирование VNC-трафика с удалённого сервера на локальный VNC-сервер
                safari13: { // Список опций, которые будут подмешаны в опции браузера, если включена или опция 'vncBeforeTest', или опция 'vncOnFail'
                    gridUrl: 'http://ios:ios@sg.yandex-team.ru:4444/wd/hub'
                }
            },
            browsers: /.*/ // Браузеры в которые необходимо добавить капабилити для дебага
        }
    },

    // ...
};
```

Здесь:

* `enabled` - плагин не делает ничего, если `enabled` установлен в `false`. По умолчанию равен `false`. Можно задать переменной окружения `hermione_debug_enabled=true` или опциями cli `--debug`, `--debug-enabled=true`.
* `noTimeouts` - выключить таймауты сессии и времени работы теста. Таймаут теста выключается полностью, sessionTimeout в desiredCapabilities устанавливается в 1h - текущее ограничение нашего grid'а, больше нельзя.
* `retryOnSuccess` - перезапускать тест, если он завершился успешно. Можно использовать, чтобы отлавливать падения плавающих тестов.
* `vncOnFail` - открывать VNC-клиент при падении теста.
* `vncBeforeTest` - открывать VNC-клиент перед стартом теста
* `pauseOnVnc` - останавливать прогон теста после открытия VNC-клиента (enter для продолжения)
* `recordVideo` - pаписать видео прогона теста (ссылка будет выведена в лог). Запись видео нагружает CPU, поэтому нельзя включать эту опцию при прогоне большого количества тестов. Видео хранятся одну неделю, после чего удаляются.
* `assignedCapabilities` - эти capabilities будут подмешаны к desiredCapabilities браузера.
* `localVncProxy` - список браузеров, для которых VNC работает через проксирование VNC-трафика с удаленного сервера на локальный VNC-сервер
* `browsers` (`RegExp`) - браузеры в которые необходимо добавить капабилити для дебага. По умолчанию матчится на все браузеры.

Все опции можно установить в конфиге, передать опциями командной строки или передать в переменной окружения:
```bash
hermione --debug-enabled=true --debug-vnc-before-test=1
hermione_debug_vnc_before_test=1 hermione_debug_enabled=true hermione
```

Для включения плагина можно использовать опцию cli `--debug`:
```bash
hermione --debug
```

Короткая опция `--debug` работает только в CLI.

Плагин добавляет три команды:

* `vncUrl()` - возвращает url с vnc-клиентом для текущей сессии.
* `openVnc()` - открывает новую вкладку с VNC-клиентом в браузере пользователя. VNC-клиент сразу после открытия подключается к текущей сессии в гриде.
* `waitForEnter(message)` - выводит сообщение в консоль и ожидает нажатия `Enter`. Аргумент `message` не обязателен.

### SurfWax

При использовании SurfWax вместо Selenium минимальный конфиг для плагина должен выглядеть следующим образом:

```js
module.exports = {
    // ...

    plugins: {
        '@yandex-int/hermione-debug': {
            novncUrl: "https://sw.yandex-team.ru/vnc",
            vncHost: "sw.yandex-team.ru",
            vncPathPrefix: "v0/vnc/",
            // ...
        }
    },

    // ...
};
```

### Поддерживаемые образы

Полностью поддерживаются:

* chrome десктопный, в том числе бразуеры "ipad" и "iphone" в web4 (десктопный chrome в режиме эмуляции)
* chrome мобильный, установленный в appium, начиная с версии 72
* searchapp, установленный в appium

Поддерживаются с ограничениями:

* edge - сервер VNC, установленный в образах с этим браузером, выдает 2-3 fps. https://st.yandex-team.ru/QAFW-2720
* chrome мобильный версии версии 67, установленный в appium

  Оригинальные образы с
  ```
  desiredCapabilities: {
      browserName: 'chrome',
      version: 'pad-67.0'
  },
  desiredCapabilities: {
      browserName: 'chrome',
      version: 'phone-67.0'
  }
  ```
  не поддерживаются. На их основе собраны образы с `version: 'vnc-pad-67.0'` и `version: 'phone-pad-67.0'`. Для использования этих образов при включенном плагине установите в настройках плагина:
  ```
  assignedCapabilities: {
      'appium-chrome-pad': {
          version: 'vnc-pad-67.0'
      },
      'appium-chrome-phone': {
          version: 'vnc-phone-67.0'
      }
  }
  ```
  Названия браузеров взяты из монорепо frontend, **на вашем проекте должны совпадать с именами браузеров, настройки которых нужно заменить**.

  В эту же категорию попадает браузер "searchapp" в web4 - мобильный хром в appium с измененным user-agent.
* firefox десктопный версии 64, есть проблемы с мышкой: https://st.yandex-team.ru/QAFW-2680
* safari в эмуляторе ios поддержан через проксирование VNC-трафика с удалённого сервера на локальный VNC-сервер

Не поддерживаются:

* ie11 - поддержки не будет: https://st.yandex-team.ru/QAFW-2641

### Примеры

* Посмотреть на прогон теста
  ```bash
  $ npm run hermione -- tests/hermione/suites/404-page/404-page.hermione.js --play -b linux-chrome --debug --debug-vnc-before-test 1 --debug-pause-on-vnc 1

  ...

  Плагин hermione-debug включен
  Плагин hermione-debug выключил параметр конфигурации mochaOpts.timeout
  Плагин hermione-debug установил capability sessionTimeout равную 1h

  ...

  Report-renderer запущен на порту 61539, pid: 17059
  Темплар запущен на порту 61524, pids: 17065
  VNC открыт. Нажмите Enter для продолжения.

  ...

  ```

* Записать видео прогона теста:
  ```bash
  $ npm run hermione -- tests/hermione/suites/404-page/404-page.hermione.js --play -b linux-chrome --debug --debug-record-video 1

  ...

  Плагин hermione-debug включен

  ...

  ✓ Внутренняя страница 404 проверка внешнего вида [linux-chrome:715231e3dd2f2b70bc48b6853735851ba03f2029a0352fdeedd6c9e14e9540ab] - 4975ms
  Видео доступно по адресу https://selenium.yandex-team.ru/video/715231e3dd2f2b70bc48b6853735851ba03f2029a0352fdeedd6c9e14e9540ab
  ```

* Запустить прогон теста, пока он не упадет, после чего открыть VNC:
  ```bash
  npm run hermione -- tests/hermione/suites/404-page/404-page.hermione.js --play -b appium-chrome-phone --debug --debug-no-timeouts 1 --debug-retry-on-success 1 --debug-vnc-on-fail 1 --debug-pause-on-vnc 1 --retry 1000

  ...

  Плагин hermione-debug включен
  Плагин hermione-debug выключил параметр конфигурации mochaOpts.timeout
  Плагин hermione-debug установил capability sessionTimeout равную 1h

  ...

  Тест завершился без ошибок. Плагин hermione-debug отправляет тест на retry.
  ⟳ Внутренняя страница 404 проверка внешнего вида [appium-chrome-phone:6674303ca1be6e75f36c50545b9e6e0a3eff6b35-ade6-431f-a641-0c1ff49a00e9] - 10015ms
  Will be retried. Retries left: 1000

  ...

  Тест завершился без ошибок. Плагин hermione-debug отправляет тест на retry.
  ⟳ Внутренняя страница 404 проверка внешнего вида [appium-chrome-phone:0ff3b8ff2240a4dca585438f6c4966051c6b7af8-942d-4a97-bb16-848417c3752b] - 8389ms
  Will be retried. Retries left: 999

  ...

  Тест завершился с ошибкой Error: Test error
      at Object.<anonymous> (/Users/slava-b/projects/customers/frontend/hermione-debug/services/tutor/tests/hermione/suites/404-page/404-page.hermione.js:7:19)
      at <anonymous>
      at process._tickDomainCallback (internal/process/next_tick.js:228:7). Открываю VNC.
  VNC открыт. Нажмите Enter для продолжения.
  ```

## Разработка

Инструкции по разработке самого плагина в [./development.md](./development.md)

# Настройка дебаггера для WebStorm

Интструкцию от JB можно найти тут: https://www.jetbrains.com/help/rider/Run_Debug_Configuration_Node_JS_Remote_Debug.html

Для настройки дебаггера для WebStorm'а нужно:
- открыть конфигурацию отладчика `Run | Edit Configurations |  Add New Configuration | Attach to Node.js/Chrome`;
- откроется окно подобного вида:
![](./webstrom-settings.png)

    - нужно проставить порт (если он изменился)
    - выбрать `--inspect` протокол
    - обязательно нужно указать путь до `realty-www` в `Remote URL` (т.е. путь вида `/home/<username>/www/<folder-name>/realty-www`)
- сохранить эти настройки, в дальнейшим достаточно будет использовать готовую конфигурацию;
- запустить отладку (нажать кнопку с жуком, `Debug '<имя конфигурации>'` или Shift+F9).

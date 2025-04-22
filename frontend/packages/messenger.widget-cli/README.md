![version](https://badger.yandex-team.ru/npm/@yandex-int/messenger.widget-cli/version.svg)<br>
[![dep health](https://oko.yandex-team.ru/badges/repo.svg?vcs=arc&repoName=frontend/packages/messenger.widget-cli)](https://oko.yandex-team.ru/repo/search-interfaces/frontend?repoFilter=packages/messenger.widget-cli)<br>
[![dep health](https://oko.yandex-team.ru/badges/pkg.svg?pkgName=@yandex-int/messenger.widget-cli)](https://oko.yandex-team.ru/pkg/@yandex-int/messenger.widget-cli)

# messenger.widget-cli

## Установка 
```
npm i @yandex-int/messenger-cli --registry=http://npm.yandex-team.ru
```

CLI для создания собственного js бандла виджета

## build

Для ручного запуска достаточно выполнить команду build с параметром -o

```
npx widget-cli build -o OUTPUT_FOLDER
```

Дальше cli попросит выбрать необходимые компоненты: базовый конфиг, ui, плагины.
При необходимости можно выбрать любое их количество.

Для запуска сборки из скрипта можно использовать параметры (подробнее npx widget-cli build --help)

Результатом выполнения команды будет `bundle.min.js`, а так же стили для каждого ui.
Пути к файлам и названия доступных модулей в бандле будут выведены в консоль после выполнения команды

Бандл транспилируется в `ES2015`. Полифилы Map/Set не включены.

## bundle.min.js
Содержит IIFE, при выполнения которой будет вызван колбек `__mssngrWidgetScriptCallback` (название можно поменять через параметр --callback) с аргументом:

```
{
    Widget,
    presets,
    config: {
        /*Выбранные конфиги*/
    },
    ui: {
        /*Выбранные фабрики интерфесов*/
    },
    plugins: {
        /*Выбранные плагины или фабрики плагинов*/
    }
}
```

## Подключение скрипта
Для бандла собранного следующей командой 
build -o ~/widget-bundle -u buttonUIFactory -c YandexConfig -p yandexUnreadCounterFactory

```js
(function() {
    window.__mssngrWidgetScriptCallback = function({
        Widget,
        presets,
        config: { YandexConfig },
        ui: { buttonUIFactory },
        plugins: { yandexUnreadCounterFactory }
    }) {
        const widget = new Widget(new YandexConfig({
            serviceId: SERVICE_ID,
        }));

        const unreadCounterPlugin = yandexUnreadCounterFactory();
        const ui = buttonUIFactory({
            unreadCounterPlugin
        });

        widget
            .addPlugin(unreadCounterPlugin)
            .setUI(ui)
            .init();

        ui.mount();
    };

    var
        node = document.getElementsByTagName('script')[0],
        script = document.createElement('script');

    script.async = true;

    script.src = PATH_TO_JS;

    node.parentNode.insertBefore(script, node);
})();
```
## Подключение стилей

Рядом с `bundle.min.js` будет лежать css файл/ы подключите нужный css любым способом

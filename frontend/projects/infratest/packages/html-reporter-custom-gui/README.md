# html-reporter-custom-gui

Пакет предоставляет набор функций, с помощью которых можно расширить `customGUI` в `html-reporter`. Каждая функция из пакета возвращает объект, который можно добавить в секцию `customGui` конфигурации плагина `html-reporter`.

## getDumpsCacheModeByIpbus

Позволяет менять режим чтения дампов `cacheMode` через шину межпроцессного взаимодействия `ipbus`.

Можно использовать в проектах, основанных на связке `archon` + `kotik`.

## getDumpsCacheModeByTemplarRunner

Позволяет менять режим чтения дампов `cacheMode` через плагин `templar-runner`.

Можно использовать в проектах, основанных на связке `templar-runner` + `templar`.

## Пример использования

Нужно установить пакет `@yandex-int/html-reporter-custom-gui`:

```
npm i @yandex-int/html-reporter-custom-gui --save-dev --save-exact
```

А затем поправить в конфиге гермионы конфигурацию плагина `html-reporter`:

```js
const { getDumpsCacheModeByIpbus } = require('@yandex-int/html-reporter-custom-gui');

plugins: {
    'html-reporter/hermione': {
        customGui: {
            ...getDumpsCacheModeByIpbus()
        }
    }
}
```
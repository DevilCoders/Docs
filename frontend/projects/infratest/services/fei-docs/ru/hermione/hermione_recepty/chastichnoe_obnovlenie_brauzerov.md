# Частичное обновление браузеров

## О проблеме

При выполнении обновления браузеров приходится сталкиваться со следующими проблемами:

- переснятие большого количества скриншотов делается долго, а вливание такого пулл-реквеста - ещё дольше
- хаки, сделанные для одних браузеров, ломаются для других
- для свежего браузера могут понадобиться свои хаки
- v-team, который хочет перейти на новый браузер, вынужден переводить на него весь проект

## Решение

### Переопределение версии браузера для конкретного теста/сьюта

Функциональность ядра hermione, которая позволяет переопределить версию браузера для конкретного теста или сьюта, является базой для решения проблемы. Она реализована через [хелпер](https://doc.yandex-team.ru/si-infra/hermione/hermione.html#version-browserversion):

```js
// Переопределяем версию браузера для всего съюта
hermione.browser('chrome-desktop').version('70.3');
describe('suite', function() {
    it('test 1', function() {...});

    // Переопределяем версию браузера для конкретного теста
    hermione.browser('chrome-desktop').version('70.1');
    it('test 2', function() {...});
});
```

### Переопределение версии браузера для группы тестов

Автоматическая замена версий браузера для тестов, обладающих определенным признаком, предоставляется плагином [hermione-browser-version-changer](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/hermione-browser-version-changer.html):

```js
module.exports = {
    // ...
    system: {
        plugins: {
            'hermione-browser-version-changer': {
                enabled: true,
                initStore: async () => {
                    // Подготавливаем словарь с произвольными признаками для разметки.
                    return {
                        'title-test1': 'tag1',
                        'title-test2': 'tag1',
                        'title-test3': 'tag2',
                    }
                }
                browsers: {
                    chrome: {
                        // Ключ '70.1' - версия браузера, значение - предикат
                        // Если функция вернет истинное значение, для браузера установится данная версия
                        '70.1': (test, version, store) => {
                            // test - текущий тест
                            // version - предлагаемая версия '70.1'
                            // store - словарь, который был подготовлен в методе initStore

                            // Установить 70.1 версию браузера если тест относится к "tag1"
                            return store[test.title] === 'tag1';
                        },
                        '80': (test, version, store) => {
                            return store[test.title] === 'tag2';
                        },
                    },
                }
            }
        }
    },
    //...
}
```

## Примеры

### Переопределение версии браузера для v-team в web4

Над web4 работает несколько v-team, и для того, чтобы команды могли обновлять браузеры независимо, была реализована следующая схема:

- [используется](https://github.yandex-team.ru/serp/web4/blob/dev/hermione/config.common.js#L351) плагин [hermione-browser-version-changer](https://doc.yandex-team.ru/si-infra/hermione/hermione_plaginy/hermione-browser-version-changer.html)
- в `initStore` происходит чтение v-team из yml-описаний сценариев при помощи [модуля](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/palmsync-specs-reader) и создание словаря "тест => v-team".
- в предикате для браузера проверяем, относится ли тест к нужному v-team

Итак, какие шаги нужно выполнить контуру для обновления браузера?

1. Отребейзить проект и установить свежие зависимости (для получения последних фич, упрощающих процесс обновления скриншотов)
2. В [конфиге hermione](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/hermione/config.common.js?rev=7312958#L374-382) добавить необходимую версию браузера, на которую собираетесь перевести ваш `v-team` (или модифицировать настройку уже существующей версии). Например, если вы хотите перевести тесты контуров `Velocity` и `Beauty` на firefox@79, то дифф будет такой:
![](https://jing.yandex-team.ru/files/sipayrt/2020-09-15T14%3A16%3A43Z.png)

   ⚠️  ВАЖНО: названия `v-team`-ов должны совпадать с указанными в yml-ах:
   ![](https://jing.yandex-team.ru/files/sipayrt/2020-09-15T14%3A41%3A30Z.png)

3. Запустить нужные тесты с помощью gui командой `npm run hermione:gui -- path/to/test/file.hermione.js --retry 1 --play --vteam=<vteamName>`
4. Провалидировать падения тестов и принять новые скриншоты

   Если среди запущенных тестов есть тесты, которые сходу не могут работать на новой версии, то такие тесты можно оставить запускаться на старой с помощью хелпера `hermione.browser('firefox').version('67');`:
   ![](https://jing.yandex-team.ru/files/sipayrt/2020-09-15T14%3A57%3A45Z.png)

   Старую версию браузера можно узнать в файле [browsers.js](https://a.yandex-team.ru/arc_vcs/frontend/projects/web4/browsers.js) в корне проекта

   Для тестов, которые не получилось сразу перевести на свежую версию, необходимо завести задачу в startrek-е в очередь вашего контура, пометив ее тегом `need_update`. Это нужно для того, чтобы контролировать перевод тестов на новые версии и не забывать про починку проблемных тестов. Данные задачи будут частью налоговой цели ["Покрытие тестами"](https://goals.yandex-team.ru/filter?user=21529&importance=0&goal=88387)


## Как подключить себе

 1. Убедиться, что версия hermione `v3.8.0` или выше.
 1. Убедиться, что версия html-reporter `6.0.0-alpha.12` или выше.
 1. Убедиться, что браузер доступен в гриде и добавлен в конфиге (пример [web4](https://github.yandex-team.ru/serp/web4/blob/dev/.hubby.conf.js))
 1. Убедиться, что последний стабильный ресурс `SELENIUM_PLATFORM_CONFIG` содержит декларацию нужного браузера. Если нет, то нужно [пересобрать](https://wiki.yandex-team.ru/search-interfaces/infra/grid-in-sandbox/#kakprotestirovatnovyjjobraz) ресурс.
 1. Использовать [хелпер](https://github.com/gemini-testing/hermione#versionbrowserversion) в тестах или [плагин](https://github.com/gemini-testing/hermione-browser-version-changer) для автоматизации.
 1. Установить и подключить [плагин](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/hermione-vteams-runner) на проект для запуска hermione c конкретным `v-team`.
 1. 🎉 Готово!

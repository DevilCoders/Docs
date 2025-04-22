# Настройка запуска hermione-тестов под флагами

## Ограничения и пререквизиты

- все источники `report-renderer` в графе должны получать в качестве одного из входов item с флагами (`type=flags`), который генерируется источником [FLAGS_MERGER](https://wiki.yandex-team.ru/jandekspoisk/sepe/dezhurnajasmena/servisy/flagsprovider/).
- шаблоны должны получать флаги из этого item аппхостового контекста
- девсервер - `kotik`

## Подключение

1. Убедиться, что пререквизиты выполнены.
1. При использовании пакетов ниже убедиться, что у этих пакетов версии такие или выше: 
    ```
    @yandex-int/archon-hermione@3.14.7
    @yandex-int/archon-renderer-devserver-command@5.4.0
    @yandex-int/kotik@2.1.0
    @yandex-int/hermione-exp-flags@0.1.2
    ```
1. Подключить в конфиге котика `.config/kotik/config.js` middleware [templateFlag](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/kotik#templateflag). Middleware должна быть расположена после получения данных (middleware `cacheReader` и `getData`) и до начала рендеринга (middleware `render`).
1. Подключить в `.hermione.conf.js` плагин [hermione-exp-flags](https://a.yandex-team.ru/arc_vcs/frontend/projects/infratest/packages/hermione-exp-flags).

## Legacy дампы templar

В некоторых проектах при миграции с templar на kotik остались старые дампы от templar. В этих дампах может не быть item с флагами.
В этом случае нужно доработать вашу локальную middleware `cacheReader`. Например, при конвертации дампов templar в формат котика добавить item так:

```javascript
function ensureFlags(sourceData, oldFlags = {}) {
    for (const answer of sourceData.answers) {
        for (const result of answer.results) {
            if (result.type === 'flags') {
                // Если флаги уже есть, то новые добавлять не нужно
                return;
            }
        }
    }

    sourceData.answers.push({
        name: 'FLAGS_MERGER',
        results: [{
            __content_type: 'yson',
            type: 'flags',
            binary: {
                all: {
                   ...oldFlags
                },
                type: 'flags',
            },
        }],
    });
}
```

Где `sourceData` - данные источника, а `oldFlags` - плоский объект с флагами. `oldFlags` нужно передавать только, если на проекте ранее уже использовались версточные флаги.

## Запуск

1. Перейти из PR в Trendbox UI

   ![Перейти из PR в Trendbox UI](../images/hermione-exp-flags-1.png)
2. Открыть список проверок для PR

   ![Открыть список проверок для PR](../images/hermione-exp-flags-2.png)
3. Открыть проверку с гермионой

   ![Открыть проверку с гермионой](../images/hermione-exp-flags-3.png)
4. Открыть задачу в Sandbox по ссылке с ID задачи

   ![Открыть задачу в Sandbox по ссылке с ID задачи](../images/hermione-exp-flags-4.png)
5. Склонировать задачу

   ![Склонировать задачу](../images/hermione-exp-flags-5.png)
6. Удалите значение параметра `Webhook url` (`webhook_url`), чтобы задача не прокрасила статусы проверок в Review Request в Arcanum

   ![Удалите значение параметра Webhook url](../images/hermione-exp-flags-6.png)
7. В конфиге задачи в поле `lifecycle.options.env` указать переменную среды окружения `ARCHON_KOTIK_TEMPLATE_FLAG` со значениями флагов в JSON, например, `"ARCHON_KOTIK_TEMPLATE_FLAG": "{\"react-page-result\": 1}"`

   ![Указать переменную среды окружения ARCHON_KOTIK_TEMPLATE_FLAG](../images/hermione-exp-flags-7.png)
8. Запустить задачу по кнопке Run

   ![Запустить задачу по кнопке Run](../images/hermione-exp-flags-8.png)

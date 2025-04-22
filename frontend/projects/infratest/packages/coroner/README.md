# coroner

Инструмент для обнаружения и диагностики проблем в конвейере.

## Источники, анализаторы и правила резолюции

Общий принцип работы:
- На вход передаются ссылки на источники информации о сборке / PR (id задачи в Sandbox, номер пулл-реквеста etc).
- С помощью анализаторов из источников извлекаются различные признаки (необязательно сигнализирующие о проблеме).
- На основе извлеченных признаков и правил определяются резолюции, описывающие проблему и ответственных.

## API

```js
const coroner = require('@yandex-int/coroner');

// Ссылки на источники.
const sourceRefs = [
    { type: 'sandbox_task_id', value: '<id>' },
];

const options = {
    sandbox: {
        // Опции для sandboxer'а.
        token: process.env.SANDBOX_AUTH_TOKEN,
    },
};

await coroner.investigate(sourceRefs, options);
=> [
    {
        // Признаки, извлеченные из источников.
        matched: [{
            // Источник.
            sourceRef: { type: 'sandbox_task_id', value: '<id>' },
            // Название признака.
            name: 'mq.merge_conflict.git',
            // Выдержка из лога.
            excerpt: {
                url: 'https: //proxy.sandbox.yandex-team.ru/<resource_id>/rebase-and-force-push.err.txt',
                data: '...CONFLICT (content): Merge conflict in...',
            },
        }],
        // Правило резолюции, подходящее под набор признаков.
        rule: {
            title: 'Невозможно отребейзить (конфликты)',
            clues: ['mq.merge_conflict.git'],
            actions: {
                setCause: { cause: "Merge conflict" },
                close: { resolution: "fixed" },
            },
        },
    },
]
```

## TODO

* [FEI-16068](https://st.yandex-team.ru/FEI-16068): Оторвать @types/retry из зависимостей (в package.json нельзя оставить комментарий)
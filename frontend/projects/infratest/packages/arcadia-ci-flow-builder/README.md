arcadia-ci-flow-builder
=======================

_TODO: https://st.yandex-team.ru/RENDERER-746_

Данный модуль предоставляет набор функций, которые берут на себя задачу провязки отдельных джобов в рамках сиайного флоу.

Мотивация - существующие флоу в CI могут быть достаточно сложными для того, чтобы править их вручную, в частности, в части корректной провязки отельных джобов. Более того, отдельные части таких флоу часто повторяются. Хочется иметь инструмент, который упростит композицию джобов или некоторых их сочетаний, а также автоматически выстроит необходимые связи между ними.

Изначально данный пакет разработан для создания и обновления сиайных флоу раскатки шаблонов report-renderer с помощью [`@yandex-int/renderer-templates-ci-flows`](../renderer-templates-ci-flows/) и [`@yandex-int/renderer-service-generator`](../renderer-service-generator/).

### Функции

Все предоставляемые пакетом функции по некоторым входным джобам или их комбинациям позволяют получить их комбинации, которые в свою очередь могут использоваться в дальнейших комбинациях. Все функции гарантируют отсутвие циклов в результирующих композциях, или бросают исключения при попытке создать композции с циклами.

#### connect

`connect(...Array<NamedJobDescription | FlowGraph>) => FlowGraph`

Принимает произвольный набор аргументов, которые могут быть как отдельными джобами с идентификаторами (объекты вида `{id: string, job: JobDescription}`, где для JobDescription ожидаются поля одноименные с полями джобов из Аркадийного CI), так и некоторыми их композициями. Заполняет массив needs переданных джобов в соответствии с порядком, в которым они были указаны и возвращает последовательную композицию джобов:

```ts
import { connect } from "@yandex-int/arcadia-ci-flow-builder";

const result = connect(
    {id: "job1", job: {task: "dummy"}},
    {id: "job2", job: {task: "dummy"}},
    {id: "job3", job: {task: "dummy"}},
);
```

приведет к такой структуре:

```ts
// result
{
    ins: new Set(["job1"]),
    outs: new Set(["job3"]),
    flow: {
        job1: {task: "dummy"},
        job2: {task: "dummy", needs: ["job1"]},
        job3: {task: "dummy", needs: ["job2"]},
    },
}
```

, которую мы и назвали композицией джобов. После получения финальной композции результирующий флоу может быть получен из свойства `flow`, после чего с ним может быть сгенерирован необходимый a.yaml файл, либо обновлен существующий, например, с помощью пакета [`@yandex-int/update-yaml`](../update-yaml/).

Далее такая структура может быть вновь передана в `connect` в перемешку с другими композициями и джобами, например:

```ts
const result2 = connect(
    {id: "job4", job: {task: "dummy"}},
    result,
    {id: "job5", job: {task: "dummy"}},
);

// result2:

{
    ins: new Set(["job4"]),
    outs: new Set(["job5"]),
    flow: {
        job1: {task: "dummy", needs: ["job4"]},
        job2: {task: "dummy", needs: ["job1"]},
        job3: {task: "dummy", needs: ["job2"]},
        job4: {task: "dummy"},
        job5: {task: "dummy", needs: ["job3"]},
    },
}
```

Одна и та же джоба может упоминаться в вызовах функций несколько раз, если это не противоречит требованию отсутствия циклов:

```ts
const jobA = { id: "a", job: dummyJob() };
const jobB = { id: "b", job: dummyJob() };
const jobC = { id: "c", job: dummyJob() };
const jobD = { id: "d", job: dummyJob() };

const result = connect(
    parallel(
        connect(
            parallel(jobA, jobB),
            jobC
        ),
        connect(jobA, jobD),
    )
);

// result

{
    ins: new Set(["a", "b"]),
    outs: new Set(["c", "d"]),
    flow: {
        a: {task: "dummy"},
        b: {task: "dummy"},
        c: {task: "dummy", needs: ["a", "b"]},
        d: {task: "dummy", needs: ["a"]},
    },
}
```

#### parallel

`parallel(...Array<NamedJobDescription | FlowGraph>) => FlowGraph`

Как и connect, принимает произвольный набор аргументов с джобами/композициями и возвращает сходную структуру, но отличается по способу композиции - для отдельных аргументов не модифицируется массив needs, что как бы воспроизводит параллельную комбинацию джобов, а лишь выставляются множества ins и outs для целей дальнейших композиций.

```ts
const result = parallel(
    {id: "job1", job: {task: "dummy"}},
    {id: "job2", job: {task: "dummy"}},
    {id: "job3", job: {task: "dummy"}},
);

// result
{
    ins: new Set(["job1", "job2", "job3"]),
    outs: new Set(["job1", "job2", "job3"]),
    flow: {
        job1: {task: "dummy"},
        job2: {task: "dummy"},
        job3: {task: "dummy"},
        job4: {task: "dummy"},
    },
}

const result2 = connect(
    {id: "job4", job: {task: "dummy"}},
    result,
    {id: "job5", job: {task: "dummy"}},
);

// result2:

{
    ins: new Set(["job4"]),
    outs: new Set(["job5"]),
    flow: {
        job1: {task: "dummy", needs: ["job4"]},
        job2: {task: "dummy", needs: ["job4"]},
        job3: {task: "dummy", needs: ["job4"]},
        job4: {task: "dummy"},
        job5: {task: "dummy", needs: ["job1", "job2", "job3"]},
    },
}
```

#### link

`link(...Array<NamedJobDescription | FlowGraph>) => FlowGraph`

Может служить для создания дополнительных связей в более общих флоу. Также как и `connect` соединяет переденные аргументы последовательно и выдает композицию, но эта композиция не имеет входов и выходов, в этой связи ее не имеет смысла использовать в составе других композций, кроме как композиции в parallel с другими джобами/композициями.

```ts
const job1 = {id: "job1", job: {task: "dummy"}};
const job2 = {id: "job2", job: {task: "dummy"}};
const job3 = {id: "job3", job: {task: "dummy"}};
const job4 = {id: "job4", job: {task: "dummy"}};

const result = parallel(
    connect(job1, job2),
    connect(job3, job4),
    link(job1, job4),
);

// result
{
    ins: new Set(["job1", "job3"]),
    outs: new Set(["job2", "job4"]),
    flow: {
        job1: {task: "dummy"},
        job2: {task: "dummy", needs: ["job1"]},
        job3: {task: "dummy"},
        job4: {task: "dummy", needs: ["job3", "job1"]},
    },
}
```

Также может служить для создания веток, которые не блокируют независящие от них вершины, что с использованием только `connect` или `parallel` не может быть выражено:

```ts
const job1 = {id: "job1", job: {task: "dummy"}};
const job2 = {id: "job2", job: {task: "dummy"}};
const job3 = {id: "job3", job: {task: "dummy"}};
const job4 = {id: "job4", job: {task: "dummy"}};
const job5 = {id: "job5", job: {task: "dummy"}};

const result = connect(
    parallel(
        connect(job1, job2, job3),
        link(job2, job4),
    ),
    job5
);

// result
{
    ins: new Set(["job1"]),
    outs: new Set(["job5"]),
    flow: {
        job1: {task: "dummy"},
        job2: {task: "dummy", needs: ["job1"]},
        job3: {task: "dummy", needs: ["job2"]},
        job4: {task: "dummy", needs: ["job2"]},
        job5: {task: "dummy", needs: ["job3"]}, // нет зависимости от job4
    },
}
```

#### transparent

`transparent() => FlowGraph`

Данная функция служит как средство дополнительной выразительности при составлении композиций джобов. Ее использование в композции эквивалентно ее отсутствию:

```ts
const result = connect(job1, condition ? job2 : transparent(), job3);

// в зависимости от значения condition будет составлен один из флоу
// result при condition === true
{
    ins: new Set(["job1"]),
    outs: new Set(["job3"]),
    flow: {
        job1: {task: "dummy"},
        job2: {task: "dummy", needs: ["job1"]},
        job3: {task: "dummy", needs: ["job2"]},
    },
}

// result при condition === false
{
    ins: new Set(["job1"]),
    outs: new Set(["job3"]),
    flow: {
        job1: {task: "dummy"},
        job3: {task: "dummy", needs: ["job1"]},
    },
}

// Альтернативный вариант, без использования transparent, является более многословным и менее очевидным для восприятия
const altResult = condition ? connect(job1, job2, job3): connect(job1, job3);
// Эффект усиливается при более сложных композициях
```

#### insertAfter

`insertAfter(FlowGraph, string, NamedJobDescription) => FlowGraph`

Принимает готовую композицию, имя джобы, после которой следует поместить новую, а также саму новую джобу. Все джобы, которые зависели от указанной, станут зависеть от новой. При необходимости `outs` будут соответственным образом обновлены. Вставляемая джоба не может быть уже существующей в графе, а также она не может иметь ссылки на другие существующие в графе вершины.

Предполагаемое использоваине - синхронизация независимых флоу в конкретных точках.

```ts
const job1 = {id: "job1", job: {task: "dummy"}};
const job2 = {id: "job2", job: {task: "dummy"}};
const job3 = {id: "job3", job: {task: "dummy"}};

const result = insertAfter(connect(job1, job2), "job1", job3);

// result
{
    ins: new Set(["job1"]),
    outs: new Set(["job2"]),
    flow: {
        job1: {task: "dummy"},
        job2: {task: "dummy", needs: ["job3"]},
        job3: {task: "dummy", needs: ["job1"]},
    },
}
```

#### insertBefore

`insertBefore(FlowGraph, string, NamedJobDescription) => FlowGraph`

Похожа на `insertAfter`, но вставляемая джоба помещается перед указанной.

```ts
const job1 = {id: "job1", job: {task: "dummy"}};
const job2 = {id: "job2", job: {task: "dummy"}};
const job3 = {id: "job3", job: {task: "dummy"}};

const result = insertBefore(connect(job1, job2), "job1", job3);

// result
{
    ins: new Set(["job3"]),
    outs: new Set(["job2"]),
    flow: {
        job1: {task: "dummy", needs: ["job3"]},
        job2: {task: "dummy", needs: ["job1"]},
        job3: {task: "dummy"},
    },
}
```


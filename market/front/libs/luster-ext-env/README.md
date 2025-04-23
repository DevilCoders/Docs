Расширение для ластера, позволяющее запускать дополнительные группы воркеров, прокинув им id группы.
Количество воркеров задаётся отдельно от конфига luster, что позволяет включать нужные группы воркеров, на разных машинах, имея одну кодовую базу.

luster-ext-env, проходит по папке, указанной в конфиге как `extEnvPath`, реквайрит файлы оттуда.
luster-ext-env содержит код как для мастера, так и для воркера.

Пример содержимого файла content-preview.json из этой папки:
```(json)
{
   workers: 2,
   env: "content-preview"
}
```

**luster-ext-env(master)** рассчитывает общее количество дополнительных воркеров, просуммировав workers в .json-файлах выше (пусть NN).

**luster-ext-env(master)** создаёт у себя внутри массив из NN элементов, в котором хранятся строки со значениями env из .json-файлов (пусть у нас 2 воркера на «content-preview» и 4 — на «market-preview»):
```(javascript)
[
   "content-preview",
   "content-preview",
   "market-preview",
   "market-preview",
   "market-preview",
   "market-preview"
]
```

**luster-ext-env(worker)** шлёт мастеру сообщение

```(javascript)
{
    cmd: "luster-ext-env config request",
}
```

В ответ на это сообщение, **luster-ext-env(master)** отдаёт `pop()` из массива выше; это либо строка, либо undefined:

```(javascript)
{
    cmd: "luster-ext-env config response",
    content: "content-preview"
}
```

**luster-ext-env(worker)** сохранит это значение в инстансе воркера. Оно будет доступно в коде воркера через `require('luster').extEnv`

В коде воркера можно проверять это значение и выполнять условный код. Например, реквайрить дополнительный конфиг.

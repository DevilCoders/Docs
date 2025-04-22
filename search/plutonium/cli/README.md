## Saas2 Command Line Interface

Команды

----

```shell
saas2 its-get
```

Посмотреть последний real time config для шардконтроллера

---

```shell
saas2 its-edit
```

Редактировать конфиг шардконтроллера, результат записать в базу

---

```shell
saas2 snapshots-size --metastream <str> --sequential-snapshots-number <int>
```

Парсит таблицу с метаинформацией runtimeFs, считает средний размер снепшота в рамках одного метасрима

##### Опции

`--metastream` - обязательная опция с названием метастрима, для которого нужно посчитать средний размер снепшота
`--sequential-snapshots-number` - если нужно посчитать размер `n` последовательных снепшотов

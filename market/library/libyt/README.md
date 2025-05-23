# libyt (combinator)

Полезные мелочи для работы с YT

## Uploader.h
Интерфейс и загрузка файлов.

## YtHelpers.h
Мелкие функции упрощающие работу с YT: создать клиента, создать таблицу, получить количество строк и т.п.

## YtTablesHasChanged.h
Библиотека позволяющая узнать изменилось ли что-нибудь по заданым путям с прошлого запуска

Пример использования:

```
TYtTablesHasChanged hasChanged(client, {"//table1" ,"//dir/table2"}, state);
if (hasChanged.HasChanges()) {
    // do something
    hasChanged.SetChange();
} else {
    // nothing to do
}
```

state - произвольный узел Кипариса (таблица), в котором хранится состояние таблиц на момент прошлого запуска.
Информация хранится в атрибутах. Можно хранить информацию о нескольких наборах таблиц в одном state (но лучще не злоупотреблять).

HasChanges() - проверяет было ли изменение
SetChange() - сохраняет текущие состояние в state

Чтение всех таблиц не происходит, учитываются косвенные данные, говорящие об изменениях:
* Размеров таблиц
* Количество записей в таблице
* Время модификации
* Сортированность (сам факт и по каким ключам)

Также:
* Если в путях будет директория, то она будет рекурсивно обойдена и будут учитываться изменения в любой таблицы в директории, а также добавление/удаление таблиц
* Если в путях будет симлинк, то он будет разименован. Изменение путя куда показывает симлинк тоже будет считаться изменением.

## YtReplicatedTable.h
Выделено в отдельную библиотеку market/library/libyt_yt_replicated_table

## YtScaler.h
Функция которая умеет множить данные в однотипных таблицах.

## YtStatistics.h
Набор функий для работы со статистикой джобов: безопасное извлечение значения параметра, удобный сбор статистики, запись статистик, дампинг в файл.

Полезно знать:
- [YT документация](https://yt.yandex-team.ru/docs/problems/jobstatistics)
- Пользовательские статистики -- асинхронный механизм, без четких гарантий, когда статистики доедут до шедулера.
- Количество пользовательских статистик ограничено 128-ю на один джоб.

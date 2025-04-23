## Вызов утилиты
```
labels_list;
```
Передача флага
```
list_mailbox(with-attaches);
```
Передача аргумента с сохранениме результата
```
list_folder(fid=$inbox.Fid threads-view) DEFINE $threads-in-inbox;
```

## Переменные
Результатом утилиты (она должна возвращать YAML) можно объявить переменную.
Её можно использовать как аргумент утилиты.
Если в переменной список, то в качестве аргумента берём его 1-ый элемент.

```
folder_list DEFINE $all-folders;
# допустимое поведение, когда не так важно какой именно fid передавать
list_folder(fid=$folders.fid);
```


### Выборка
```
DEFINE $inbox FROM $folders WHERE SymbolicName = inbox;
DEFINE $heavy-thread FROM $threads-in-inbox WHERE ThreadCount IS GREATEST;
```
### `RANDOM`
```
DEFINE $new-label-name FROM RANDOM NOT IN $labels.Name;
```

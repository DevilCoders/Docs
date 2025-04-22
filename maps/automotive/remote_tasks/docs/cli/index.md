## Заморожено и пока не планируется к разработке

### Требования
Собираем бинарь yauto-rt из Аркадии, который будем предоставлять пользователям ресурсом из сендбокса.
Пока видим нужду в следующей функциональности:

* Проверка авторизованности пользователя по токену или в обмен на ssh (который у всех и так должен быть).
* Сам доступ будет регулироваться через IDM.
* Можно отправить запрос на сбор логов для конкретной головы.
* Есть возможность отменить таску.
* Доступна выгрузка результата таски (или ошибки).
* Доступна выгрузка тасок и истории изменения их статусов с фильтрами по (пользователь или все пользователи), конкретной голове, конкретной таске, конкретному статусу таски (даты, лимит в будущем).

Также сейчас кажется, что если таска не смогла выполнится n (=3?) раз ее на сервере надо перевести в состояние canceled, если таска выполнилась с ошибкой (и мы смогли это поймать на клиенте), то переводим в состояние error.

### Примеры использования
#### Добавить таску
```
<< yauto-rt add report
>> New task queued
```

#### Выгрузка тасок для конкретной головы от текущего пользователя
```
<< yauto-rt list --head-id ABCD --all-users
>> Tasks with head-id=ABCD, all-users:
>> user \t head_id \t task_id \t type \t status \t time
>> alice \t ABCD \t 12343 \t report \t error \t 12:26 15.05.2020
>> alice \t ABCD \t 12345 \t report \t processed \t 12:36 15.05.2020
>> alice \t ABCD \t 12346 \t report \t canceled \t 12:41 15.05.2020
>> bob \t ABCD \t 12346 \t report \t requested \t 12:37 15.05.2020
```

#### Выгрузка тасок с конкретной головы в статусе processed или error
```
<< yauto-rt list --head-id ABCD --status error,processed
>> Tasks with head-id=ABCD, status=error|processed, current user:
>> user \t head_id \t task_id \t type \t status \t time
>> alice \t ABCD \t 12343 \t report \t error \t 12:26 15.05.2020
>> alice \t ABCD \t 12345 \t report \t processed \t 12:36 15.05.2020
```

#### Выгрузка инфы по конкретной таске
```
<< yauto-rt task --id 12343
>> Taskid=12343
>> Type=report
>> HeadId=ABCD
>> Creator=alice
>> Statuses=
>> status \t time \t description
>> queued \t 12:20 15.05.2020 \t
>> requested \t 12:25 15.05.2020 \t
>> requested \t 12:26 15.05.2020 \t
>> canceled \t 12:27 15.05.2020 \t by bob
```

#### Выгрузка результатов тасок
```
<< yauto-rt result --id 12345
>> <file with result>

<< yauto-rt result --id 12343
>> <file with error>

<< yauto-rt result --id 12346
>> Task was canceled
```


#### Отмена конкретной таски
```
<< yauto-rt cancel --id 12346
>> Canceled task with id=12346
```

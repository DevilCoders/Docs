# Sandbox-задача `YDB_RESTORE_TO_YT`
Эта sandbox-задача — бинарная. https://wiki.yandex-team.ru/sandbox/tasks/binary/

## Инструкция по обновлению кода:
Метод `on_execute` может быть проверен только через запуск бинарной задачи в sandbox.
Все остальные методы можно проверить в локальном sandbox.

### 1. Внести исправления

### 2. Прогнать тесты
```bash
ya make -tt sandbox/projects/kikimr/tasks/YdbRestoreToYt
```

### 3. Скомпилировать бинарь
**Сборка работает только под Linux.** Не пытайтесь собрать бинарь под MacOS
```bash
ya make --checkout sandbox/projects/kikimr/tasks/YdbRestoreToYt/bin
```

### 4a. Загрузить бинарь в sandbox
```bash
./sandbox/projects/kikimr/tasks/YdbRestoreToYt/bin/YdbRestoreToYt upload --attr target=sandbox/projects/kikimr/tasks/YdbRestoreToYt --attr release=test
```

### 4b. Запуск в локальном sandbox
_Костыль. Хак. Никаких гарантий. I have no idea what am I doing._ Используйте пункт 4а

```bash
./sandbox/projects/kikimr/tasks/YdbRestoreToYt/bin/YdbRestoreToYt run --no-auth --skynet --url "%sandbox_url" --tid %task_id --attr target=sandbox/projects/kikimr/tasks/YdbRestoreToYt --attr release=stable
```
* `%sandbox_url` — адрес вашего "локального sandbox". Например `http://my-lovely-dev-for-local-sandbox.yandex.net:13337`. На этом URL должен открываться интерфейс sandbox
* `%task_id` — id ранее запущенной задачи, из которой будут скопированы параметры. Задать параметры через аргументы `YdbRestoreToYt run` нельзя
* вместо `--tid %task_id` можно использовать `--template %scheduler_id`

### 5. Запустить задачу в sandbox
1. Создать задачу типа `YDB_RESTORE_TO_YT`
2. Выбрать в параметрах `YdbRestoreToYt binary type = test`
3. Запустить задачу

Все методы, кроме `on_execute`, будут взяты из транка. Изменения в этих методах можно проверить в локальном sandbox.

### 6. Код-ревью

### 7. Опубликовать бинарь в sandbox
```bash
./sandbox/projects/kikimr/tasks/YdbRestoreToYt/bin/YdbRestoreToYt upload --attr target=sandbox/projects/kikimr/tasks/YdbRestoreToYt --attr release=stable
```

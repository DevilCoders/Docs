# billing/library/go/template
Cookiecutter-шаблон проекта, использующего `billing/library/go/billingo`.

### Quickstart
1. `pip install cookiecutter`
2. В корне аркадии запустить: `cookiecutter billing/library/go/template -o <путь куда положить результат>/`
3. Вводим `project_name`. Разные слова следует разделить дефисами
4. Переменные `PROJECT_NAME`, `PROJECTNAME`, `projectname`, `ProjectName` переопределять не стоит, жмем `Enter` до сходимости.
    * Переменную `project_path` можно переопределить, если `<путь куда положить результат>` ≠ `billing`
    * Переменную `owner` можно переопределить, если проектом должна владеть группа, отличная от `billing`
5. Запустить `make yoimports` в корне проекта

### Что делать, если я вдруг хочу разрабатывать на `Python`?
Шаблон с похожими идеями: [mail/swat/template](https://a.yandex-team.ru/arc/trunk/arcadia/mail/swat/template)

### Как разрабатывать этот шаблон?
1. `cookiecutter template --no-input` - генерируем проект `example_project` со значениями по-умолчанию.
2. Работаем с `example_project`, отлаживаем на нем свои изменения.
4. Чистим `example_project` от бинарей: `find . -type l -delete`
5. `./uncut.sh example_project` изменит `example_project` так, чтобы он соответствовал директории
   `template/{{cookiecutter.project_name}}`.
6. Посмотрим на разницу: `diff -qr example_project template/\{\{cookiecutter.project_name\}\}`.
7. `cp -r example_project/* template/{{cookiecutter.project_name}}/`.
8. (Опционально) Проверяем, что `uncut` отработал правильно: `grep -ri example example_project`.


### Опциональное добавление файлов/директорий
Шаблон позволяет добавлять/удалять файлы и директории в зависимости от переменных cookiecutter.
Для этого используется `post hook`. Подробонее про хуки можно прочитать в [документации Cookiecutter](https://cookiecutter.readthedocs.io/en/2.1.1/advanced/hooks.html).
Post hook - это Python скрипт, который выполняется после создания шаблона.
Хук описан в `hooks/post_gen_project.py` и обрабатывает файл `manifests.yaml`, который лежит в корне шаблона.
Хук проходит по всем features по очереди и выполняет действие в зависимости от указанных переменных.
Хук поддерживает 2 типа действий:
- simple
  Это действие смотрит на поле `enabled` и если в нем `false`, то удаляет все файлы, перечисленные в `resources`.
- selector
  Это действие пытается сматчить значение в поле `selector` на значения в `resources`, если удается - то сохраняет указанный ресурс, а остальные удаляет, иначе удаляет все ресурсы.
  Селектор также поддерживает значение `none`, которое также удаляет все ресурсы.

После обработки всех действий, хук удаляет файл `manifests.yaml` из финального шаблона.

### Известные проблемы
1. Может случиться так, что из-за названия переменной, нарушится лексиграфический порядок в импортах. Это порушит `style`-тесты. Решение - 5 пункт из Quickstart.


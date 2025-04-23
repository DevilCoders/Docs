# mail/swat/template
Cookiecutter-шаблон проекта, использующего `mail/python/sendr-qtools`.


### Quickstart
1. `pip install cookiecutter`
2. `cookiecutter mail/swat/template`
3. Вводим `project_name`. Остальные переопределять не стоит.

### Что делать, если я вдруг хочу разрабатывать на `Go`?
Шаблон с похожими идеями: [billing/library/go/template](https://a.yandex-team.ru/arc/trunk/arcadia/billing/library/go/template)


### Как разрабатывать этот шаблон?
1. `cookiecutter template --no-input` - генерируем проект `example_project` со значениями по-умолчанию.
2. Работаем с `example_project`, отлаживаем на нем свои изменения.
3. Чистим `example_project` от бинарей: `find . -type l -delete`
3. `./uncut.sh example_project` изменит `example_project` так, чтобы он соответствовал директории
   `template/{{cookiecutter.project_name}}`.
4. Посмотрим на разницу: `diff -qr example_project template/\{\{cookiecutter.project_name\}\}`.
4. `cp -r example_project/* template/{{cookiecutter.project_name}}/`.
5. (Опционально) Проверяем, что `uncut` отработал правильно: `grep -ri example example_project`.


### Что означают `{##}` в именах файлов ya.make?
Это шаблонное выражение, которое на языке jinja2 означает пустой комментарий.
Нужно, чтобы не триггерилась проверка аркадии на недостижимость проекта для автосборки.

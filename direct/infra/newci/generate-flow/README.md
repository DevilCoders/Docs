# Генерация a.yaml Директа

Для генерации достаточно выполнить `./generate.sh`.

Документация jinja2: https://jinja.palletsprojects.com/en/3.1.x/templates/#template-inheritance

Структура файлов:
- `templates/` &mdash; директория с шаблонами
- `templates/direct-logviewer.j2` &mdash; файл, из которого собирается `a.yaml`
- `templates/base/` &mdash; директория с базовыми шаблонами, использующимися во многих `a.yaml`
  https://jinja.palletsprojects.com/en/3.1.x/templates/#template-inheritance
- `templates/parts/` &mdash; директория с макросами, из которых построены шаблоны
  https://jinja.palletsprojects.com/en/3.1.x/templates/#macros
